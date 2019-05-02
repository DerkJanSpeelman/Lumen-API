If you see words you don't know, scroll to the bottom.

# Lumen API

Why [Lumen](https://lumen.laravel.com/)? Lumen is a micro-framework built on top of the Laravel framework. The framework is ideal for small apps and services that are optimized for speed. It's a good introduction to the MVC (Model View Controller) Pattern and [PHP](https://php.net/). Probably because PHP is developed in 1994 en became public in 1995, it has an immense community. And that makes it easier.

In order to follow this guide, the following requirements must be met:

 - PHP >= 7.1.3
 - Composer
 - PostgreSQL >= 11.2

Installation guides for both of these programs can be found everywhere online. Make sure to install the programs in this specific order. To check if these programs are already installed on your computer, or to check if you have updated to the versions you need. Open your terminal. On MacOS you can find the terminal by searching (`Command + Space`) for the _Terminal_ application. (I recommend installing iTerm if you're on a Mac) On Windows you can find the terminal by searching (`Windows + S`) for the _CMD_ application. Run these commands:

```sh
php -v
composer
psql --version
```

## Installation of Lumen

[Install Lumen](https://lumen.laravel.com/docs) using your shell or terminal. Open your terminal again if you closed it.

Navigate to the location where you want the project folder to be created. In your terminal you can navigate like this. Where `\Users\username\folder` is the location you want to navigate to.

```sh
cd \Users\username\folder
```

To install Lumen, run this command. Where `project-folder` is the name you want to give the genereated folder.

```sh
composer create-project --prefer-dist laravel/lumen project-folder
```

This will generate a bunge of files into `/project-folder`. Open the `.env` file in your favorite code-editor. I'm using [Atom](https://atom.io/), but feel free to use any other code-editor. Like [VSCode](https://code.visualstudio.com/), [Sublime Text](https://www.sublimetext.com/) or even [Notepad++](https://notepad-plus-plus.org/). Anything will do.

In the `.env` file you can see that the `APP_KEY=` is empty. We need this, though. So in order to generate the application key, we need to open `routes/web.php` and add a new route.

```php
<?php

/*
|--------------------------------------------------------------------------
| Application Routes
|--------------------------------------------------------------------------
|
| Here is where you can register all of the routes for an application.
| It is a breeze. Simply tell Lumen the URIs it should respond to
| and give it the Closure to call when that URI is requested.
|
*/

$router->get('/', function () use ($router) {
    return $router->app->version();
});

$router->get('/key', function() {
    return str_random(32);
});
```

This creates a completely new route on `http://localhost:8000/key`. Go there. Copy and paste the key as `APP_KEY` in your `.env`. For example, this could be: `APP_KEY=ksUQ93LoKdhW81K0JQY7FNnbvat72hN2` in your `.env` file. **Don't** copy this key, that's not secure.

## PostgreSQL

First of all: why PostgreSQL? To keep this answer as short as possible: we need a management system for managing data. So with or without PostgreSQL, we need a system like this. PostgreSQL supports much more data types compared to its competitors. We can even create our own data types. So PostgreSQL has a lot of capability. Built using an object-relational model, it supports complex structures and a breadth of built-in and user-defined data types. It provides extensive data capacity and is trusted for its data integrity. You may not need all of the advanced features PostgreSQL comes with, but since data needs can evolve quickly, there is undoubtedly clear benefit to having it all at your fingertips.

If you have not yet installed PostgreSQL, you should follow the installation guide on [postgresql.org](https://www.postgresql.org/). Take a look at: https://www.postgresql.org/docs/11/tutorial-install.html. Make sure to actually start Postgres: `pg_ctl -D /usr/local/var/postgres start`.

After you succesfully setup PostgreSQL run:

```sh
sudo -u postgres psql
```

This should take you to postgres. It might ask for a password, type in the password for your account on your computer as you would when logging in. This is an adminstator check. On Windows, if you are not an administrator, restart CMD as an administrator, or log into an account that is an administrator.

```sh
psql (11.2)
Type "help" for help.

postgres=#
```

Create a database and a user. Hit enter for each command.

```sh
CREATE DATABASE lumenapi;
CREATE USER lumenuser WITH ENCRYPTED PASSWORD 'lumenpass';
GRANT ALL PRIVILEGES ON DATABASE lumenapi TO lumenapiuser;
```

If the last line returns an error like `FATAL:  database "lumenapi" does not exist`. You should exit postgres by running `\q`. And run the following command: `createdb lumenapi`. After this, log back into postgres and grant all privileges to the user _lumenapiuser_ on the _lumenapi_ database again.

You can install on any PostgreSQL Client on your computer to get a better visualisation of your databases. Connect to `127.0.0.1:5432` and your user, password and database. Currently, the database is completely empty, so you will only be able to make a connection.

## Run

To actually run your application, you need to run:

```sh
php -S localhost:8000 -t public
```

This will serve the project on `http://localhost:8000/`. If this gives you an `Address already in use` error, try running your application on a different port by changing `8000` into `8080` (for example). For example, I have many projects running simultaneously, so I run this project on port 8085.

If you navigate in your favorite browser (i.e. [Chrome](https://www.google.com/chrome/)) to `http://localhost:8000/`, you shold see something like: **Lumen (5.8.4) (Laravel Components 5.8.\*)**

----------

# Words

| Word | Meaning |
| ------ | ------ |
| API (Application Programming Interface) | It's a set of clearly defined methods of communication among various components. A good API makes it easier to develop a computer program by providing all the building blocks. |
| Framework | An abstraction in which software providing generic functionality can be selectively changed by additional user-written code, thus providing application-specific software. A software framework is a universal, reusable software environment that provides particular functionality. |
| MVC (Model View Controller) | MVC design patterns decouples three major components (Models, Views, Controllers) allowing for efficient code reuse and parallel development. |
| MVC Model | Responsible for managing the data of the application. It receives input from the controller. |
| MVC View | The view means presentation of the model in a particular format. |
| MVC Controller | Responds to the input and performs interactions on the data model objects. The controller receives the input, optionally validates it and then passes the input to the model. |
| PHP | A general-purpose programming language _originally_ designed for web development. It's dynamic, but weak as well, which makes it easy to learn, but hard to master. |
