# Getting Started
Before you start developing with Pantheon you will need to install some initial software and then begin setting up your projects. 

## Pantheon
Pantheon is our hosting and deployment center for development on several of our accounts. 

### Generate Machine Token
As part of the setup you will need to be logged into pantheon and generate a machine token from logging into pantheon account and going to User Dashboard > Account > Machine Tokens. Write this token value down - you’ll only see it once. After closing the window, if you forget this, you’ll need to generate a new one. This token will be used by both Lando and Terminus.

## Lando 
For any Pantheon based websites - we utilize Lando to develop locally. Lando is a specialized Docker wrapper for working with sites on Pantheon. Lando utilizes what they’ve branded as MultiDev environments, which you can think of as an isolated Docker Container connected to a Git branch.
For more details about working with Lando, see the official documentation here. 

### Installation Overview:
Below is a quick overview of how to install Lando on your system. For full details see the official documentation here.

1. Download the latest .dmg package from GitHub
2. Mount the DMG by double-clicking it
3. Double-click on the LandoInstaller.pkg
4. Go through the setup workflow
5. Enter your username and password when prompted

## Terminus
Official Terminus setup overview from Pantheon - https://pantheon.io/docs/terminus

### Install via Command Line:
Follow the commands below to install terminus. You can view the Official Instructions for any updated information. 

- Create a terminus folder in your home directory (~/) 
  - `mkdir ~/terminus && cd ~/terminus`
- Get the latest release tag of Terminus, download and save the release as ~/terminus/terminus 
  - `curl -L https://github.com/pantheon-systems/terminus/releases/download/$(curl --silent "https://api.github.com/repos/pantheon-systems/terminus/releases/latest" | perl -nle'print $& while m{"tag_name": "\K.*?(?=")}g')/terminus.phar --output terminus`
- Make the file executable 
  - `chmod +x terminus`
- Add a symlink to your local bin directory for the Terminus executable 
  - `sudo ln -s ~/terminus/terminus /usr/local/bin/terminus`
The first time you run terminus from the command line you will need to add you pantheon token and email address from the command line:
- `terminus auth:login --machine-token=‹machine-token›`
- `terminus auth:login --email=dev@example.com`

## Docker
The installations should have installed docker as part of the process. One thing to verify is the version. Newer versions of Docker may have issues. If you run into a problem, you may need to downgrade your Docker version. Currently we’ve had success using v2.5.0.1. This version and other older versions can be downloaded here: https://docs.docker.com/docker-for-mac/release-notes/ 

Once you have Lando, Terminus, and Docker installed, we can begin setting up local environments.


# Using Lando For A Project
The following sections will go over how to use Lando for local environment setup and general use.

The basic outline is that we will init a project in a directory, start the project, pull updates to the repo, files, and database, and then from there you can follow a relatively normal git style workflow. 

## Project Initialization
Open your terminal and create and/or navigate to the folder where you would like to clone the website to on your computer and follow the steps below:

- Run `lando init` in your terminal
- Select Pantheon for the first option
- Choose your personal username/email for the second option (if its your first time using lando, you may need your machine token as well)
- Select the project that you would like to use for the third option

After this your project should start downloading all of the resources that it needs to run locally. Essentially the docker side of things is getting setup with all the images and networks that it needs to get running. 

## Project Start
Now that your project has been initialized, you can spin up your local environment by running `lando start` in your terminal. If this is your first time spinning up the project, see the “Pulling In Repo, Files, and Database” section below to get your full website ready to use locally. Otherwise, you should see a list of local URL’s that are available to use for development. 

## Pulling In Repo, Files, and Database
With Pantheon/Lando you can pull down the files and database alongside of your git repository. After starting your project, you can do the following: 

- From project root folder, run lando pull in your terminal
- Pull Code From: Select `Live`
- Pull Database From: Select `Live`
- Pull Files From: Select `Live`

This will get you set up with the repository, database, and files from the live version of the website. This is a great starting point for any new project. See “Switching Environments” below for details on how to easily change from different environments.  


## Failed / Restore Database
Occasionally, the database may fail to download or you may break the database on your local install and want to restore it. 

First make sure there is a backup available on the pantheon environment you’d like to connect to (ex: dev, live, etc...). Once there’s a backup DB you can run a command like:

- `lando terminus backup:get bonterra.dev --element=db --to=/app/database.sql.gz`
- `lando db-import database.sql.gz`

Basically you change the “.dev” part of the 1st command to match the environment name you need to download (including Multidevs).


## Switching Environments
You may be in the primary Dev environment depending on how you set up your initial project. To switch to another environment, simply use the following command: `lando switch` to change to another environment (including Multidev environments). After entering this command, simply choose the environment you would like to use and whether you want to download the files, repo, and/or the database. 


## Committing & Pushing Changes
After you have made some changes from within your environment, you may be ready to commit those changes and push them up. To do this, use a normal Git workflow using `git add`, `git commit -m “Your message about updates here”` and `git push` to push your file changes up to the branch. If you prefer, you may also use a GUI tool such as Sourcetree, GitHub Desktop, GitKraken, or something similar. When any changes are pushed to a branch that is tied to a Multidev environment, the changes will be automatically rendered on the Multidev URL in a matter of moments. 


## Stopping An Environment
To shut down your local environment when you are done developing and wish to free up system resources, simply run `lando stop` from the root directory of the project to stop the environment from running on your local machine. This does not delete anything, it simply turns off the local environment.


## Creating A New Multidev
Setting up a new Multidev is essentially just attaching a Docker Container to Git Branch. This will give you a branch to work on as well as an isolated set of files and a database if needed as well. 

### Create new Multidev from the Pantheon Admin
With Pantheon, the best way to create a new multidev is from the website admin. Go to the Project you are working on and access the Multidev tab. From here you can create a new Multidev environment, names are limited to 11 characters. You will be able to choose the environment that you want to pull files, code, and databases from. Typically you should be pulling from the live site but in some cases it will make more sense to pull from another environment.

Note: You can create a git branch first, and then later have it turned into a Multidev. Just remember, the same 11 character limit will still apply. 

### Create new Multidev from the Command Line
You can technically also create a new multidev from the command line, however, this is not recommended. For more details, view the official documentation. 

<Site> = the pantheon site or project you are working on

<env> = The enviroment you would like to clone from, likely dev or live

<multidev> = the name of your new multidev environment

`terminus multidev:create --no-db --no-files -- <site>.<env> <multidev>`


## Using PHPmyAdmin
You can add PHPmyAdmin for basic database management. Simply go to the root folder of your project, find the .lando.yml file and open it. You will want to add/append the follow details to your file to connect PHPmyAdmin with your Lando powered site. Remember to update the {{YOUR_SITE_NAME}} with the name of the project you are working on. 

```
services:
 phpmyadmin:
   type: phpmyadmin
   hosts:
     - database
proxy:
 phpmyadmin:
   - phpmyadmin.{{YOUR_SITE_HERE}}.lndo.site
```
