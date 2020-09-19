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
- DDEV (Docker based setup)

### Administrative rights
You will need to ensure that you have administrative rights to install, configure or manage file permissions required by the list of tools outlined above.  If you do not have administrative rights, in the case of using a work laptop, then please have your company install the following items for you.

### Terminal
The terminal is an interface in which we can execute text based commands.  It can be much faster to complete some tasks using a Terminal than with graphical applications and menus. The remaining requirements will be mostly ran from a Terminal using a series of command line prompts.  Take a moment to ensure that you have a Terminal (MAC) or Command Prompt (Windows) available to use.

> We will be using the terminal window to work with tools such as `DDEV`, `Composer`, `NPM`, and `Gulp` throughout the training.  It is important to be comfortable using the command line as it should be part of any daily Front End development workflow.

### Composer
Composer (https://getcomposer.org/) is a dependency manager for PHP that allows us to perform a multitude of tasks; everything from creating a Drupal project to declaring libraries and even installing contributed modules. The advantage of using Composer is that it allows us to quickly install and update dependencies by simply running a few commands from a terminal window.

`DDEV` will allow us to run these commands without the need to physically install `Composer` on our computer or laptop.  We will revisit the various `Composer` commands that will be used later during the training.

### Node & NPM
[Node](https://nodejs.org/en/) is a cross platform runtime environment for creating server side and networking applications. JavaScript running outside the browser. [NPM](https://www.npmjs.com/) is the package manager for JavaScript used to install, share, and distribute code and is used to manage dependencies in projects.

> We will be using NPM to manage dependencies when working with themes in Drupal 9.

`DDEV` will allow us to run these commands without the need to physically install `NPM` on our computer or laptop.  We will revisit the various `NPM` commands that will be used later during the training.

### Gulp
[Gulp](https://gulpjs.com/) is a JavaScript task runner that allows us to perform repetitive tasks like minification, compilation, unit testing, linting and more. We use `Gulp` to compile Sass, Pattern Lab and watch for file changes during development.

`DDEV` will allow us to run these commands without the need to physically install `Gulp` on our computer or laptop.  We will revisit the various `Gulp` commands that will be used later during the training.

## Using the training files and configuring Drupal

### Downloading the training files
Now that we have all the necessary requirements out of the way we can proceed by either downloading a copy of the training files located within the `Develop` branch or if we are familiar with `Git` we may choose to clone the branch to our computer.

#### Downloading the repo
Begin by locating the green `Code` drop-down button at the top of the page and choose **Download ZIP**.  Locate the zipped file named `components-develop.zip` and extract it's contents. Make sure to rename the `components-develop` folder to `components`.

> For sake of training, we will be copying this folder to a new directory called **Training**.

#### Cloning the repo
If you prefer to clone the repository to your computer using `Git`, we can do so by locating the green `Code` drop-down button, selecting the `HTTPS` option and copying the path to our clipboard for use by running the following command in our terminal window.

```
  cd training
  git clone https://github.com/chazchumley/components.git
```

If you have chosen to clone the repository please make sure to remove the `git origin remote` as we will not be pushing any updates back up to the repository.  You can do this by entering the following command in our terminal window.

```
  cd training/components
  git remote remove origin
```

Now that we have a copy of the training files on our local computer it is time to use `DDEV` to create our Drupal 9 instance along with installing our theme and any dependencies it may need.  In order to do so we need to make sure we have `Docker` and `DDEV` installed on our computers.

> Note: We will only have to perform this install once.  We will be able to use both Docker and DDEV for future projects.

### Docker / DDEV
To eliminate the need for various setups that may involve different **AMP** (Apache/MySQL/PHP) stacks we have chosen to use `DDEV` a Docker based development environment to work with PHP, MySQL and Drupal.  Prior to installing `DDEV` we can verify the system requirements by navigating to the [System Requirements](https://ddev.readthedocs.io/en/stable/#system-requirements) page and following the directions for our operating system.

Once we have verified and/or met the System Requirements for DDEV, we can move on to the [Installation](https://ddev.readthedocs.io/en/stable/#installation) steps based on our operating system.

Once completed we will revisit how to use DDEV to import a Drupal 9 website as well as how to start a server, run composer, drush and import the initial database snapshot that will be used throughout the training.

### Setup
The initial setup of DDEV requires a configuration file which we have already provided located in the `.ddev` folder of the project.  In order to initialize the Docker containers needed by DDEV we will need to execure the following commands within the terminal window.

```
  cd training/components
  ddev start
```

> Note: If this is the first time ever starting DDEV, we may be prompted to send anonymous usage statisitics and errors.  This is completely up to you to opt in or opt out.

Once DDEV finishes spinning up the containers it will automatically scaffold up our Drupal 9 instance by running the composer install command, import our datbase, run any configuration and open the Drupal 9 website within a browser.

> Note: anytime we need to install, remove or update modules or depedencies DDEV requires the `ddev` prefix in order to execute these commands within the terminal window.

## Working with the theme
The custom Drupal theme, `ohana` can be found in the `web/themes/custom` folder and the first time `DDEV` opens our Drupal 9 website, it does not have access to our theme's compiled assets (CSS, Images, JS).  In order for Drupal to have access to those files we will need to install the theme's dependencies and compile it.

### Installing theme dependencies
To ensure that we install and use the correct version of `node` required by our theme, we will need to enter the following commands in the terminal window:

```
  ddev nvm install && ddev nvm use
```

> We only need to run these commands once.

Next we will need to install all of the node dependencies (Gulp, Pattern Lab, Browsersync, and others). We can do this by enterting the next command in the terminal window:

```
  ddev npm install
```

> This command will ensure our theme has all the dependencies it needs to be able to compile our codebase.

### Build/Compile the theme
To build the entire codebase for our theme, we will need to run the following command within the terminal window:

```
  ddev npm run build
```

> This commands builds our theme, assets and Pattern Lab

### Clear Drupal cache
While our theme has been built we currently will only be able to tell so by clearing Drupal's cache in the browser, where we will see a small change to our theme's font and color.  We can accomplish this by entering the following command in our terminal window.

```
  ddev drush cr
```

### Run the watch task to access Pattern Lab
In order for us to preview our theme within Pattern Lab, we need to start the watch task.  This command will listen for changes we make to various files and automatically compile it and make it accessible to Drupal.  We can accomplish this by running the following command from the terminal window:

```
  ddev npm run watch
```

We should now be able to access Pattern Lab by navigating either to `https://components.ddev.site:3000` or by navigating to `http://localhost:3001` within our browser.

## Congratulations
We now have a Drupal 9 project with the `Ohana` theme enabled. We will be using this theme throughout the remaining training. This Drupal 9 instance is configured with the latest best practices in mind for site building. This includes use of  Media, Paragraphs, various Twig modules and the Component libraries modules.

This training does not cover site building but we will briefly discuss various decision made when implementing a component-based theme using Twig and Pattern Lab.

## Drupal and Pattern Lab Links
- Drupal 9 URL: `https://components.ddev.site`
- Pattern Lab URL: `https://components.ddev.site:3000`

> Note: If you happen to be a Lando user or have been using another Docker based instance then you may need to modify the ports above to be something like https://components.ddev.site:8000

## Drupal Credentials
- username: **admin**
- password: **admin**