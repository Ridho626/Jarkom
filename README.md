# Jarkom Modul 2 | IT29 | 2023
- M. Azril Fathoni (5027211002)
- Ridho Husni Indrawan (5027211043)

### Topologi
![image](https://github.com/Ridho626/Jarkom/blob/58a6ddbe6f79b824efd75cd149a73716119b0817/Image/Screenshot%202023-11-19%20140813.png)

### Config
#### Aura (DHCP)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.78.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.78.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.78.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.78.4.0
	netmask 255.255.255.0
```
###  Himmel DHCP 
```
auto eth0
iface eth0 inet static
	address 10.78.1.2
	netmask 255.255.255.0
	gateway 10.78.1.0
```
### Heiter DNS 
```
auto eth0
iface eth0 inet static
	address 10.78.1.3
	netmask 255.255.255.0
	gateway 10.78.1.0
```
### Denken Database 
```
auto eth0
iface eth0 inet static
	address 10.78.2.2
	netmask 255.255.255.0
	gateway 10.78.2.0
```
### Eisen Load 
```
auto eth0
iface eth0 inet static
	address 10.78.2.3
	netmask 255.255.255.0
	gateway 10.78.2.0
```
### Frieren Laravel 
```
auto eth0
iface eth0 inet dhcp
hwaddress ether e2:9b:dd:48:d7:7a
```
### Flamme Laravel
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 32:1b:dc:e1:e5:fb
```
### Fern Laravel
```
auto eth0
iface eth0 inet dhcp
hwaddress ether e6:f3:18:44:66:da
```
### Lawine PHP
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 16:71:c9:3e:36:f5
```
### Linie PHP
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 6a:e2:30:85:a1:b2
```
### Lugner PHP
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 72:47:98:04:b0:c0
```
### Revolte, Richter, Sein, Stark (Client)
```
auto eth0
iface eth0 inet dhcp
```

## Soal 1
> Lakukan konfigurasi sesuai dengan topologi yang ada. Kemudian, lakuakn register domain berupa riegel.canyon.com untuk Laravel dan granz.channel.com untuk worker PHP mengarah pada worker yang memiliki IP [prefix IP].x.1

## Soal 2
> Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 

## Soal 3
> Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 

## Soal 4
> Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut 

## Soal 5
> Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit 

## Soal 6
> Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

## Soal 7 
> Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second

## Soal 8
> Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
Nama Algoritma Load Balancer
, Report hasil testing pada Apache Benchmark
, Grafik request per second untuk masing masing algoritma. 
, Analisis 

## Soal 9
> Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire

## Soal 10
> Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/ 

## Soal 11
> Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. `hint: (proxy_pass)`

## Soal 12 
> Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168 `hint: (fixed in dulu clinetnya)`

## Soal 13
> Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern

## Soal 14
> Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

## Soal 15 
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `POST /auth/register`

## Soal 16
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `POST /auth/login`

## Soal 17
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `GET /me `

## Soal 18 
> Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern

## Soal 19 
> Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire

## Soal 20 
> Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second
