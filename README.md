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

First you need to [install composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

> Note: The instructions below refer to the [global composer installation](https://getcomposer.org/doc/00-intro.md#globally).
You might need to replace `composer` with `php composer.phar` (or similar) 
for your setup.

After that you can create the project:

```
composer create-project --stability dev --no-interaction --no-install drupal/composer/drupal-project:8.x-dev mydrupl8site
```
The `composer create-project` command passes ownership of all files to the project that is created.

```
cd mydrupl8site
composer clear-cache
```
and

```
composer update
```
And this will install all the packages we need,  e.g. twig, guzzle etc. If you see your installation there are few directories, the `web` directory is actually the core of drupal. `composer.lock` as the numage suggest its lock your version to a specific version so when you install `dev` version of module e.g. it will lock the specific version of that dev module so that anywhere else you install it on a staging or prodcution environment, you will know that you will be getting exact same version of that you used on your development machine.

# What does the template do?

When installing the given `composer.json` some tasks are taken care of:

* Drupal will be installed in the `web`-directory.
* Autoloader is implemented to use the generated composer autoloader in `vendor/autoload.php`,
  instead of the one provided by Drupal (`web/vendor/autoload.php`).
* Modules (packages of type `drupal-module`) will be placed in `web/modules/contrib/`
* Theme (packages of type `drupal-theme`) will be placed in `web/themes/contrib/`
* Profiles (packages of type `drupal-profile`) will be placed in `web/profiles/contrib/`
* Creates default writable versions of `settings.php` and `services.yml`.
* Creates `web/sites/default/files`-directory.
* Latest version of drush is installed locally for use at `vendor/bin/drush`.
* Latest version of DrupalConsole is installed locally for use at `vendor/bin/drupal`.
