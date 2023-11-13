# Cara Install Apache2 dan Wordpress di Ubuntu Server 22.04
Artikel ini akan membahas tentang cara menampilkan apache dan cara remote ke CMD, PuTTY dan Ubuntu Dekstop <br>
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
cek ip address menggunakan perintah `ip a`
copy *ip a* pada browser dan nanti akan tampil seperti ini
![Apache](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/b9a9c673-a095-4fd2-81d3-a770540cdec8)
## 7. Membuat Web
### 7.1 Pindah ke direktori /var/www/html untuk membuat web
    cd /var/www/html
### 7.2 Buat file
    mkdir <nama direktori>
### 7.3 Pindah ke root
    sudo su
### 7.4 Pindah ke direktori yang sudah dibuat
    cd <nama direktori>
### 7.5 Edit direktori
    nano index.html
### 7.8 Contoh program
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
### 7.9 Output
`ip a/<nama direktori>`
![web](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/db657a74-fdd5-4d84-973f-0b606ef9d210)

#3 Cara Remote ke CMD
```sh
ssh<nama server>@ip a
```
![CMD](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/a99239f9-a75c-4bab-a6aa-7a8644d9a607)
## Cara Remote ke PuTTY
1. Masukkan alamat ip pada PuTTY <br>
2. klik open <br>
3. connect once <br>
![PuTTY](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/3c003998-7aaf-45b0-8646-a40667e0ac76)
## Cara Remote ke Ubuntu Dekstop
```sh
ssh<nama server>@ip a
```
![image](https://github.com/feliana444/Apache2-UbuntuServer/assets/145323449/063b1a83-dc9f-44ff-a83c-c8b047524a19)
