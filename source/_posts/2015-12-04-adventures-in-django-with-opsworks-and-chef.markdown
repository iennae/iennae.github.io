---
layout: post
title: "Adventures in Django with OpsWorks and Chef"
date: 2015-12-04 23:34:07 -0800
comments: true
categories: 
---

Recently I had the opportunity to work with the new released [OpsWorks Chef 12 for Linux](http://blogs.aws.amazon.com/application-management/post/Tx1T5HNA1TSU8NH/AWS-OpsWorks-Now-Supports-Chef-12-for-Linux). I wrote up a process to deploy Django with the [application_python](https://supermarket.chef.io/cookbooks/application_python) cookbook walking through a sample deploy.

I learned quite a bit of Django in the process and found some great resources in the process. The following is just a snippet of that information.

## Django Terminology

Django is a free and open source web application framework written in Python.

Web application frameworks provide a set of components that are common across applications allowing an individual to speed up development and deployment of a web application. Functionality like user authentication and authorization, forms, file management, are some examples of these common components. These frameworks exist to speed up delivery so that you don't have to reinvent the wheel each time you want to create a site.

Within Django, an app is a Web application that does something, for example a poll app. Within Django, a project is a collection of apps and configurations. An app can be in multiple projects.

Django follows the MVC(Model View Controller) architectural pattern. In the MVC architectural pattern, the model handls all the data and business logic, the view presents data to the user in the supported format and layout, and the controller receives the requests (HTTP GET or POST for example), coordinates, and calls the appropriate resources to carry them out.

When creating a web application, we generally create a set of controllers, models, and views. The reason that it uses this pattern is to provide some separation between the presentation (what the user sees) and the application logic.

In Django, the view pattern is implemented through an abstraction called a template and the controller pattern is implemented through an abstraction called a view.


## Further Resources

* [Django Resources](https://code.djangoproject.com/wiki/DjangoResources)
* [Django Digital Ocean tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-centos-7)
* [Deploying a Django application tutorial](http://python-deploy-framework.readthedocs.org/en/latest/pages/django-deployment.html)
* [Dpaste docs](http://dpaste.readthedocs.org/en/latest/integration.html)