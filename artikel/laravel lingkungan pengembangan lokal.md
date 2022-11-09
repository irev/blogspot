# Laravel dengan lingkungan pengembangan lokal

Hal penting yang dilakukan untuk memulai pengerjaan projek dengan laravel, seorang programer harus memiliki beberapa aplikasi pendukung untuk memulai pekerjaan tersebut. Apa saja aplikasi yang dibutuhkan programer untuk memulai projek dengan laravel ?

## Persiapan Aplikasi

Web Server
----------

- Apache2

  Aplikasi server web yang dapat dijalankan di banyak sistem operasi (Unix,
  BSD, Linux, Microsoft Windows dan Novell Netware serta platform
  lainnya) yang berguna untuk melayani dan memfungsikan situs web.
  Protokol yang digunakan untuk melayani fasilitas web/www ini menggunakan
  HTTP/HTTPS.
- Nginx

  Aplikasi server web open-source yang berfungsi sebagai reverse proxy,
  penyeimbang beban HTTP, serta proxy email untuk IMAP, POP3, dan SMTP. Engix cara pengejaannya "enjin-eks".
- lighttpd

  Aplikasi server web yang dirancang dengan mengutamakan aspek cepat, aman, fleksibel, dan sesuai dengan standar. Ini dioptimalkan untuk lingkungan di mana kecepatan sangat penting. Ini karena ia mengkonsumsi lebih sedikit CPU dan RAM daripada server lain.

Database
--------

- Mysql

  Adalah sebuah database management system (manajemen basis data) menggunakan perintah dasar SQL ( *Structured Query Language* ) yang cukup terkenal. Database management system (DBMS) MySQL multi pengguna dan multi alur
- Mariadb

  MariaDB adalah sistem manajemen *database* yang merupakan pengembangan mandiri dari MySQL. Atau sering disebut versi lain dari MySQL.

Bahasa Pemprograman
-------------------

- PHP

  PHP adalah singkatan dari Hypertext Preprocessor, yaitu bahasa penulisan skrip yang umum dipakai dalam pembuatan dan pengembangan suatu web.

  Untuk kebutuhan Laravel minimal versi PHP yang diinstal adalah PHP versi 7.2.5 keatas.

## Package Manager

- Composer

  Aplikasi manajer paket untuk bahasa pemrograman PHP yang menyediakan format standar untuk mengelola dependensi PHP dan pustaka-pustaka yang diperlukan.

## Install Laravel

Jalankan perintah berikut pada terminal/command line

```
composer create-project laravel/laravel:^9.0 test-app.
```

Untuk langkah selanjutnya silahkan baca tutorial [Cara Install Laravel versi 9 Framework](https://meeduns.blogspot.com/2022/11/cara-install-laravel-9-di-linux-mint.html) atau [Cara Install Laravel 9 di Linux Mint 20.3 Una](https://meeduns.blogspot.com/2022/11/cara-install-laravel-9-di-linux-mint.html).

