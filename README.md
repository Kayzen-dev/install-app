# install-app

FASE 1, INSTALASI SISTEM :
1.INSTALL UBUNTU 
2.INSTALL PHP
3.INSTALL APACHE
4.INSTALL MYSQL
5.INSTALL NVM
6.INSTALL NODE.JS
7.INSTALL NPM
8.INSTALL COMPOSER


1.CARA INSTALL UBUNTU DAN PERSIAPAN :
* BUKA MICROSOFT STORE LALU CARI UBUNTU DAN INSTALL
1.buat user
2.sudo apt update && sudo apt upgrade
3.sudo apt install build-essential curl git

* JIKA APLIKASI SUDAH DAN JALAN DAN AMAN:
1. sudo chmod -R 755 /var/www/html , untuk mengizinkan file,
2. sudo chown -R www-data:www-data /var/www/html , untuk mengizinkan apache akses file
3. sudo systemctl restart apache2, resrtart apache


* INI WAJIB DIJALANKAN
1. sudo apt update
2. sudo apt install libapache2-mod-php8.3
3. sudo a2enmod php8.3

LALU SETELAH JALAN DAN AMAN APPNYA, BUAT FILE info.php di /var/www/html
ISI FILE info.php :
<?php phpInfo(); ?>
JIKA SUDAH LALU CEK DI http://localhost/info.php, jika muncul maka selanjutnya buat file index.php di /var/www/html
ISI FILE index.php :
<?php


// Perintah pindahkan file index.php
 // sudo mv index/index.php /var/www/html 

// Perintah Hapus file defalurt = sudo rm index.html
// Perintah Hapus Folder jika salah = sudo rm -r index

// Tentukan project yang akan dijalankan
$projectPath = '/home/crown/app-hotel'; // Ganti dengan path proyek Laravel kamu

// Pindah ke direktori proyek Laravel
chdir($projectPath);
http://127.0.0.1:8000/
$command = 'php artisan ser --host 127.0.0.1';

// Cek apakah server sudah berjalan pada port 8000
exec("lsof -i :8000", $output);

if (empty($output)) {
    // Jika server belum berjalan, jalankan server Laravel di latar belakang
    pclose(popen($command . " > /dev/null 2>&1 &", "r"));
}

// Redirect ke localhost:8000
header("Location: http://127.0.0.1:8000");
exit;




  


2.CARA INSTALL PHP :
1.sudo apt install unzip
2.sudo add-apt-repository ppa:ondrej/php
3.sudo apt update
4.sudo apt-get install php php-gd php-xml php-mbstring php-curl php-zip php-intl php-bcmath php-json php-mysql
5.sudo apt-get install php php-gd php-cli php-fpm php-mysql php-xml php-mbstring php-zip php-curl php-bcmath 
php-intl php-json




3.CARA INSTALL APACHE :
1. *Instal Apache:*
   1. sudo apt install apache2
2. *Periksa Status Apache:*
    2. sudo systemctl status apache2
3. sudo tail -f /var/log/apache2/error.log (untuk cek error)





4.CARA INSTALL MYSQL:
1.sudo apt install mysql-server
2.sudo MySQL -u root -p
3.ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'crown';




5.CARA INSTALL NVM
1. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   - Tutup dan buka kembali terminal, lalu instal Node.js:
2.   nvm install node




6.CARA INSTALL NODE.JS:
1. node -v



7.CARA INSTALL NPM:
2. npm -v


8.CARA INSTALL COMPOSER:
1.sudo apt install composer
2.sudo apt update










