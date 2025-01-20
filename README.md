# PHP Check out

Current PHP version is `8.4.3`.


There are many ways to run php web application, here we have check out of several ways how to do it from scratch.

## 1. Ubuntu - PHP in Apache as a module

### Installing Apache
```sh
sudo apt update
sudo apt install apache2
```

### Check opened ports
```sh
sudo apt install net-tools
sudo netstat -ntlp
```

### Install PHP

You’ll also need `libapache2-mod-php` to enable Apache to handle PHP files and wrking as a Apache module. 

```sh
sudo add-apt-repository ppa:ondrej/php
sudo apt install php8.4 libapache2-mod-php
```

PHP is working with Apache as a module, `php.ini` file is located in `apache2` subdirectory, like `/etc/php/8.4/apache2/php.ini`.


## 2. Ubuntu - PHP with NginX as an FPM workers

### Install NginX
```
sudo apt update
sudo apt install nginx
```

Check NginX is working.
```
systemctl status nginx
```

### Install PHP-FPM
```
sudo apt install php-fpm8.4 -y
```
Output for `php-fpm -v`
```
PHP 8.4.3 (fpm-fcgi) (built: Jan 19 2025 14:20:58) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.4.3, Copyright (c) Zend Technologies
    with Zend OPcache v8.4.3, Copyright (c), by Zend Technologies
```

To check PHP-FPM is working, type:
```
sudo service php8.4-fpm status
```

### Configure NginX to work with PHP-FPM
Example file `/etc/nginx/sites-availabe/sample`
```
server {
         listen       80;
         server_name  sample-domain.com;
         root         /var/www/html;

         access_log /var/log/nginx/sample-domain.com-access.log;
         error_log  /var/log/nginx/sample-domain.com-error.log error;
         index index.html index.htm index.php;

         location / {
                      try_files $uri $uri/ /index.php$is_args$args;
         }

         location ~ \.php$ {
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass unix:/run/php/php8.4-fpm.sock;
            fastcgi_index index.php;
            include fastcgi.conf;
    }
}
```

PHP-FPM is working on a unix socket located in `unix:/run/php/php8.4-fpm.sock`. Configuration file `php.ini` is located in `fpm` subdirectory, like `/etc/php/8.4/fpm/php.ini`.

# 3. PHP on IIS as FastFGI module

## Install PHP on windows

```cmd
winget search php
winget install PHP.PHP.8.4 --location "c:\php\8.4"
```

## Configuring PHP with IIS

Like we can read in [PHP](https://www.php.net/manual/en/install.windows.iis.php) manual page.

> In IIS Manager (1), Install FastCGI module (2) and add a handler mapping for .php to the path to php-cgi.exe (not php.exe) (3)


## 1. Install IIS on windows

### Check if IIS is installed

```cmd
get-service w3svc
```
If not installed
> get-service : Cannot find any service name 'w3svc'

### Install

```cmd
Dism /Online /Enable-Feature /FeatureName:IIS-DefaultDocument /All

Dism /Online /Enable-Feature /FeatureName:IIS-ASPNET45 /All
```

### 2. Install FastCGI module

Under `Windows Features`
Internet Information Services \ World Wide Web Services \ Application Development Features \ CGI

### 3. Configure PHP with IIS

Register module with 
```
Request path: *.php
Module: FastCgiModule
Executable: c:\php\8.4\php-cgi.exe
Name: PHP
```


- [URL Rewrite](https://iis-umbraco.azurewebsites.net/downloads/microsoft/url-rewrite) 

# PHP Frameworks

Here are some PHP frameworks check out

[1. Symfony Framework - install & setup](Symfony%20Framework.md)