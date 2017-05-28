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

## Basic setup stuff

* Craete the database
    ```
    we will create following database mydrupl8site
    ```
* Add the site to host file
    ```
    host file can be found on folliwng url - win10
    C:\Windows\System32\drivers\etc
    
    127.0.0.1       loc.dup8.com
    ``` 
* Create the VirtualHost entry
    Open up the Xampp control panel and stop Apache (Ensure that you don’t have it running as a service, this is where doing so complicates things). Navigate to 
    ```
    C:/xampp/apache/conf/extra or wherever you installed xampp
    ```
    Fire up your text editor with administrative privileges and open up httpd-vhosts.conf found in the C:/xampp/apache/conf/extra folder. At the very bottom of the file paste the following: 
    ```
    NameVirtualHost *:80
    ```
    With out that line of code you will lose access to your default htdocs directory.
    Now copy and paste the code below .. below the first code
    ```
    <VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/mydrupl8site/web"
    ServerName loc.dup8.com
    ServerAlias loc.dup8.com.*.xip.io
    </VirtualHost>
    
    .*.xip.io - A super handy development thing from basecamp guys, you can substitute * with local ip of local computer and you can view webiste on iPad or iPhone    
    ```
    
* Create the Drush aliases file
    ```
    Craete drush aliase file on following location C:\Users\username\.drush\
    
    d8.aliases.drushrc.php
    
    d8 is site short code - you can name anyting you want
    
    <?php
    // Local site.
    $aliases["loc"] = array(
      'uri' => 'loc.dup8.com',
      'root' => 'C:/xampp/htdocs/mydrupl8site/web'
    );
    
    and loc is alias to this website
    
    ```

# Install Drupal with Drupal Console

Assuming you are in `mydrupl8site` directiry then navigate to `web` directory, run following command.

```
drupal site:install standard --site-name "My Drupal 8 Site" --langcode en --db-type mysql --db-port 3306 --db-user root --db-pass root --db-host 127.0.0.1 --db-name dup8 --site-mail admin@dup8.com --acount-name admin --acount-mail admin@dup8.com --acount-pass admin

OR

You can simply run short command


drupal site:install standard

but then it will ask you all required inputs one by one.

```

Bravo your Drupal 8 installation completed successfully :ok_hand:
