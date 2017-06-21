+++
author = "JMN"
categories = ["Tech"]
date = "2017-06-03T23:47:51-07:00"
description = "In which we take a look at keeping a WordPress database synced across environments"
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "wordpress database syncing/migration"

+++

WordPress. A PHP based CMS with a MySQL database that generates pages as they are requested. Reviled. Loved. Free. Open Source. The most used content management system on the WWW. Make or choose any obnoxious plugin you want. Complain about that free plugin not being maintained well.

Whatever. Setting up a local development environment for WordPress (WP) has always been harder than it should have been for me but I won't be covering that here. Instead, I'll just give you a little peek into the way I keep my local, remote, and production site in sync and under version control. I expect the reader to have an understanding of the way that WordPress connects to it's database and how their server uses PHP to generate their WP pages. 

I'm working with an installation of Arch Linux, wp-cli v.1.2.1, and wp-sync-db v.1.5, PHP v.7.1.6

### The tools:
- Git
- wp-cli
- WP Sync DB

### The flow:
In my case, I will be the only one developing so I do all my work locally and then push up my changes to the staging server afterward. 

### Problems to consider:
You have the exact same version of PHP on your local machine than what you run on your production server. You have the exact versions of MySQL, your web server, and the config files are different too. Wait, you don't? Nooooo, this is going to require more attention than I anticipated. You'll still have to consider the differences in your development and production environments as you develop and troubleshoot. This is why I won't be covering local dev environment setup. 

Here are some solutions from reputable sources that have been recommended to me but that I HAVEN'T USED: You could also consider using [Vagrant](https://www.vagrantup.com/intro/index.html) to mirror your production server environment. Here's a thorough [Smashing Magazine article](https://www.smashingmagazine.com/2015/07/development-to-deployment-workflow/) that walks you through that. It looks very GUI but hey, they at least they hold your hand. 

### Down to it:

We'll assume we're starting a project from scratch. I initialize git in my working directory and then connect it to a github repository. Then I get into that project directory, and use wp-cli to drop in a freshly downloaded WP core.

Did you know how convenient [wp-cli](http://wp-cli.org/) was?

The wp-cli tool allows you to download, configure, install, and manage your WordPress site from the comfort of your commandline. It's a wonderful tool that will save you tons of time. Forget clicking through multiple menus and waiting for windows to load in order to just change a users password. It has tons of features and you can include commands in your scripts to automate site setup or user set up or plugin updates or ...

Alright, now you have the WordPress core downloaded into your folder. You then set up a database, link your database to your WP site by putting your credentials in your wp-config.php file, and installing. With the exception of the database creation, all those steps can be done with wp-cli.

We also need to make sure our .gitignore file is ignoring our wp-config.php file since we will have a different database in our different environments. In this setup we'll also push uploads across our local and remote sites but we'll do that using the wp-sync tool. We also install our wp-sync plugin.

A quick overview of the [wp-sync plugin](https://github.com/wp-sync-db). As the developer mentions on [the projects github info page](http://wp-sync-db.github.io), WP Sync DB is a copyleft clone of the paid-for [WP Migrate DB Pro](https://deliciousbrains.com/wp-migrate-db-pro) developed by delicious brains. The plugin facilitates database migrations. It allows to you to sync your databases in either direction, push or pull from whatever server you are from. It also has a great find and replace function that will be used when updating URLs when syncing from one environment to another. 

Cool. After you commit your local changes and push them to your remote repository you can go to your staging server and clone down the project.

Now you have the same files in both locations but you only have a database on your local installation. Set up a database for your staging server installation and configure a wp-config.php file to link the WP site to it. Now you have a functional WP site in both locations although their databases aren't synced.

Now all you have to do is access the wp-sync tool dashboard, link to your remote server with the provided connection ID, make your needed string substitutions (find&replace), and push your database! There are a range of options available when setting up your migration. For example, you could choose to only migrate certain tables or make a backup before you began the migration. 

This could be adjusted easily for the reverse situation. You have an existing site online that you want to set up locally for development. You would install a blank WP site on your staging server, install your wp-sync-db plugin on both sites, pull down the database from your live server onto your staging server, then do the same process down to your local machine making the necessary configuration changes as needed. Once you get through the initial setup the migrations are painless. 

Once you're using wp-cli there are fewer reason to use git to deploy a WP core. A potential use case: Your host will allow you to pull down a git project but you don't have access to the wp-cli tool. Whatever. If you wanted to just track your theme dev then you could just set up a git repo for that folder.
