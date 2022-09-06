This tutorial for laravel 8 in Mac OS

# Run Laravel on local

## A. Install

### We need apache and phpmyadmin (mysql)

Just download [xampp](https://www.apachefriends.org/download.html)

Everytime you need apache you can just activate it.

### Install Composer

Composer is dependencies manager for PHP. [Install composer via brew](https://formulae.brew.sh/formula/composer)

### Install PHP

I suggest 8.0. [install](https://www.google.com/search?q=install+php+8.0+brew)

## B. Setting UP

### Prepare dependencies

#### PHP dependencies

```
composer install
```

if the command above is error use

```
composer update
```

#### Node js dependencies

```
npm install
```

if you getting error, just force it

```
npm install -f
```

### Make Database

Goto phpmyadmin and create empty database. (just let it empty)

### Setting Up environment

We need `.env` file. where is that ? its not published in the repository because the `.gitignore`

How we can get it ? we can copy `.env.example` then rename it to `.env`

Look this section

```
DB_DATABASE=YOUR_DATABASE_NAME
DB_USERNAME=root
DB_PASSWORD=
```

### Migrate database

```
php artisan migrate
```

### Generate Secret for JWT

```
php artisan jwt:secret
```

### Generate Key

```
php artisan key:generate
```

### Storage Link

```
php artisan storage:link
```

This command will create symbolic link in `public` folder. link to `storage/app/public`

## C. Run

### Run the laravel (PHP)
run command in laravel directory

```
php artisan serve
```

### Compile Build asset / Watch (Node js)

Im use laravel mix.

If you want upload on server -> Make Production Asset

```
npm run prod
```

If you want develop and editing the react js code -> Tell laravel mix to watch code changes.

```
npm run watch
```