<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

# Purpose

This repository is a minimal example repository to show an issue during the installation of `joy/voyager-export` on recent version of Laravel.

## Environment

```shell
$ composer --version
Composer version 2.3.3 2022-04-01 22:15:35

$ php --version 
PHP 8.1.4 (cli) (built: Apr  4 2022 13:30:00) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.4, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.4, Copyright (c), by Zend Technologies

$ php artisan --version
Laravel Framework 9.7.0
```

## Issue

On a simple project, when I try to install `joy/voyager-export`, I get the following errors:
```shell
$ composer require joy/voyager-export -W
Using version ^1.2 for joy/voyager-export
./composer.json has been updated
Running composer update joy/voyager-export
Loading composer repositories with package information
Updating dependencies
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires joy/voyager-export ^1.2 -> satisfiable by joy/voyager-export[v1.2.1, ..., v1.2.17].
    - joy/voyager-export[v1.2.1, ..., v1.2.17] require illuminate/support ^7|^8 -> found illuminate/support[v7.0.0, ..., 7.x-dev, v8.0.0, ..., 8.x-dev] but these were not loaded, likely because it conflicts with another require.

You can also try re-running composer require with an explicit version constraint, e.g. "composer require joy/voyager-export:*" to figure out if any version is installable, or "composer require joy/voyager-export:^2.1" if you know which you need.

Installation failed, reverting ./composer.json and ./composer.lock to their original content.
```

## How this project was built

This project was built with the following commands:
```shell
# Step 0: create a fresh new Laravel project
$ composer create-project laravel/laravel joy-voyager-export-issue
$ cd joy-voyager-export-issue/
$ composer install
$ git init
$ git add .
$ git commit -m "first commit"

# Step 1: create a simple model Article
$ php artisan make:model Article -m
# TODO manually: Adjust migration and model file
# TODO manually: Create the correct database manually
# TODO manually: Adjust the .env file
$ git add app/Models/Article.php database/migrations/*_create_articles_table.php
$ git commit -m "Create article model."

# Step 2: install tcg/voyager
$ composer require tcg/voyager
$ php artisan voyager:install
$ git add .
$ git commit -m "Install tcg/voyager"

# Step 3: setup an admin account for tcg/voyager
$ php artisan voyager:admin your@email.com --create

$ php artisan serve

# TODO manually: check if tcg-voyager is available at http://127.0.0.1:8000/admin/login
# TODO manually: kill the web server

# Step 4: Try to install joy/voyager-export
$ composer require joy/voyager-export
Using version ^1.2 for joy/voyager-export
./composer.json has been updated
Running composer update joy/voyager-export
Loading composer repositories with package information
Updating dependencies
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires joy/voyager-export ^1.2 -> satisfiable by joy/voyager-export[v1.2.1, ..., v1.2.17].
    - joy/voyager-export[v1.2.1, ..., v1.2.17] require illuminate/support ^7|^8 -> found illuminate/support[v7.0.0, ..., 7.x-dev, v8.0.0, ..., 8.x-dev] but these were not loaded, likely because it conflicts with another require.

You can also try re-running composer require with an explicit version constraint, e.g. "composer require joy/voyager-export:*" to figure out if any version is installable, or "composer require joy/voyager-export:^2.1" if you know which you need.

Installation failed, reverting ./composer.json and ./composer.lock to their original content.
```

This procedure is inspired by [this tutorial](https://www.gekkode.com/developpement/laravel/tutoriel-laravel-8-pour-les-debutants/).
