---
title: "Custom REST Resources in Drupal 8"
date: 2018-12-16
slug: "custom-rest-resources-drupal-8"
tags: ["site-building", "development", "drupal"]
description: "A step-by-step guide to building a custom REST endpoint in Drupal 8, illustrated with a decidedly important Arnold Schwarzenegger example."
draft: false
---

# Introduction

Drupal 8 is a great platform for storing structured data and exposing web service endpoints. This offers Drupal a competitive advantage when creating a decoupled application or building Drupal as part of a larger enterprise of systems. Core offers many complementary out-of-the-box features to publish web services and configure them in different ways. This includes roles/permissions, Rest Web Services, Serialization, Views, and more.

Since Drupal is so robust out of the box, it often minimizes the need for custom development. But, Drupal’s framework has support for any customized needs. The following article describes how to create a custom REST endpoint in Drupal 8, as we share how to conditionally return a quote from a provided Arnold Schwarzenegger movie.

# Development

Assuming you [have a custom module already created](https://www.drupal.org/docs/8/creating-custom-modules) and enabled, we can leverage the native autoloading features to register a new plugin class for a custom REST resource.

Place a new MyCustomResource.php class in your module’s src/Plugin/rest/resource directory. Create any missing directories as needed. The REST resource will automatically get discovered after [clearing the cache](https://www.drupal.org/docs/user_guide/en/prevent-cache-clear.html).  

Example 1: modules/my_custom_module/src/Plugin/rest/resource/[MyCustomResource.php](https://gist.github.com/nerdstein/9f5c71e40e6d073890cba9ea638d895b)

This example demonstrates an exposed GET endpoint found at the path /api/custom/arnold. Let’s walk through the code to get an understanding.

## Namespacing

If the PHP class is placed into a module’s src/Plugin/rest/resource directory, Drupal will automatically register the class and knows, given the path, to associate it with a REST resource. This is a common pattern leveraged by Drupal’s Plugin API.

## Annotation

Annotations define static attributes and configuration of the REST resource. Lines 16-27 demonstrate the annotation for the REST resource class. Most notably, a unique ID (no spaces and use of underscores) is shown in line 20 and a human recognizable label on line 21. Lines 23 and 24 define the endpoint for the API, for which requests can be made.

## Base Class

Classes are capable of implementing interfaces (a common, shared definition of expected functions) or extending base classes that have defined functions. Line 28 demonstrates the name of the custom class, which should match the filename per object oriented best practice. Extending ResourceBase as a base class allows us to inherit standard REST resource functionality and only needing to develop our specific functionality within our class.

## Dependency Injection

The use of an overridden __construct and the complementary create functions demonstrate how we use dependency injection to load additional system resources into our class. In this example, I load serialization formats, a specific logger, the current user, and the current request from Drupal’s runtime container. The request and current user extend the constructor of the ResourceBase class and saved into the currentUser and request attributes of a class instance defined in lines 35 and 42 respectively. This demonstrates how to extend your REST resource for any additional class attributes.

## Request Method

Web service endpoints define the expected methods of the request. Drupal’s REST resource plugins support requests by defining specific methods within the class. Line 99 demonstrates a get() method that corresponds to a GET request available from the endpoint. All code within this method is used to generate the response.

## Caching

Responses can be cached from the endpoint to help with performance. Lines 117-121 demonstrate specific caching directives that can be used at your discretion. In this example, I’ve set it to not cache requests.

## Response

Line 124 demonstrates the response triggered by returning a ResourceResponse object with the desired data.

# Configuration

Once REST resources are developed, they still require configuration. Start by downloading and enabling the [REST UI module](https://www.drupal.org/project/restui) to manage Drupal’s REST endpoints at /admin/config/services/rest.  You should see your new REST resource defined in the list.

![](/sites/default/files/uploaded/custom-rest-resource-1.png)

The REST resource endpoint will be activated once enabled and configured. Configuration includes selection of the exposed methods (from those available from your class), the authentication (select cookie to use Drupal’s default authentication tied to it’s login), and the serialization formats (JSON is commonly used for tools like React and Vue).

Finally, you need to define who is able to access the endpoint.

- Go to Drupal’s permissions page, found at /admin/people/permissions,

- Search for the permission tied to your REST resource, e.g. “access {METHOD} on {RESOURCE NAME} resource”, where method corresponds to the method defined in your class, like GET/POST/DELETE/PUT, and the resource name is the label in your class annotation.

- Select the applicable roles that you wish to access (which will be verified by your authentication method). Selecting anonymous will allow your endpoint to be publicly accessible.

# An Extended Example

The previous example outlined the basics of Drupal’s REST resource API but did not describe how to leverage other Drupal features. I’ve created a second example that is more relevant for retrieving Drupal-sponsored content.

Example 2: modules/my_custom_module/src/Plugin/rest/resource/[MyCustomResourceRandom.php](https://gist.github.com/nerdstein/417c8ef105205d8159386a26c771ee9b)

The updated example assumes the use of an “arnold_quotes” content type, which leverages the “title” field for the quote and has a boolean “bonus” field to tag specific quotes as a bonus feature. It also assumes the use of a custom permission for accessing bonus quotes, which can be assigned to a user by role.

The example leverages an [entity query](https://api.drupal.org/api/drupal/core!lib!Drupal.php/function/Drupal%3A%3AentityQuery/8.2.x) to conditionally load quotes to first filter by a movie parameter and bonus products, if the user has the correct permission. A random returned node is loaded and the quote is returned through the response.

Example 2 better exemplifies a use case for a custom REST resource in Drupal 8 and potential opportunities to interact with the other Drupal subsystems.

# Testing

Intuitively, you may go to a web browser to test your endpoint. But, web service endpoints are configured to only accept requests in specific serialized formats and methods. A standard web browser request likely won’t create a request that matches your endpoint settings, but Drupal will still return return a result that likely prints an error and is in the serialized format you selected (e.g. JSON).

The easiest way to test your endpoint is through a tool like [Postman](https://www.getpostman.com/). After downloading, configure a request to your endpoint.

- Specify the method (e.g. GET)

- Specify the full URL to the endpoint (e.g. [https://mysite.com/api/custom/arnold](https://mysite.com/api/custom/arnold))

- Add a parameter for “_format” and specify the desired response serialization format from one configured by the endpoint (e.g. “_format=json”)

- Add any other parameters for the endpoint (e.g. “movie=Predator”)

- Set a header for the correct mime type by setting “Content-Type” to “application/json” to match expected request serialization formats

- If authenticated, click “Cookies” and enter a cookie value for your Drupal site after logging in (you can get this from your browser)

- Click “Save” your Postman settings to persistently store

- Click “Send” to test the request

![](/sites/default/files/uploaded/custom-rest-resource-2.png)

![](/sites/default/files/uploaded/custom-rest-resource-3.png)

# Further Reading

More details can be found on the [official drupal.org documentation](https://www.drupal.org/docs/8/api/restful-web-services-api/custom-rest-resources). And, just as I was finishing the article, Open Sense Labs published [a similar article](https://opensenselabs.com/blog/tech/creating-custom-rest-resource-get-method-drupal-8) that is both helpful and explanatory.