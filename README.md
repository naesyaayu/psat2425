# Penilaian Sumatif Akhir Tahun
## Mapil DevOps XI TJKT 1 - Penilaian Praktek
### SMKN 1 Banyumas - TA. 2024 2025


#
# Cara mendeploy Aplikasi
```
sudo apt update -y

sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client

sudo rm -rf /var/www/html/{*,.*}

sudo git clone https://github.com/naesya/psat2425.git /var/www/html

sudo chmod -R 777 /var/www/html

echo DB_USER=admin > /var/www/html/.env
echo DB_PASS=P4ssw0rd  >> /var/www/html/.env
echo DB_NAME=psat2425  >> /var/www/html/.env
echo DB_HOST=dbnesa.cysbxsw7ilhe.us-east-1.rds.amazonaws.com>> /var/www/html/.env

atau bisa dibuat menjadi shell script, misal diberi nama otomatis.sh
```
# Membuat deploy dengan otomatis.sh
```
#!/bin/bash
echo '#!/bin/bash
sudo apt update -y
sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client
sudo rm -rf /var/www/html/{,.}
sudo git clone https://github.com/naesyaayu/psat2425 /var/www/html
sudo chmod -R 777 /var/www/html
echo DB_USER=admin > /var/www/html/.env
echo DB_PASS=P4ssw0rd  >> /var/www/html/.env
echo DB_NAME=psat2425  >> /var/www/html/.env
echo DB_HOST=dbnesa.cysbxsw7ilhe.us-east-1.rds.amazonaws.com >> /var/www/html/.env
sudo apt install -y openssl
sudo a2enmod ssl
sudo a2ensite default-ssl.conf
sudo systemctl reload apache2' > /home/ubuntu/otomatis.sh

Mengaplikasikan/menjalankan terdapat 2 cara
1. Dieksekusi langsung
2.Dibuat menjadi executable kemudian dieksekusi
```
chmod +x /home/ubuntu/otomatis.sh  

## 1. Buat File .env

File .env adalah file environment sistem mirip seperti file konfig.php
#
isi file .env sebagai berikut

```.env
DB_USER=....  (isi dengan user RDS)
DB_PASS=....  (isi dengan password RDS)
DB_NAME=....  (isi dengan nama database yang akan dibuat di RDS)
DB_HOST=....  (isi dengan Endpoint RDS)
```
## 2. Jalankan 
Jalankan dengan username dan password default berikut ini
#
### username = admin
### password = 123
#

Kemudian inputkanlah data sesuai dengan datamu

`
## Tambahan
## ✅ Langkah-langkah Membuat Security Group di AWS EC2
```
Masuk ke AWS Management Console
Kunjungi: https://console.aws.amazon.com/
Login dengan akun AWS Anda.
Cari dan buka layanan EC2.
Pilih “Security Groups”
Di bagian kiri menu, klik “Security Groups” di bawah “Network & Security”.
Klik “Create security group”
Isi nama, deskripsi, dan pilih VPC (Virtual Private Cloud) yang sesuai.
Tambahkan Rules
Pada bagian Inbound rules (lalu lintas masuk):
Misalnya untuk akses SSH (port 22):
Type: SSH
Protocol: TCP
Port Range: 22
Source: My IP (jika hanya dari IP kamu)
Untuk akses HTTP (port 80) atau HTTPS (port 443), tambahkan aturan sesuai kebutuhan.
Pada bagian Outbound rules (lalu lintas keluar), biasanya default-nya membolehkan semua.
Klik “Create security group”
Asosiasikan Security Group dengan Instance
Saat membuat EC2 instance, kamu bisa memilih Security Group ini.
Atau, untuk instance yang sudah ada:
Pilih instance → klik Actions → Networking → Change Security Groups.

```
## Cara mengisntall RDS/Databse
```
Masuk ke AWS Console
Buka https://console.aws.amazon.com/ dan login.
Buka Layanan RDS
Ketik "RDS" di kolom pencarian dan buka layanan RDS.
Klik “Create database”
Pilih Standard create.
Pilih Engine database
Contoh: MySQL, PostgreSQL, MariaDB, SQL Server, Oracle.
Atur detail database
Tentukan:
DB instance identifier (nama database)
Master username & password
Pilih jenis instance
Atur storage dan konektivitas
Storage: 20 GB (contoh)
Konektivitas: atur VPC, subnet, dan security group (izin akses)
Klik “Create database”
Tunggu beberapa menit sampai status DB menjadi “Available”.
Koneksi ke database



