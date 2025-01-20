# Install & setup the Symfony Framework

## Curl & PHP Curl
```sh
sudo apt-get install php8.4-cli unzip
sudo apt-get install curl
sudo apt-get install php8.4 php8.4-curl
```

## Install composer Global

Download latest `composer.phar`.

[https://getcomposer.org/download/]([https://getcomposer.org/download/]())

```sh
wget https://getcomposer.org/download/latest-stable/composer.phar
sudo mv composer.phar /usr/local/bin/composer
chmod 755 /usr/local/bin/composer
```
cd \
## Update composer
```sh
composer self-update
```

## Install Symfony

Install Symfony CLI Debian/Ubuntu - APT based Linux

[https://symfony.com/download]([https://](https://symfony.com/download))

```
curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
sudo apt install symfony-cli
```

```
symfony check:requirements
```

Install recommended php extensions 

```
sudo apt-get install php8.4-intl
# or others
```

```
In PackageDiscoveryTrait.php line 376:

  Could not find package webapp.

  Did you mean one of these?
      tg/tgwebvalid
      peej/tonic
      symfony/webapp-pack
      symfony/webapp-meta
      erag/laravel-pwa
```
Run
```
composer require webapp
```
And select `symfony/webapp-pack`

```
symfony new sample1 --version="7.2.x" --webapp
```

## The Symfony MakerBundle
```
composer require --dev symfony/maker-bundle
```


## Start local server
```
cd my-project
symfony server:start
```