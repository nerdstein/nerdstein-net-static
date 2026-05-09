---
title: "Setting up your system for Drupal coding standards"
date: 2016-08-24
slug: "setting-your-system-drupal-coding-standards"
tags: ["development", "drupal"]
description: "As a bit of background, my main objective is to integrate Drupal coding standards into PHPStorm. I would imagine similar steps can be taken with other IDEs."
draft: false
---

As a bit of background, my main objective is to integrate Drupal coding standards into PHPStorm. I would imagine similar steps can be taken with other IDEs. I'm mainly writing this blog post to remind myself of these steps if/when I need to do this in the future. But, it occurred to me others might benefit from this as well.

## Dependencies

Composer is the lone dependency. And, bear in mind, the instructions are for PHPStorm.

## Installing tools

PHPCS is the defacto tool used to do code sniffing. And, Drupal has built in PHPCS libraries with it's Coder tool. 

- ``` composer global require "squizlabs/php_codesniffer=*" ```

- ``` composer global require "drupal/coder=>7" ```

Do not forget to add your composer bin directory to your path.

Now, your home directory will have the composer binaries for the projects. Drupal Coder libraries for PHPCS need to be moved into the PHPCS namespace to register the Drupal coding standards.

```

cp -R ~/.composer/vendor/drupal/coder/coder_sniffer/* ~/.composer/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards
```

**Update: **Manually copying Drupal Coder's standards will not update when you upgrade Coder (thank you, Owen Barton). As such, please use the following command to configure the installation path:

```

phpcs --config-set installed_paths ~/.composer/vendor/drupal/coder/coder_sniffer
```

## Setting up PHPStorm

PHPStorm has built in capability for PHP Code Sniffer and the ability to select the coding standard. 

- From the menu: PHPStorm > Preferences

- Languages & Frameworks > PHP > Code Sniffer

- Under "Development Environment" select the "..." icon

- Enter *~/.composer/vendor/squizlabs/php_codesniffer/scripts/phpcs* for the location, click "Validate" and then "OK"

This sets up the main scaffolding for the PHP Code Sniffing. Next you must configure your projects to inspect the code and select the standard.

- From the menu: PHPStorm > Preferences

- On the main preferences page, Editor > Inspections

- Expand PHP and check the box next to PHP Code Sniffer Validation

- Select "Drupal" as the standard

- Click "OK"