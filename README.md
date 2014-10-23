# bbPress

bbPress is forum software with a twist from the creators of WordPress. Easily setup discussion forums inside your WordPress.org powered site.

Have you ever been frustrated with forum or bulletin board software that was slow, bloated and always got your server hacked? bbPress is focused on ease of integration, ease of use, web standards, and speed.

We're keeping things as small and light as possible while still allowing for great add-on features through WordPress's extensive plugin system. What does all that mean? bbPress is lean, mean, and ready to take on any job you throw at it.

## The new development repo

As part of bbPress 2.6 we have revamped our development workflow to streamline and automate many of the tasks that come up day-to-day.

* Validate and test i18n support and generating *pot* files for easy translation into other languages
* Generate RTL CSS for our international locales that use *right-to-left* text such as Arabic and Hebrew
* Compile bbPress' admin themes SCSS into CSS
* Minimize CSS, RTL CSS and JavaScript files
* Validating our JavaScript files for errors and coding best practices
* PHPUnit testing framework for PHP integrated with Travis-CI

### The src directory

The `/src` directory is the bbPress core source. All of the existing bbPress core files have been moved into this directory. You’ll develop and test against this directory as usual, but the real power will come from using the rest of the tools in the repository. The contents are optimized for development, not production (this means uncompressed CSS and JavaScript files and uncompiled SCSS files).

### The tests directory

The `/tests` directory is where our PHPUnit tests are stored and makes testing a cinch, it also allows us to commit patches that include changes to both the source and the tests in a single commit.

### The root directory

The `/` direcory includes configuration files for our *build* tools, Travis CI and PHPUnit tests.

## Installing the tools

### Node.js

Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications.

Any of the following options will get Node.js installed for you:

* Visit [Node.js](http://nodejs.org/) and click on the *install* link to download Node.js
* If your a Mac user and have [Homebrew](http://brew.sh) installed `brew install node`
* If your a Windows user and have [Scoop](http://scoop.sh) installed `scoop install nodejs`

### Grunt

Grunt is a JavaScript task runner to automate the tasks outlined above.

First we need to install Grunt's command line interface (CLI).

1. Open a command shell terminal *You may need to use sudo (for OSX, *nix, BSD etc) or run your command shell as Administrator (for Windows)*
2. Type the following into your command shell `npm install -g grunt-cli`

## Checking out the bbPress source

You can use SVN or Git to contribute to bbPress, the choice is yours. so first you need to get a copy of our source

* [Installing SVN on a Mac](https://make.wordpress.org/core/handbook/installing-a-version-control-system/installing-svn-on-a-mac/)
* [Installing TortoiseSVN on Windows](https://make.wordpress.org/core/handbook/installing-a-version-control-system/installing-tortoisesvn/)
* [Installing GitHub for Mac](https://mac.github.com/)
* [Installing GitHub for Windows](https://windows.github.com/)

Once you've made that choice checkout of clone our repo If you’re fixing a bug, start by checking out bbPress' repository on your computer.

* `svn checkout http://bbpress.svn.wordpress.org/trunk`
* `git clone git://bbpress.git.wordpress.org/`
* `git clone https://github.com/bbpress/bbPress.git`

Note: Our GitHub mirror repo is *not* setup at this stage, soon, just not yet. See [Meta #637](https://meta.trac.wordpress.org/ticket/637)

## Installing Node.js dependancies with Node Package Manager (NPM)

NPM is included with Node.js and to install the dependancies we need

* Open up your terminal/command shell, you no longer need use sudu/admin
* Change to the directory where you checked out the source eg. `cd ~/dev/bbpress`
* Type the following into your command shell `npm install`

## Creating the build

* Open up your terminal/command shell, again, you no longer need use sudu/admin
* Change to the directory where you checked out the source eg. `cd ~/dev/bbpress`
* Type the following into your command shell `grunt`

## Overview of the Grunt tasks we use

### Build tasks.
The default task `grunt` or `grunt build` runs the following tasks in order:

1. `clean:all` - Cleans and deletes the entire `/build` folder
2. `copy:files` - Copies all the required files to the `/build` folder
3. `colors` - Compiles our admin themes SCSS and copies the compile CSS to the `/build` folder
4. `cssjanus:core` - Compiles the default CSS to RTL CSS in the `/build` folder
5. `cssmin:ltr` - Minimizes the default LTR CSS in the `/build` folder
6. `cssmin:rtl` - Minimizes the RTL CSS in the `/build` folder
7. `uglify:core` - Minimizes the JavaScript files in the `/build` folder
8. `jsvalidate:build` - Validates the JavaScript files for errors and coding best practices
9. `makepot` - Generates the `bbpress.pot` file for translators

The build release task `grunt build-release` tasks prepares everything we need to release a new version of bbPress on WordPress.org. Again the following tasks are run in order:

1. `clean:all` - Cleans and deletes the entire `/build` folder
2. `copy:files` - Copies all the required files to the `/build` folder
3. `colors` - Compiles our admin themes SCSS and copies the compile CSS to the `/build` folder
4. `cssjanus:core` - Compiles the default CSS to RTL CSS in the `/build` folder
5. `cssmin:ltr` - Minimizes the default LTR CSS in the `/build` folder
6. `cssmin:rtl` - Minimizes the RTL CSS in the `/build` folder
7. `uglify:core` - Minimizes the JavaScript files in the `/build` folder
8. `jsvalidate:build` - Validates the JavaScript files for errors and coding best practices
9. `checktextdomain` - Validates all of bbPress i18n text domains for internationalization
10. `makepot` - Generates the `bbpress.pot` file for translators
11. `phpunit` - Runs the PHPUnit tests for single site and multisite WordPress installs


### Testing tasks.

* `grunt phpunit` - Runs PHPUnit tests, including the ajax and multisite tests.
* `grunt jstest` - Runs both our javascript tasks `grunt jsvalidate` and `grunt jshint`


### Color schemes task.

* `grunt colors` - Compiles our admin themes SCSS and copies the compile CSS to the `/build` folder

### Patch task.

* `grunt patch` - List, download and patch bbPress like a boss eg. `grunt patch:2452`

### Watch task

* `grunt watch` or `grunt watch:all` Watches for file changes in the `/src` directory and automatically copy the updated file to the `/build` directory with any minification or RTL tasks included if nessecsary

## Patch All the Things! Creating and Submitting Patches

* [WordPress Core Handbook - Working with Patches](https://make.wordpress.org/core/handbook/working-with-patches/)
* [WordPress Core Handbook - Working with Patches](https://make.wordpress.org/core/handbook/working-with-patches/create-a-patch-using-tortoisesvn/)
* [WordPress Core Handbook - Working with Patches](https://make.wordpress.org/core/handbook/working-with-patches/apply-a-patch-using-tortoisesvn/)
* [WordPress Core Handbook - Working with Patches](https://make.wordpress.org/core/handbook/working-with-patches/patches-with-command-line/)
* [WordPress Core Blog - Git mirrors - Creating a patch with Git](https://make.wordpress.org/core/2014/01/15/git-mirrors-for-wordpress/)

### Bug Zapping

## Development Best Practices for Everyone

For best practices please refer to the information in the WordPress.org codex. You’ll find more information about [PHP](http://make.wordpress.org/core/handbook/coding-standards/php/), [HTML](http://make.wordpress.org/core/handbook/coding-standards/html/), [CSS](http://make.wordpress.org/core/handbook/coding-standards/css/) and [JavaScript](http://make.wordpress.org/core/handbook/coding-standards/javascript/) coding standards there.
