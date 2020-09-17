# Component-based Theming with Twig
This repository provides a detailed guide to setting up a local development environment that utilizes a Composer based workflow with Drupal 9.

Please ensure that you follow the directions outlined below to install and configure the necessary requirements for this training. We will not be able to cover these steps in class nor will we have time to stop class to assist with setting up laptops.

Below is a list of requirements that will ensure you get the most out of the training.

## Requirements
- Administrative rights to install and configure various applications
- DDEV (Docker based setup)
- Terminal
- Composer
- Node & NPM
- Gulp
- Git

### Administrative rights
You will need to ensure that you have administrative rights to install, configure or manage file permissions required by the list of tools outlined above.  If you do not have administrative rights, in the case of using a work laptop, then please have your company install the following items for you.


### Docker / DDEV
To eliminate the need for various setups that may involve different AMP (Apache/MySQL/PHP) stacks we recommend using a Container based setup using Docker and DDEV. You can verify the system requirements for DDEV by navigating to the [System Requirements](https://ddev.readthedocs.io/en/stable/#system-requirements) page and following the directions for your operating system.

### Terminal
The terminal is an interface in which we can execute text based commands.  It can be much faster to complete some tasks using a Terminal than with graphical applications and menus. The remaining requirements will be mostly ran from a Terminal using a series of command line prompts.  Take a moment to ensure that you have a Terminal (MAC) or Command Prompt (Windows) available to use.

We will be using the terminal window to work with tools such as `DDEV`, `Composer`, `NPM`, and `Gulp` throughout the training.  It is important to be comfortable using the command line as it should be part of any daily Front End development workflow.

### Composer
Composer (https://getcomposer.org/) is a dependency manager for PHP that allows us to perform a multitude of tasks; everything from creating a Drupal project to declaring libraries and even installing contributed modules. The advantage of using Composer is that it allows us to quickly install and update dependencies by simply running a few commands from a terminal window.

`DDEV` will allow us to run these commands without the need to physically install `Composer` on our computer or laptop.  We will revisit the various `Composer` commands that will be used during the training.

### Node & NPM
[Node](https://nodejs.org/en/) is a cross platform runtime environment for creating server side and networking applications. JavaScript running outside the browser. [NPM](https://www.npmjs.com/) is the package manager for JavaScript used to install, share, and distribute code and is used to manage dependencies in projects.

> We will be using NPM to manage dependencies when working with themes in Drupal 9.

`DDEV` will allow us to run these commands without the need to physically install `NPM` on our computer or laptop.  We will revisit the various `NPM` commands that will be used during the training.

### Gulp
[Gulp](https://gulpjs.com/) is a JavaScript task runner that allows us to perform repetitive tasks like minification, compilation, unit testing, linting and more. We use `Gulp` to compile Sass, Pattern Lab and watch for file changes during development.

`DDEV` will allow us to run these commands without the need to physically install `Gulp` on our computer or laptop.  We will revisit the various `Gulp` commands that will be used during the training.

## Using the training files and configuring Drupal

### Downloading the training files
Now that we have all the necessary requirements out of the way we can proceed to downloading a copy of the training files located within the Master branch.

Begin by locating the green `Clone or download` drop-down button and either choose **Download ZIP**.  Locate the zipped file named `components-develop.zip` and extract it's contents. Make sure to expand the `components-develop.zip` folder and rename the `components-develop` folder to `components`.  For sake of demonstration, I will be copying this folder to a directory called **Training**.

OR

Clone the repository to your computer by locating the green `Clone or download` drop-down button and copy the Clone with SSH path and run the similar command in your terminal window.

```
  git clone git@github.com:chazchumley/components.git
```
If you have chosen to clone the repository please make sure to remove the git origin remote as we will not be pushing any updates back up to the repository.  You can do this by entering the following command in your terminal window.

```
  git remote remove origin
```


### DDEV

To eliminate the need for various setups that may involve different **AMP** (Apache/MySQL/PHP) stacks and consider yousrself an advanced user then you can choose to use `DDEV` a Docker based development environment to work with PHP, MySQL and Drupal.  You can download and install DDEV for Windows, MACOS and Linux by navigating to the [Installation](https://ddev.readthedocs.io/en/stable/#installation) page and following the install prompts for your operating system.  Make sure to check the [System Requirements](https://ddev.readthedocs.io/en/stable/#system-requirements) prior to installing DDEV.

Once completed we will revisit how to use DDEV to import a Drupal 9 website as well as how to start a server, run composer, drush and import the initial database snapshot that will be used throughout the training.


### Setup
The initial setup of DDEV requires a .config configuration file which I have already provided in the .ddev folder of the project.  In order to initialize the Docker containers needed by DDEV we will need to execure the following commands within the terminal window.

```
  cd training/components
  ddev start
```

Once DDEV finishes spinning up the containers it will automatically scaffold up our Drupal 9 instance by running the composer install command, import our datbase, run any configuration and open the Drupal 9 website within a browser.

> Note: anytime we need to install, remove or update modules or depedencies DDEV requires the `ddev` prefix in order to execute these commands within the terminal window.

### Login to Drupal

We can login to Drupal using the following credentials:

- username: **admin**
- password: **admin**

## Working with the theme

The custom Drupal theme, `ohana` can be found in the `web/themes/custom` folder.  Commsnds to intersct wwith the theme can be ran from anywhere within the project.  In order to get started we will need to install the theme's dependencies and compile it.

### Installing theme dependencies

To ensure that we install and use the correct version of node declared in the `.nvmrc` file, we will need to enter the following commands in the terminal window:

```
  ddev nvm install && ddev nvm use
```

> We only need to run these last two command once.

Next we will need to install all of the node dependencies (Gulp, Pattern Lab, Browsersync, and others). We can do this by enterting the following command in the terminal window:

```
  ddev npm install
```

### Build/Compile the theme

To build the entire codebase for our theme, we will need to run the following command within the terminal window:

```
  ddev npm run build
```

### Run the watch task to access Pattern Lab

In order for us to preview our theme within Pattern Lab, we need to start the tasks needed to watch for new code changes within the theme, so it will automatically compile it and make it accessible to Drupal.  We can accomplish this by running the following command from the terminal window:

```
  ddev npm run watch
```

We should now be able to access Pattern Lab ny navigating to `https://components/ddev/site:3000` or by navigating to `http:localhost:3001` within our browser.

## Congratulations
We now have a Drupal 9 project with the `Ohana` theme enabled that we will be using throughout the remaining training. This Drupal 9 instance is configured with the latest best practices in mind for site building. This includes use of  Media, Paragraphs, various Twig modules and the Component libraries modules.

- Drupal 9 URL: `https://components.ddev.site`
- Pattern Lab URL: `https://components.ddev.site:3000`

This training does not cover site building but we will briefly discuss various decision made when implementing a component-based theme using Twig and Pattern Lab.