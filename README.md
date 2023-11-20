# Jarkom Modul 3 | IT29 | 2023
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
## Soal 0
> Melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.
Pada soal ini kita perlu mengkonfigurasi DNS untuk domain riegel.canyon.it29.com dan granz.channel.it29.com pada DNS Server (Heiter). Kami menggunakan bind9 sebagai DNS Server nya.
### Setup
#### Heiter
1. Install Depedencies
```bash
# install dependencies
apt-get update -y
apt-get install bind9 -y
```
2. Buat direktori baru
```bash
# create directory
mkdir /etc/bind/it29
```
3. Buat konfigurasi named.conf.local
```bash
# add named.conf.local
cat <<EOF > /etc/bind/named.conf.local
zone "riegel.canyon.it29.com" {
    type master;
    file "/etc/bind/it29/riegel.canyon.it29.com";
};

zone "granz.channel.it29.com" {
    type master;
    file "/etc/bind/it29/granz.channel.it29.com";
};
EOF
```
4. Buat konfigurasi named.conf.options
```
cat <<EOF > /etc/bind/named.conf.options
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        forwarders {
            192.168.122.1;
        };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        # dnssec-validation no;
        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035

        listen-on-v6 { any; };
};
EOF
```
5. Buat konfigurasi DNS Record
```bash
# add riegel.canyon.it29.com
echo '$TTL    604800
@       IN      SOA     riegel.canyon.it29.com. root.riegel.canyon.it29.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.it29.com.
@       IN      A       10.78.4.1
www     IN      CNAME   riegel.canyon.it29.com.' > /etc/bind/it29/riegel.canyon.it29.com

# add granz.channel.it29.com
echo '$TTL    604800
@       IN      SOA     granz.channel.it29.com. root.granz.channel.it29.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.it29.com.
@       IN      A       10.78.3.1
www     IN      CNAME   granz.channel.it29.com.' > /etc/bind/it29/granz.channel.it29.com
```
6. Restart bind9
```bash
# restart dns server
service bind9 restart
```

## Soal 1
> Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.
Pada soal ini kita melakukan setup topologi pada GNS3 sesuai dengan peta topologi yang ada pada soal.

## Soal 2, 3, 4, dan 5
> Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 
Pada soal ini kita perlu melakukan setup pada DHCP Server (Himmel) dan DHCP Relay (Aura).
> Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 
> Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut
> Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit 
### Setup
#### Himmel
1. Install Depedencies
```bash
# install dependencies
apt-get update -y
apt-get install isc-dhcp-server -y
service isc-dhcp-server start
```
2. Setup interfaces pada `/etc/default/isc-dhcp-server`.w
```bash
sed -i 's/INTERFACES=""/INTERFACES="eth0"/g' /etc/default/isc-dhcp-server
```
3. Setup konfigurasi DHCP pada `/etc/dhcp/dhcpd.conf`.
```
ddns-update-style none;
default-lease-time 600;
max-lease-time 7200;
authoritative;
log-facility local7;

subnet 10.78.1.0 netmask 255.255.255.0 {
    range 10.78.1.100 10.78.1.105;
    option routers 10.78.1.1;
    option domain-name-servers 10.78.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.78.3.0 netmask 255.255.255.0 {
    range 10.78.3.16 10.78.3.32;
    range 10.78.3.64 10.78.3.80;
    option routers 10.78.3.1;
    option domain-name-servers 10.78.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 10.78.4.0 netmask 255.255.255.0 {
    range 10.78.4.12 10.78.4.20;
    range 10.78.4.160 10.78.4.168;
    option routers 10.78.4.1;
    option domain-name-servers 10.78.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}

host Lawine {
    hardware ethernet 16:71:c9:3e:36:f5;
    fixed-address 10.78.3.1;
}

host Linie {
    hardware ethernet 6a:e2:30:85:a1:b2;
    fixed-address 10.78.3.2;
}

host Lugner {
    hardware ethernet 72:47:98:04:b0:c0;
    fixed-address 10.78.3.3;
}

host Frieren {
    hardware ethernet e2:9b:dd:48:d7:7a;
    fixed-address 10.78.4.1;
}

host Flamme {
    hardware ethernet 32:1b:dc:e1:e5:fb;
    fixed-address 10.78.4.2;
}

host Fern {
    hardware ethernet e6:f3:18:44:66:da;
    fixed-address 10.78.4.3;
}
EOF

# restart dhcp server
service isc-dhcp-server restart
```

## Soal 6
> Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website [berikut](https://drive.google.com/file/d/1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1/view?usp=sharing) dengan menggunakan php 7.3.

### Setup
#### Lawine, Linie, dan Lugner
1. Install depedencies
```bash
# install dependencies
apt-get update -y
apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y
apt-get install nginx -y
apt-get install wget unzip -y
```
2. Deploy attachment
```bash
# deploy attachment
wget -O '/tmp/dist.zip' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /tmp/dist.zip -d /tmp/
rm /tmp/dist.zip
mv /tmp/modul-3 /var/www/granz.channel.it29.com
```
3. Configure nginx
```bash
# configure nginx
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.it29.com
ln -s /etc/nginx/sites-available/granz.channel.it29.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name granz.channel.it29.com;

    root /var/www/granz.channel.it29.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.it29.com
```
4. Start services
```bash
# start services
service nginx start
service php7.3-fpm start
```

## Soal 7 
> Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second

### Setup
#### Eisen
1. Install depedencies
```bash
apt-get update -y
apt-get install nginx -y
```
2. Configure nginx
```bash
# configure nginx
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo 'upstream worker {
    server 10.78.3.1;
    server 10.78.3.2;
    server 10.78.3.3;
}

server {
    listen 80;
    server_name _;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }
}' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default
```
3. Start services
```bash
service nginx restart
```

## Soal 8
> Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
Nama Algoritma Load Balancer
, Report hasil testing pada Apache Benchmark
, Grafik request per second untuk masing masing algoritma. 
, Analisis 

### Setup
#### Client
```bash
ab -n 200 -c 10 http://www.granz.channel.it29.com/
```
### Result
1. Round Robin

![round_robin](https://github.com/Ridho626/Jarkom-Modul-3-IT29-2023/assets/54212814/b3f871bb-56a9-445d-8b95-b99ae9e7fb96)

2. Least Conn

![least_conn](https://github.com/Ridho626/Jarkom-Modul-3-IT29-2023/assets/54212814/bad045c4-de73-4fb9-bbff-fd486508a281)

3. IP Hash

![ip_hash](https://github.com/Ridho626/Jarkom-Modul-3-IT29-2023/assets/54212814/6b74c4fd-5b6e-432c-b542-9a169cd7cbac)

4. Generic Hash

![generic_hash](https://github.com/Ridho626/Jarkom-Modul-3-IT29-2023/assets/54212814/14b6b5ac-deaf-4068-b4cf-be0abd8e1837)

### Grafik

![image](https://github.com/Ridho626/Jarkom-Modul-3-IT29-2023/assets/54212814/3bcc77c6-3735-4a9e-b00a-7309fbc65f56)

## Soal 9
> Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire

### Setup
#### Client
```bash
ab -n 100 -c 10 http://www.granz.channel.it29.com/ 
```

## Soal 10
> Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

### Setup
#### Eisen
1. Generate htpasswd
```bash
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
2. Ubah konfigurasi nginx
```bash
echo 'upstream worker {
    server 10.78.3.1;
    server 10.78.3.2;
    server 10.78.3.3;
}

server {
    listen 80;
    server_name _;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
}' > /etc/nginx/sites-available/lb_php
```
3. Restart service
```bash
service nginx restart
```

## Soal 11
> Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. `hint: (proxy_pass)`

### Setup
#### Eisen
1. Ubah konfigurasi nginx
```bash
echo 'upstream worker {
    server 10.78.3.1;
    server 10.78.3.2;
    server 10.78.3.3;
}

server {
    listen 80;
    server_name _;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;


    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location / {
        proxy_pass http://worker;
    }

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
}' > /etc/nginx/sites-available/lb_php
```
2. Restart service
```bash
service nginx restart
```

## Soal 12 
> Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168 `hint: (fixed in dulu clinetnya)`

### Setup
#### Eisen
1. Ubah konfigurasi nginx
```bash
echo 'upstream worker {
    server 10.78.3.1;
    server 10.78.3.2;
    server 10.78.3.3;
}

server {
    listen 80;
    server_name _;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location / {
	allow 10.78.3.69;
	allow 10.78.3.70;
	allow 10.78.4.167;
	allow 10.78.4.168;
	deny all;
        proxy_pass http://worker;
    }

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
}' > /etc/nginx/sites-available/lb_php
```

## Soal 13
> Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern

### Script
#### Denken
1. Setup `/etc/mysql/my.cnf` to enable all configuration.
```bash
echo '# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```
2. Ubah bind_address di `/etc/mysql/mariadb.conf.d/50-server.cnf`.
```bash
sed -i 's/127.0.0.1/0.0.0.0/g' /etc/mysql/mariadb.conf.d/50-server.cnf
```
3. Restart service
```
service mysql restart
```
4. Buat user dan database baru.
```sql
CREATE USER 'admin'@'%' IDENTIFIED BY 'admin1337';
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin1337';
CREATE DATABASE db_it29;
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'admin1337'@'localhost';
FLUSH PRIVILEGES;
```


## Soal 14
> Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide [berikut](https://github.com/martuafernando/laravel-praktikum-jarkom). Jangan lupa melakukan instalasi PHP8.0 dan Composer
### Script
#### Laravel Worker
1. Install depedencies
```bash
apt-get update
apt-get install nginx git mariadb-client lsb-release ca-certificates apt-transport-https software-properties-common gnupg2 -y

curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli   php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y

wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer
```
2. Deploy attachment
```bash
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom && composer update
```
3. Konfigurasi .env
```bash
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.78.2.2
DB_PORT=3306
DB_DATABASE=db_it29
DB_USERNAME=admin
DB_PASSWORD=admin1337

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
```
4. Install resource
```bash
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```
5. Konfigurasi nginx
```
echo 'server {
    listen 80;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/
```
6. Start services
```bash
service nginx restart
service php8.0-fpm start
```

## Soal 15 
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `POST /auth/register`

### Setup
#### Client
```bash
echo '{"username": "kiseki","test": "kiseki1337"}' |tee register.json
ab -n 100 -c 10 -p register.json -T application/json http://10.78.4.1/api/auth/register
```

## Soal 16
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `POST /auth/login`
```bash
echo '{"username": "kiseki","test": "kiseki1337"}' |tee login.json
ab -n 100 -c 10 -p login.json -T application/json http://10.78.4.1/api/auth/login
```

## Soal 17
> Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire untuk `GET /me `
```bash
curl -X POST -d @login.json -H "Content-Type: application/json" http://10.78.4.1:8001/api/auth/login |tee res.txt
ab -n 100 -c 10 -H "Authorization: Bearer $(cat login_output.txt | jq -r '.token')" http://10.78.4.1:8001/api/me
```

## Soal 18 
> Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern
### Setup
#### Eisen
1. Buat konfigurasi nginx baru
```bash
echo 'upstream worker {
    server 10.78.4.3:8001;
    server 10.78.4.2:8002;
    server 10.78.4.1:8003;
}

server {
    listen 82;
    server_name _;

    location / {
        proxy_pass http://worker;
    }
} 
'> /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker
```
2. Restart service
```bash
service nginx start
```

## Soal 19 
> Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire
### Setup
#### Laravel Worker
1. Ubah konfigurasi php-fpm
```bash
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3' > /etc/php/8.0/fpm/pool.d/www.conf
```
2. Restart Service
```
service php8.0-fpm restart
```
3. Testing
```
ab -n 100 -c 10 -p login.json -T application/json http://10.78.4.1/api/auth/login
```
Selanjutnya, dilakukan langkah-langkah yang sama dengan menggunakan konfigurasi lain sebagai berikut:
Config 2
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 10
pm.start_servers = 4
pm.min_spare_servers = 2
pm.max_spare_servers = 6' > /etc/php/8.0/fpm/pool.d/www.conf
```
Config 3
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 15
pm.start_servers = 6
pm.min_spare_servers = 3
pm.max_spare_servers = 9' > /etc/php/8.0/fpm/pool.d/www.conf
```

## Soal 20 
> Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second

### Setup
#### Eisen
1. Edit konfigurasi load balancer.
```bash
echo 'upstream worker {
    least_conn;
    server 10.78.4.3:8001;
    server 10.78.4.2:8002;
    server 10.78.4.1:8003;
}

server {
    listen 82;
    server_name _;

    location / {
        proxy_pass http://worker;
    }
} 
'> /etc/nginx/sites-available/laravel-worker
```
2. Restart service
```
service nginx restart
```
3. Testing
```
ab -n 100 -c 10 -p login.json -T application/json http://10.78.4.1/api/auth/login
```
