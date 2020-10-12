# Component-based Theming with Twig
This repository provides a detailed guide to setting up a local development environment that utilizes a Composer based workflow with Drupal 9.

Please ensure that you follow the directions outlined below to install and configure the necessary requirements for this training. We will not be able to cover these steps in class nor will we have time to stop class to assist with setting up laptops.

### Downloading the training files
Now that we have all the necessary requirements out of the way we can proceed by downloading a copy of the training files located within the `develop-lando` branch.

### Downloading the repo
Begin by locating the green `Code` drop-down button at the top of the page and choose **Download ZIP**.  Locate the zipped file named `components-develop.zip` and extract it's contents. Make sure to rename the `components-develop` folder to `components`.

> For sake of training, we will be copying this folder to a new directory called **Training**.

Now that we have a copy of the training files on our local computer it is time to use `Lando` to create our Drupal 9 instance along with installing our theme and any dependencies it may need.  In order to do so we need to make sure we have `Docker` and `Lando` installed on our computers.

> Note: We will only have to perform this install once.  We will be able to use both Docker and Lando for future projects.

### Docker / LANDO
To eliminate the need for various setups that may involve different **AMP** (Apache/MySQL/PHP) stacks we have chosen to use `LANDO` a Docker based development environment to work with PHP, MySQL and Drupal.  Prior to installing `LANDO` we can verify the system requirements by navigating to the [System Requirements](https://docs.lando.dev/basics/installation.html#system-requirements) page and following the directions for our operating system.

Once we have verified and/or met the System Requirements for `Lando`, we can move on to the installation steps based on our operating system.

Once completed we will revisit how to use `Lando` to import a Drupal 9 website as well as how to start a server, run composer, drush and import the initial database snapshot that will be used throughout the training.

### Setup
The initial setup of `Lando` requires a configuration file which we have already provided located in the root folder of the project.  In order to initialize the Docker containers needed by `Lando` we will need to execute the following commands within the terminal window.

```
  lando start
```

Once `Lando` finishes spinning up the containers we will need to scaffold up our Drupal 9 instance by running the following composer  command.

```
  lando composer install
```

> Note: anytime we need to install, remove or update modules or depedencies `Lando` requires the `lando` prefix in order to execute these commands within the terminal window.

### Importing the Database
If this is the first time setting up the traing file then we will want to import the database snapshot found in the `db` folder. We can execute the following commands within the terminal window.

```
  lando db-import db/components.sql.gz
```

### Running Database updates and importing configuration
To ensure we are following best practices it is a good habit to make sure the both the database is up to date and that we have imported the latest configuraiont files.  We can accomplish both these tasks using `Drush` which is a command line tool for working with Drupal 8/9.  Within our terminal window make sure to execute the following commands.

```
  lando drush updb -y && lando drush cim -y && lando drush cr
```

> Note: the first drush command tells Drupal to run database updates, while the second command tells Drupal to import any configurations files found in the `config` folder and the last command tells Drupal to rebuild the cache.  While outside the scope of our training, if you are interested in seeing all the various `Drush` commands we can visit the following link: [Drush Comands](https://drushcommands.com/).

## Working with the theme
The custom Drupal theme, `ohana` can be found in the `web/themes/custom` folder and the first time `Lando` opens our Drupal 9 website, it does not have access to our theme's compiled assets (CSS, Images, JS).  In order for Drupal to have access to those files we will need to install the theme's dependencies and compile it.

### Installing theme dependencies
We will need to install all of the node dependencies (Gulp, Pattern Lab, Browsersync, and others). We can do this by enterting the next command in the terminal window:

```
  cd web/themes/custom/ohana
  npm install
```

> This command will ensure our theme has all the dependencies it needs to be able to compile our codebase.

### Building the theme
To build the entire codebase for our theme, we will need to run the following command within the terminal window:

```
  npm run build
```

> This commands builds our theme, assets and Pattern Lab

## Accessing our site
We now have a Drupal 9 project with the `Ohana` theme enabled. We will be using this theme throughout the remaining training. This Drupal 9 instance is configured with the latest best practices in mind for site building. This includes use of  Media, Paragraphs, various Twig modules and the Component libraries modules.

This training does not cover site building but we will briefly discuss various decision made when implementing a component-based theme using Twig and Pattern Lab.

We can access the Drupal site by opening up a browser, navigating to the login screen and entering the credentials below.

### Drupal Site
- Drupal 9 URL: https://components.lndo.site

### Drupal Credentials
- username: **admin**
- password: **admin**

### Clearing Drupal cache
While our theme has been built we currently may not see all the default styling displayed.  This is often due to Drupal's theme layer not having registered the changes.  This is easy to resolve by clearing Drupal's cache.  We can accomplish this by entering the following command in our terminal window.

```
  lando drush cr
```

## Running the watch tasks
In order for us to preview our theme within Pattern Lab, we need to start the watch task.  This command will listen for changes we make to various files and automatically compile assets and make it accessible to Drupal.  We can accomplish this by running the following command from the terminal window:

```
  npm run watch
```

We should now be able to access Pattern Lab by navigating either to https://components.lndo.site:3000 or by navigating to http://localhost:3001 within our browser.

### Pattern Lab Links
- Pattern Lab URL: https://components.lndo.site:3000