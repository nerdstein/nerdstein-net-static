---
title: "Local Drupal development sandboxes"
date: 2014-08-04
slug: "local-drupal-development-sandboxes"
tags: ["development", "drupal"]
description: "If you're doing Drupal development, having a local sandbox is a necessity. Why? No one should be making untested changes on a production or staging server."
draft: false
---

If you're doing Drupal development, having a local sandbox is a necessity. Why? **No one** should be making untested changes on a production or staging server. And, a development server should be free of initial development errors where the developer should execute a small set of engineering tests before deployment. Plus, it can be time consuming to regularly deploy code developed locally onto a development server. To summarize: a local sandbox is absolutely best practice. I hope to summarize how to quickly get up to speed without having to rehash the lessons I have learned.

 

## Disclaimer

This blog posts makes some high level assumptions. First, you have a working knowledge of exporting Drupal configuration. This blog post is certainly not a "how-to" for Features, but I highly recommend you use it if you are currently not. The second, you understand how to use Git or another version control platform with comparable functionality. The third, we assume you are maintaining your entire docroot within the Git repository. And, lastly, you have a high level knowledge of configuring web servers and your computer's hosts file.

 

## Design Goals

The principle goal is to mimic whatever environment your Drupal site runs on. A second goal is to not build the environment on top of your principle operating system, where you develop the code. A third goal is to not have to develop on a remote server. These use cases are solved by installing a virtual machine.

 

## Step One: Infrastructure

To start things off, install a virtual machine platform (for example: VirtualBox or VMWare Fusion) and install Vagrant.

Next, identify a Vagrant box that comes pre-built with features that mimic your environment. There are many community adopted boxes that come pre-configured to run Drupal sites locally. To determine the right fit, evaluate the Chef (or Puppet) recipes that come with the Vagrant box. For Drupal, I highly recommend starting with recipes for the typical Linux, Apache, MySQL, and PHP stack. Then, add in your desired recipes like Drush, Git, Solr, Varnish and Memcache based on your environment. If your environment has other requirements, the Chef community has a wealth of different recipes to use. 

 

## Step Two: Setup and Workflow

The goal of the set up will be to get a fully provisioned site that runs from the code found in your repository. I have found it is extremely beneficial to set up your local sandbox as a multisite that is not maintained in your Git repository.

Start by provisioning the virtual machine. This should be executed within the Vagrant box directory.

> vagrant up

This command will build the virtual machine and configure the recipes. You then need to SSH into your new virtual machine.

> vagrant ssh

Clone your site repository into your VM. Most boxes will have a docroot in which Apache is serving up a default site. Adjust Apache's default virtual host configuration to point to your repository's docroot (more details can be found in [this linux.com blog post](http://www.linux.com/news/enterprise/systems-management/8202-how-to-set-up-apache-virtual-hosting)). You will need to restart Apache to load this change. Finally, install your site:

> drush si --site-subdir=<*development site URL*>

This command should be executed from the docroot of the site. Please note the parameter for the development site URL. This should match Apache's virtual host and the URL used to access the site from Vagrant. 

Some Vagrant boxes do not automatically add the new virtual hosts to your hosts file. If you cannot access the new Apache server from your host machine, alter your computer's hosts file to route the development site URL to the IP address of the Vagrant machine defined in it's configuration (more details can be found in [this howtogeek.com blog post](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/)).

At this point you should be able access your new Drupal site by going to the URL.

The last step for set up is to alter your Git repository configuration to ignore your multisite. Assume your multisite resides at *docroot/sites/development.local *within your repository. To ignore all files in that directory, edit your the .*gitignore* file in the root of the repository. Append a line for your multisite, for example: *docroot/sites/development.local *which will ignore all file paths that contain your local multisite.

 

## Step Three: Operations and Maintenance

Now that you have set up your infrastructure, I wanted to share some tips on how to be dangerous.

The first is simply a reminder that you are using Drupal's multisite feature. As such, any Drush commands would need to be run with an additional parameter: 

> *--uri=development.local*

One common example of a Drush command is loading a database backup from an external server. This example assumes you have a SQL file, preferably stored within your multisite directory to avoid unintentionally committing this to the repository. I highly recommend that you load the most current database before beginning development on a new feature.

> drush sql-query --uri=*development.local* sql-connect --file=database_backup.sql

For a distributed team, the repository will be updated regularly with new code. As I mentioned earlier, it is best practice to use a tool like Features to export code. And, generally speaking, any new module or module update may require database updates. Anytime I am starting to develop a new feature, I make sure to run the following commands:

> git pull
> drush updb --uri=*development.local* -y
> drush fra --uri=*development.local* -y
> git checkout -b <*new branch name*>

Each command in the script performs the following actions: *Command 1*. It pulls down any recently committed code. *Command 2*. It performs all of Drupal’s database updates from any code that requires schematic changes. *Command 3*. It reverts all of your system’s features to their representation in code (**note**: use this with caution if you have local changes you wish to keep). *Command 4*. It creates a new branch in your repository to begin building code for your new feature.

Lastly, Vagrant is a very powerful tool. There are a few commands I have found to be extremely beneficial, especially when working on multiple projects. As a recommendation, I would avoid running many virtual machines simultaneously. This can conflict with any Vagrant configuration needed to bootstrap the virtual machine and use a significant amount of host resources. As such the *vagrant suspend* command will allow you to gracefully save the state of your virtual machine. When you are ready to work on the site again, *vagrant resume* will restore the machine.

 

## Bonus Points

The aforementioned steps will yield a fully functional development environment. There are some other tips that can help for specific use cases.

Drush aliases can be used to help connect with remote servers. This assumes a valid SSH connection. Your local multisite can also be set up as a Drush alias, instead of having to pass the *uri* parameter. This can be incredibly useful to pull down both a remote database and the remote file contents by leveraging *drush sql-dump* and *drush rsync*. 

Finally, the issue of development-specific modules. All code that is intended only for your development can be stored in your multisite's modules subdirectory. Git will then ignore unnecessary development-specific code from being committed (e.g. Coder or Devel modules). If you do want code to be committed, simply move the code out of your multisite (e.g. *sites/all/modules*).

 

## Conclusion

Local development can be complicated, but hopefully this helps!