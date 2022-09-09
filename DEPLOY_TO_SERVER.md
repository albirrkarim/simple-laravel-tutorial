# Deploy on self-hosted or VPS

In here i using ubuntu 20.04 and Nginx (whitout cpanel or site management system)

## A. Install

[Install Composer](https://getcomposer.org/download/)

[Install PHP](https://www.digitalocean.com/community/tutorials/how-to-install-php-8-1-and-set-up-a-local-development-environment-on-ubuntu-22-04)

[Install Node js via NVM](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04#option-3-installing-node-using-the-node-version-manager)

[Install Nginx](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)

[Install MySQL](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)


[Install phpmyadmin on nginx](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-20-04-server)

## B. Setting UP

### Place laravel

```
/home/admin/YOUR_LARAVEL
```

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

### Setting Nginx


Open the Nginx config file with

```
sudo nano /etc/nginx/sites-available/default
```

Add this code

```
server {
        root /home/admin/YOUR_LARAVEL/public;

        listen [::]:8000 ssl ipv6only=on;
        listen 8000 ssl;

        add_header Access-Control-Allow-Origin https://example.com;

        ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem; # managed by Certbot
        include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
```

Access the laravel with

```
https://example.com:8000
```