# Drupal 8 Sites with Composer and Configuration Management

We will cover how to build and maintain a site with Composer, as well as how to use Configuration Management to push changes from a local environment to a production one.

## What is Composer?

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

## What is Configuration Management?

Drupal 8 has a whole new configuration system to store configuration data in a consistent manner. All of your site configuration from enabled modules, through to content types, taxonomy vocabularies, fields, and views.

Exporting and importing configuration changes between a Drupal installation in different environments, such as Development, Staging, and Production, allows you to make and verify your changes with a comfortable distance from your site's live environment. 

This allows you to deploy a configuration from one environment to another (as a precaution, Drupal checks the site is the same before importing, by comparing its UUID).

## Prerequisites

You will need to have the following installed before you can follow.

* [Composer](https://getcomposer.org/)
* [Git](https://git-scm.com/)
* Drush – Install globally that will make your life easier

## Installing Drupal 8

We will Install Composer template for Drupal projects.
