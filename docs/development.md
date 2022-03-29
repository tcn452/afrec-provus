# Development

* [Docksal Commands](#docksal-commands)
* [Installation](#installation-setup)
* [Testing](#testing)
* [Theming](#theming)
* [Getting Updates](#getting-updates)
* [Deployment](#deployment)

## Installation & Setup

[Install Docksal](https://docs.docksal.io/getting-started/setup/).

Once you've setup docker run:

``fin init``

This will install the database and get you all ready to roll.

### Setup git remote

Add your remote git project from Pantheon or Acquia as ``git remote add deploy [remote-git-url]``.

### Add Terminus Settings

For Pantheon projects add your pantheon token as ``SECRET_TERMINUS_TOKEN=`` to ``./docsal/docksal-local.env`` and restart docksal (``fin restart``) to use Terminus.

## Docksal Commands

Provus uses [Docksal](http://docksal.io) for local development and in the CI. In additon to basic commands we also include:

```bash

Custom commands:
  behat                    	Test behat
  build-artifacts          	Builds sites files. 
  build-theme              	Builds theme dist files. Not currently necessary 
  deploy                   	Deploy to dev branch 
  drupal-coreupdate        	Updates Drupal Core when in TravisCI cron or from local.
  init                     	Initialize stack and site (full reset)
  init-site                	Initialize/reinstall site
  pa11y                    	Test pa11y 
  php-cbf                  	Runs PHPCBF on modules 
  php-cs                   	Runs PHPCS on modules 
  phpunit                  	Runs PHPUnit tests found in custom code
  site-mode                	Site site mode 
  storybook                	Run storybook tool locally 
  storybook-deploy         	Deploy storybook by pushing to "storybook" branch. 
  test                     	Test site installation
  test-content             	Imports test content 
  theme-lint               	lint theme js

```

### Testing

This repo includes bethat, phpunit, pa11y, and cypress tests and docksal commands:

  * cypress ``fin cypress``
  * phpUnit ``fin phpunit``
  * behat ``fin behat``
  * pa11y ``fin pa11y``
  
## Theming

This repository includes a theme that uses [Emulsify](http://emulsify.io). See the [Emulsify docs](http://docs.emulsify.io) for more info.

### Compiling Theme Updates

1. Edit scss or js files.
2. Run ``fin build-theme`` to compile sass files

To "watch" the files update in real-time run storybook command below.

### Storybook

#### Run Locally

To run Storybook ``fin storybook`` and click on the local network link:

![image](https://user-images.githubusercontent.com/512243/74872340-0ae99200-532b-11ea-9f67-2b4a4c68ea89.png)

## Getting Updates

After a site is properly setup to run with Acquia, Pantheon, or other hosting service, run the following commands to get updates.

### Start Over

``fin init`` or ``fin init-site`` (the same as the former but doesn't rebuild the containers) to start from an installed or recently updated state.

### Database updates

``fin pull db`` to get a most recent database update.

### Files updates

``fin pull files`` to get an updated files directory from the host.

## Deployment

The command ``fin build-artifacts`` prepares the site for deployment. The commands ``fin deploy`` is set to push a built artifact when a tag or the develop branch is built from. By default ``fin deploy`` is run in TravisCI to push updates to the develop branch or when a new tag is pushed.

### Pantheon

To push work to the Pantheon Dev environment from local, assuming you are on branch release-v1.2.3 and want to push it to Pantheon Dev:

``git push deploy release-v1.2.3:master``

Note – With Pantheon, you can only push code from local to Dev via the “master” branch in Pantheon’s repo; pushing from Dev to Staging and from Staging to Prod must be done via the Pantheon UI.

### Acquia

To push work to Acquia from local, just push the desired release name:

``git push deploy release-v1.2.3``






