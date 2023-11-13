# Cara Install Apache2 dan Wordpress di Ubuntu Server 22.04
Artikel ini akan membahas tentang cara menampilkan apache dan cara remote ke CMD, PuTTY dan Ubuntu Dekstop <br>
# Cara Install Apache2
## 1. Login ke ubuntu server
## 2. Update dan Upgrade package
    sudo apt update && sudo apt upgrade
## 3. Install Apache2
    sudo apt install apache2
## 4. Cek Aplikasi yang Sudah di Install
     sudo ufw app list
## 5. Untuk Melihat Status dari Apache2 Gunakan Perintah
    sudo systemctl status apache2
## 6. Menampilkan Apache2 pada Browser
cek ip address menggunakan perintah `ip a` , copy *ip a* pada browser dan nanti akan tampil seperti ini
![Apache](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/b9a9c673-a095-4fd2-81d3-a770540cdec8)
## 7. Membuat Web <br>
### 7.1 Pindah ke direktori /var/www/html untuk membuat web
    cd /var/www/html
### 7.2 Buat Direktori
    mkdir <nama direktori>
### 7.3 Pindah ke root
    sudo su
### 7.4 Pindah ke direktori yang sudah dibuat
    cd <nama direktori>
### 7.5 Edit direktori
    nano index.html
### 7.6 Contoh program
```sh
<html>
<head>
<title> website eyn </title>
</head>
<h1>
<body> Selamat Datang di Website Ini </body>
</h1>
<p>Nama : Feliana Yunita
<p>NIM : 09011282227039
<p>Kelas : SK5C
<p>Prodi : Sistem Komputer
</html>
```
### 7.7 Output 
`ip a/<nama direktori>`
![web](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/db657a74-fdd5-4d84-973f-0b606ef9d210)

## Cara Remote
### 1. CMD
    ssh<nama server>@ip a
![CMD](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/a99239f9-a75c-4bab-a6aa-7a8644d9a607)
### 2. PuTTY
1. Masukkan alamat ip pada PuTTY <br>
2. klik open <br>
3. connect once <br>
![PuTTY](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/3c003998-7aaf-45b0-8646-a40667e0ac76)
3. Ubuntu Dekstop
```sh
ssh<nama server>@ip a
```
![image](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/063b1a83-dc9f-44ff-a83c-c8b047524a19)

# Cara Install Wordpress
Pastikan sudah ada apache2 pada ubuntu server yang digunakan
## 1. Pindah ke root
    sudo su
## 2. Install MySql
### 2.1 Install MySQL
    apt install mariadb-server mariadb-client
### 2.2 Amankan basis data MariaDB dan larang login root jarak jauh
    mysql_secure_installation
## 3. Install PHP
### 3.1 Install
    apt install php php-mysql
### 3.2 Untuk mengonfirmasi bahwa PHP diinstal, buat file info.php di `/var/www/html/`
    nano /var/www/html/info.php
Tambahkan baris berikut
```sh
<?php
phpinfo();
?>
```
### 3.4 Buka browser `ip/info.php`
![image](https://github.com/feliana444/Apache2-dan-Wordpress-UbuntuServer/assets/145323449/bf1726cd-60b3-4138-a9b6-9ce82c430bcd)
### 3.5 Install Komponen PHP & Apache
    sudo apt install php libapache2-mod-php php-mysql
## 4. Membuat Data Base Wordpress
### 4.1 Masuk ke database MariaDB
    mysql -u root -p
### 4.2 Ketikkan perintah ini satu per satu
```sh
CREATE DATABASE wordpress_db;
```
```sh
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
```
```sh
GRANT ALL ON wordpress_db.* TO 'wp_user'@'localhost' IDENTIFIED BY 'password';
```
```sh
FLUSH PRIVILEGES;
```
```sh
Exit;
```
## 5. Install WordPress CMS
### 5.1 Install
```sh
cd /tmp && wget https://wordpress.org/latest.tar.gz
```
```sh
tar -xvf latest.tar.gz
```
### 5.2 Selanjutnya ikuti perintah ini
```sh
cp -R wordpress /var/www/html/
```
```sh
chown -R www-data:www-data /var/www/html/wordpress/
```
```sh
chmod -R 755 /var/www/html/wordpress/
```
```sh
$ mkdir /var/www/html/wordpress/wp-content/uploads
```
```sh
chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads/
```
### 5.4 Buka browser <br>
`ip/wordpress`
Isi formulir seperti saat membuat database WordPress di database MariaDB
![image](https://github.com/feliana444/Apache2-dan-Wordpress-UbuntuServer/assets/145323449/db000734-c0ce-42a5-a2ac-38c3630dd408)
klik *run the installation* <br>
Kemudian, isi detail tambahan yang diperlukan seperti judul situs, Nama Pengguna, dan 
Kata Sandi lalu klik install wordpress untuk login ke akun wordpress yang sudah 
kita buat
### 5.5 Jika sudah selesai akan muncul tampilan seperti ini
![image](https://github.com/feliana444/Apache2-dan-Wordpress-UbuntuServer/assets/145323449/52d0a77d-d23a-4418-a628-d28e24148041)
![image](https://github.com/feliana444/Apache2-dan-Wordpress-UbuntuServer/assets/145323449/60959b01-75bf-4fb0-a069-45aa67687da2)
## 6. Edit File Wordpress
Agar wordpress masi bisa dibuka ketika kita menggunakan alamat ip yang berbeda, ubah konfig file wordpress
```sh
cd /var/www/html/wordpress
```
```sh
nano wp-config.php
```
salin teks ini dibawah *db_collate*
```sh
$ip = exec('ip addr show enp0s3 | grep "inet\b" | awk \'{print $2}\' | cut -d/ -f1');
if (!empty($ip)) {
  define('WP_HOME', 'http://' . $ip . '/wordpress');
  define('WP_SITEURL', 'http://' . $ip . '/wordpress');
}
```
lalu ketikan perintah
```sh
php wp-config.php
```
