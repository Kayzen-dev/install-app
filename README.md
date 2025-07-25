
---

````markdown
# 🚀 install-app

Panduan lengkap instalasi sistem untuk menjalankan aplikasi Laravel di Ubuntu (WSL / Linux).

---

## 🧩 FASE 1: INSTALASI SISTEM

### ✅ Komponen yang Akan Di-install:

1. Ubuntu
2. PHP
3. Apache
4. MySQL
5. NVM
6. Node.js
7. NPM
8. Composer

---

## 🖥️ 1. Instalasi Ubuntu & Persiapan

### 🔹 Langkah Awal

1. Buka **Microsoft Store** → cari `Ubuntu` → klik **Install**
2. Setelah instalasi, buka Ubuntu dan buat user

### 🔹 Update & Install Tools

```bash
sudo apt update && sudo apt upgrade
sudo apt install build-essential curl git
````

### 🔹 Konfigurasi Akses Folder Apache

```bash
bash
sudo chmod o+x /home/crown  // Ganti sesuai nana usersname ubuntunya

sudo systemctl restart apache2
```
* agar Apache bisa *masuk* ke direktori itu.

### 🔹 Wajib: Install Modul PHP Apache

```bash
sudo apt update
sudo apt install libapache2-mod-php8.3
sudo a2enmod php8.3
```

---

## 📄 2. Cek PHP via info.php

1. Buat file `info.php` di `/var/www/html`:

```php
<?php phpInfo(); ?>
```

2. Buka di browser: [http://localhost/info.php](http://localhost/info.php)

---

## 📂 3. Setup index.php untuk Menjalankan Laravel setelah melakukan fase 2

1. Buat file `index.php` di `/var/www/html` dengan isi berikut:

```php
<?php
// Path ke folder Laravel kamu
$projectPath = '/home/crown/app-hotel'; // Ganti sesuai lokasi project Laravel

// Pindah ke direktori project Laravel
chdir($projectPath);

// Jalankan server Laravel jika belum berjalan
$command = 'php artisan serve --host 127.0.0.1';
exec("lsof -i :8000", $output);

if (empty($output)) {
    // Jalankan server Laravel di background
    pclose(popen($command . " > /dev/null 2>&1 &", "r"));
}

// Redirect ke aplikasi Laravel
header("Location: http://127.0.0.1:8000");
exit;
?>
```
*atau clone repo ini: https://github.com/Kayzen-dev/index.git

### 🔧 Perintah Tambahan:

```bash
# Pindahkan file index.php jika perlu
sudo mv index/index.php /var/www/html

# Hapus file default Apache
sudo rm /var/www/html/index.html

# Hapus folder jika salah
sudo rm -r /var/www/html/index
```

---

## 🧪 4. Instalasi PHP

```bash
sudo apt install unzip
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install -y php8.3 php8.3-cli php8.3-fpm php8.3-gd php8.3-mysql php8.3-xml php8.3-mbstring php8.3-zip php8.3-curl php8.3-bcmath php8.3-intl php8.3-json libapache2-mod-php8.3



sudo apt-get install php php-gd php-cli php-fpm php-mysql php-xml php-mbstring php-zip php-curl php-bcmath php-intl php-json //ini auto versi terbaru
```
5. Verifikasi Versi PHP
```bash
php -v
```
* Untuk memastikan versi CLI juga sudah ke PHP 8.3:

```bash
sudo update-alternatives --set php /usr/bin/php8.3
```
---

## 🌐 5. Instalasi Apache

```bash
sudo apt install apache2
sudo systemctl status apache2
sudo tail -f /var/log/apache2/error.log  # Untuk melihat error log jika ada
```

## 🌐 jika Instalasi menggunkaan nginx
* Konfigurasi Nginx + PHP-FPM
* Nginx tidak menggunakan module PHP langsung, tapi lewat php8.3-fpm.

* Contoh konfigurasi blok server di Nginx (/etc/nginx/sites-available/namasite):
```bash
server {
    listen 80;
    server_name namadomain.com;
    root /var/www/html;

    index index.php index.html index.htm;

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.3-fpm.sock;
    }

    location / {
        try_files $uri $uri/ =404;
    }
}
```
*Setelah itu:

```bash
sudo nginx -t && sudo systemctl reload nginx

```
---

## 🗄️ 6. Instalasi MySQL

```bash
sudo apt install mysql-server
sudo mysql -u root -p
```

Setelah masuk ke MySQL CLI, jalankan perintah ini:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'crown';
```

---

## 🧰 7. Instalasi NVM & Node.js

### 🔹 Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

> Tutup dan buka kembali terminal setelah instalasi selesai.

### 🔹 Install Node.js via NVM

```bash
nvm install node
```

### 🔹 Cek Versi Node & NPM

```bash
node -v
npm -v
```

---

## 🎼 8. Instalasi Composer

```bash
sudo apt install composer
sudo apt update
```

---

## 🎉 Selesai!

Server Laravel kini bisa dijalankan melalui `index.php` secara otomatis. Kunjungi [http://localhost](http://localhost) untuk membuka aplikasi kamu.

> Jangan lupa untuk selalu memeriksa kembali konfigurasi setiap kali melakukan perubahan sistem.

---

### 🧾 Catatan Tambahan

* Pastikan semua service (MySQL, Apache) aktif.
* Gunakan `php artisan migrate` atau `composer install` saat meng-clone project Laravel baru.
* Jika terjadi error saat menjalankan Laravel, cek log dengan `tail -f storage/logs/laravel.log`.

---

### 🧾 Fase Ke 2

* FASE 2, INSTALASI APP :
* CLONE GITHUB : `https://github.com/KYZ1-DEV/app-hotel.git`
* `COMPOSER INSTALL`
*  `NPM INSTALL`
*  `NPM RUN BUILD`
*  `PHP ARTISAN STORAGE:LINK`
*  `CP .ENV.EXAMPLE .ENV`
*  `PHP ARTISAN KEY:GENERATE`
*  `PHP ARTISAN MIGRATE --SEED`
*  `PHP ARTISAN SER`
*  `TESTING`


---

Selanjutnya setelah semua fase 😁😁

```
Buat file crown.bat dan nanti di convert ke .exe
---
@echo off
start wsl
timeout /t 5
start "" "http://localhost"
timeout /t 3
powershell -command "$wshell = New-Object -ComObject wscript.shell; $wshell.SendKeys('{F11}')"
```
