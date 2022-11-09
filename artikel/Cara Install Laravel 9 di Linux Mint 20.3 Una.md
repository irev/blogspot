## Cara Install Laravel 9 di Linux Mint 20.3 Una


Laravel 9 baru saja [dirilis](https://laravel-news.com/laravel-9-released)
 dengan banyak penambahan fitur baru, di antaranya controller route
groups, default Ignition error page, Laravel Scout databas engine,
Symfony mailer integration, Flysystem 3.x, peningkatan Eloquent
accessors/mutators, dan masih banyak lagi.

Terhitung sejak
Laravel 9, pengembang Laravel akan merilis versi mayor setiap 12 bulan
yang sebelumnya setiap 6 bulan. Laravel 9 termasuk ke dalam versi LTS
(Long Term Support) yang akan mendapatkan dukungan bug fixes hingga 8
Februari 2024 dan dukungan security fixes hingga 8 Februari 2025.

## Server Requirements

Server requirements khususnya PHP yang harus dipenuhi untuk dapat menjalankan Laravel 9:

* PHP >= 8.0
* BCMath PHP Extension
* Ctype PHP Extension
* DOM PHP Extension
* Fileinfo PHP Extension
* JSON PHP Extension
* Mbstring PHP Extension
* OpenSSL PHP Extension
* PCRE PHP Extension
* PDO PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension

## Install PHP

Repository default Ubuntu 20.04 hanya menyediakan PHP v7.4. Oleh karena itu membutuhkan repository tambahan untuk PHP terbaru.

Memasang repository  **ppa:ondrej/php** .

```bash
sudo add-apt-repository ppa:ondrej/php
```

Install PHP 8.1 dan extensionnya.

```bash
sudo apt install php8.1 php8.1-cli php8.1-common php8.1-mbstring php8.1-gd php8.1-intl php8.1-xml php8.1-mysql php8.1-zip php8.1-xsl php8.1-curl
```

Memverifikasi instalasi PHP dengan menampilkan versi.

```
sa@ubuntu:~$ php -vPHP 8.1.2 (cli) (built: Jan 24 2022 10:42:33) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2, Copyright (c), by Zend Technologies
```


## Install Composer

Install Laravel akan menggunakan Composer untuk itu install Composer terlebih dahulu.

```bash
sudo apt install curl git unzip 
curl–sS https://getcomposer.org/installer | php 
sudo mv composer.phar /usr/local/bin/composer
```

Memverifikasi instalasi Composer.

```bash
user@mint:~$ php -v
PHP 8.1.12 (cli) (built: Oct 28 2022 17:39:37) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.12, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.12, Copyright (c), by Zend Technologies
```

## Install Laravel

Install Laravel 9.0 dengan menggunakan Composer dan tersimpan di dalam folder  **webapp** .

composer create-project laravel/laravel webapp 9.0

```bash
composer create-project laravel/laravel  myprojrcj 9.0
```

Menjalankan Laravel development server.

cd webapp
php artisan serve

```bash
cd webapp php artisan serve 
```

Hasil perintah di atas.

```bash
user@mint:~$ composer -V
Composer version 2.2.6 2022-02-04 17:00:38
```

Jika menggunakan VPS dan ingin mengaksesnya melalui Public IP tambahkan  **–host** .

```bash
php artisan serve --host 0.0.0.0
```

![Laravel berjalan di development server](https://musaamin.web.id/wp-content/uploads/2022/02/install-laravel9-ubuntu2004_laravel-development-server.jpg)
Laravel berjalan di development server
