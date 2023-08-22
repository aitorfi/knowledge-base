---
layout: default
title: Setting It Up
parent: Laravel
nav_order: 1
---

# Setting It Up

1. Run `sudo apt install php libapache2-mod-php -y` to install php and the php extension for apache2 if they are not installed yet.
2. Install composer following the [official guide](https://getcomposer.org/download/).
3. Install Laravel with the following command: `$ composer global require laravel/installer`.
4. Make sure all the [php extensions required by Laravel](https://laravel.com/docs/5.8/installation#server-requirements) are installed running the following command: `sudo apt install openssl php-common php-curl php-json php-mbstring php-mysql php-xml php-zip`.
5. Add the directory `~/composer/vendor/bin` to the `$PATH` environment variable by editing the `/etc/environment` file, if the `~/composer/vendor/bin` directory does not exist check for `~/.config/composer/vendor/bin`.
6. To create a new project run `laravel new myapp` or alternatively `composer create-project --prefer-dist laravel/laravel myapp`.
7. To run the application use the command `php artisan serve`, the output of the command will indicate the port on which the application is running.
