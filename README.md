# Component-based Theming with Twig
This repository provides a detailed guide to setting up a local development environment that utilizes a Composer based workflow with Drupal 9.

Please ensure that you follow the directions outlined below to install and configure the necessary requirements for this training. We will not be able to cover these steps in class nor will we have time to stop class to assist with setting up laptops.

Below is a list of requirements that will ensure you get the most out of the training.

## Requirements
- Administrative rights to install and configure various applications
- Terminal
- Composer
- Node & NPM
- Gulp
- Git
- LAMP (Docker, VM, DDEV, Lando, MAMP...)

> There is no preference for our LAMP setup.  It is best to use what you are most comfortable using.  You will need to make sure that you can import the database, run composer, drush, npm and gulp commands in a terminal window.

### Administrative rights
You will need to ensure that you have administrative rights to install, configure or manage file permissions required by the list of tools outlined above.  If you do not have administrative rights, in the case of using a work laptop, then please have your company install the following items for you.

### Terminal
The terminal is an interface in which we can execute text based commands.  It can be much faster to complete some tasks using a Terminal than with graphical applications and menus. The remaining requirements will be mostly ran from a Terminal using a series of command line prompts.  Take a moment to ensure that you have a Terminal (MAC) or Command Prompt (Windows) available to use.

> We will be using the terminal window to work with tools such as `Composer`, `Drush`, `NPM`, and `Gulp` throughout the training.  It is important to be comfortable using the command line as it should be part of any daily Front End development workflow.

### Composer
Composer (https://getcomposer.org/) is a dependency manager for PHP that allows us to perform a multitude of tasks; everything from creating a Drupal project to declaring libraries and even installing contributed modules. The advantage of using Composer is that it allows us to quickly install and update dependencies by simply running a few commands from a terminal window.  We can download and install `Composer` by following the [Getting Started](https://getcomposer.org/doc/00-intro.md) documentation for your specific opearting system.

> We will want to install Composer globally so make sure to read the directions for [Globally installing](https://getcomposer.org/doc/00-intro.md#globally).

### Node & NPM
[Node](https://nodejs.org/en/) is a cross platform runtime environment for creating server side and networking applications. JavaScript running outside the browser. [NPM](https://www.npmjs.com/) is the package manager for JavaScript used to install, share, and distribute code and is used to manage dependencies in projects.

We will need to [install](https://nodejs.org/en/download/) the latest version of `Node` by choosing the correct version for your operating system.

> `NPM` automatically comes with `Node` so we will not need to install `NPM` seperately. We will be using NPM to manage dependencies when working with themes in Drupal 9.

### Gulp
[Gulp](https://gulpjs.com/) is a JavaScript task runner that allows us to perform repetitive tasks like minification, compilation, unit testing, linting and more. We use `Gulp` to compile Sass, Pattern Lab and watch for file changes during development.

We will want to install `Gulp` globally on our operating system.  Since we installed `Node` previously, we can easily install `Gulp` by opening a terminal window and running the following commands:

```
  npm install --global gulp-cli
```

> The command above will not work unless you have `npm` installed.  If you need more information follow the [Quick Start](https://gulpjs.com/docs/en/getting-started/quick-start) guide.

## Using the training files and configuring Drupal
These next steps will vary based on how you prefer to setup your local development environment.  Most organizations have moved away from virtual machines or standalone `LAMP` environment such as MAMP, WAMP or Acquia Dev Desktop for doing Drupal development.  In it's place is the use of container based environments that utilize `Docker`.

### Optional Branches
If you would like to use `DDEV` or `LANDO` which are wrapper for `Docker` then you can checkout either the [develop-ddev](https://github.com/chazchumley/components/tree/develop-ddev) or [develop-lando](https://github.com/chazchumley/components/tree/develop-lando) branches I have setup.

If you prefer to setup the rest of the project using something else, then you will need to be able to scaffold a Drupal project, Import the database snapshot provided and be able to run various commands using the tools we installed previously.

> **The remaining setup assumes you are not using `DDEV` or `LANDO`**.

### Downloading the training files
Now that we have all the necessary requirements out of the way we can proceed by either downloading a copy of the training files located within the `Develop` branch.

#### Downloading the repo
Begin by locating the green `Code` drop-down button at the top of the page and choose **Download ZIP**.  Locate the zipped file named `components-develop.zip` and extract it's contents. Make sure to rename the `components-develop` folder to `components`.

> For sake of training, we will be copying this folder to a new directory called **Training**.

Now that we have a copy of the training files on our local computer it is time to create our Drupal 9 instance along with installing our theme and any dependencies it may need.

> Note: We will only have to perform this install once.

### Setup
The initial setup of Drupal requires us to run `composer` to scaffold up are instance based on the configuration provided. We will need to execure the following commands within the terminal window.

```
  cd training/components
  composer install
```

> Note: anytime we need to install, remove or update modules or depedencies we will need to use `composer` within the terminal window.

### Importing the database
If you prefer to not got thru the typical Drupal 9 setup and would like to instead use the provided database snapshot, you can find the snapshot in the `db` folder.  Feel free to use a command line or GUI to import the database into your Drupal setup.

## Working with the theme
The custom Drupal theme, `ohana` can be found in the `web/themes/custom` folder and the first time we preview our Drupal 9 website, it does not have access to our theme's compiled assets (CSS, Images, JS).  In order for Drupal to have access to those files we will need to install the theme's dependencies and compile it.

### Installing theme dependencies
Next we will need to install all of the node dependencies (Gulp, Pattern Lab, Browsersync, and others). We can do this by enterting the following commands in the terminal window:

```
  cd web/themes/custom/ohana
  npm install
```

> This command will ensure our theme has all the dependencies it needs to be able to compile our codebase.

### Build/Compile the theme
To build the entire codebase for our theme, we will need to run the following command within the terminal window:

```
  npm run build
```

> This commands builds our theme, assets and Pattern Lab

### Clear Drupal cache
While our theme has been built we currently will only be able to tell so by clearing Drupal's cache in the browser, where we will see a small change to our theme's font and color.  We can accomplish this by entering the following command in our terminal window.

```
  drush cr
```

### Run the watch task to access Pattern Lab
In order for us to preview our theme within Pattern Lab, we need to start the watch task.  This command will listen for changes we make to various files and automatically compile it and make it accessible to Drupal.  We can accomplish this by running the following command from the terminal window:

```
  npm run watch
```

We should now be able to access Pattern Lab by navigating to http://localhost:3000 within our browser.

## Congratulations
We now have a Drupal 9 project with the `Ohana` theme enabled. We will be using this theme throughout the remaining training. This Drupal 9 instance is configured with the latest best practices in mind for site building. This includes use of  Media, Paragraphs, various Twig modules and the Component libraries modules.

This training does not cover site building but we will briefly discuss various decision made when implementing a component-based theme using Twig and Pattern Lab.

## Drupal Credentials
- username: **admin**
- password: **admin**