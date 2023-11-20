# Jarkom-Modul-3-A15-2023

### Kelompok A15

| **No** | **Nama**                   | **NRP**    |
| ------ | -------------------------- | ---------- |
| 1      | Frederick Hidayat          | 5025211152 |
| 2      | Reyner Fernaldi            | 5025201094 |


# PEMBAHASAN

## 1. Topologi dan Konfigurasi
![Alt text](img/topologi.png?raw=true "1a")

-   Aura
    ```

    auto eth0
    iface eth0 inet dhcp

    auto eth1
    iface eth1 inet static
        address 192.176.1.1
        netmask 255.255.255.0

    auto eth2
    iface eth2 inet static
        address 192.176.2.1
        netmask 255.255.255.0

    auto eth3
    iface eth3 inet static
        address 192.176.3.1
        netmask 255.255.255.0

    auto eth4
    iface eth4 inet static
        address 192.176.4.1
        netmask 255.255.255.0
    ```

-   Himmel
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.1.2
    netmask 255.255.255.0
    gateway 192.176.1.1
    ```
-   Heiter
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.1.3
    netmask 255.255.255.0
    gateway 192.176.1.1
    ```

-   Denken
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.2.2
    netmask 255.255.255.0
    gateway 192.176.2.1
    ```

-   Eisen
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.2.3
    netmask 255.255.255.0
    gateway 192.176.2.1
    ```

-   Revolte
    ```
    auto eth0
    iface eth0 inet dhcp
    ```

-   Richter
    ```
    auto eth0
    iface eth0 inet dhcp
    ```

-   Lawine
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.3.4
    netmask 255.255.255.0
    gateway 192.176.3.1
    ```

-   Linie
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.3.5
    netmask 255.255.255.0
    gateway 192.176.3.1
    ```

-   Lugner
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.3.6
    netmask 255.255.255.0
    gateway 192.176.3.1
    ```

-   Sein
    ```
    auto eth0
    iface eth0 inet dhcp
    ```

-   Stark
    ```
    auto eth0
    iface eth0 inet dhcp
    ```

-   Frieren
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.4.4
    netmask 255.255.255.0
    gateway 192.176.4.1
    ```

-   Flamme
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.4.5
    netmask 255.255.255.0
    gateway 192.176.4.1
    ```

-   Fern
    ```
    auto eth0
    iface eth0 inet static
    address 192.176.4.6
    netmask 255.255.255.0
    gateway 192.176.4.1
    ```

-   Melakukan konfigurasi pada DNS Server
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf

    apt-get update
    apt install bind9 -y
    echo 'zone "canyon.a15.com" {
            type master;
            file "/etc/bind/jarkom/canyon.a15.com";
    };

    zone "channel.a15.com" {
            type master;
            file "/etc/bind/jarkom/channel.a15.com";
    };
    ' > /etc/bind/named.conf.local

    mkdir -p /etc/bind/jarkom

    echo ';
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     canyon.a15.com. root.canyon.a15.com. (
                            2022100601      ; Serial
                            604800         ; Refresh
                            86400         ; Retry
                            2419200         ; Expire
                            604800 )       ; Negative Cache TTL
    ;modu
    @       IN      NS      canyon.a15.com.
    @       IN      A       192.176.1.3 
    riegel  IN      A       192.176.4.1
    @       IN      AAAA    ::1
    ' > /etc/bind/jarkom/canyon.a15.com

    echo ';
    ; BIND data file for local loopback interface
    ;
    $TTL    604800
    @       IN      SOA     channel.a15.com. root.channel.a15.com. (
                            2022100601      ; Serial
                            604800         ; Refresh
                            86400         ; Retry
                            2419200         ; Expire
                            604800 )       ; Negative Cache TTL
    ;modu
    @       IN      NS      channel.a15.com.
    @       IN      A       192.176.1.3 
    granz  IN      A       192.176.3.1
    @       IN      AAAA    ::1
    ' > /etc/bind/jarkom/channel.a15.com

    echo'options {
            directory "/var/cache/bind";

            forwarders {
                    192.168.122.1;
            };

        // dnssec-validation auto;        allow-query{any;};
            auth-nxdomain no;
            listen-on-v6 { any; };
    };' > /etc/bind/named.conf.options

    service bind9 restart
    ```
## 2. Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80

Melakukan configurasi pada DHCP Server (Himmel)
```
echo 'subnet 192.176.1.0 netmask 255.255.255.0 {
}

subnet 192.176.2.0 netmask 255.255.255.0 {
}

subnet 192.176.3.0 netmask 255.255.255.0 {
    range 192.176.3.16 192.176.3.32;
    range 192.176.3.64 192.176.3.80;
    option routers 192.176.3.1;
    option broadcast-address 192.176.3.255;
    option domain-name-servers 192.176.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}
```

## 3. Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168

```
echo 'subnet 192.176.1.0 netmask 255.255.255.0 {
}

subnet 192.176.2.0 netmask 255.255.255.0 {
}

subnet 192.176.3.0 netmask 255.255.255.0 {
    range 192.176.3.16 192.176.3.32;
    range 192.176.3.64 192.176.3.80;
    option routers 192.176.3.1;
}

subnet 192.176.4.0 netmask 255.255.255.0 {
    range 192.176.4.12 192.176.4.32;
    range 192.176.4.160 192.176.4.168;
    option routers 192.176.4.1;
}
```

## 4. Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut
```
subnet 192.176.3.0 netmask 255.255.255.0 {
    range 192.176.3.16 192.176.3.32;
    range 192.176.3.64 192.176.3.80;
    option routers 192.176.3.1;
    option broadcast-address 192.176.3.255;
    option domain-name-servers 192.176.1.3;
}

subnet 192.176.4.0 netmask 255.255.255.0 {
    range 192.176.4.12 192.176.4.32;
    range 192.176.4.160 192.176.4.168;
    option routers 192.176.4.1;
    option broadcast-address 192.176.4.255;
    option domain-name-servers 192.176.1.3;
}
```

Result
</br><img src="img/4.png?raw=true" alt="Alt text" title="1a" width="400">


## 5. Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit

```
subnet 192.176.3.0 netmask 255.255.255.0 {
    range 192.176.3.16 192.176.3.32;
    range 192.176.3.64 192.176.3.80;
    option routers 192.176.3.1;
    option broadcast-address 192.176.3.255;
    option domain-name-servers 192.176.1.3;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.176.4.0 netmask 255.255.255.0 {
    range 192.176.4.12 192.176.4.32;
    range 192.176.4.160 192.176.4.168;
    option routers 192.176.4.1;
    option broadcast-address 192.176.4.255;
    option domain-name-servers 192.176.1.3;
    default-lease-time 720;
    max-lease-time 5760;
}
```

</br><img src="img/5a.png?raw=true" alt="Alt text" title="1a" width="400">
</br><img src="img/5b.png?raw=true" alt="Alt text" title="1a" width="400">



## 6. Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

Setup seluruh worker PHP

```
wget -O '/var/www/granz.channel.a15.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.a15.com -d /var/www/
rm /var/www/granz.channel.a15.com
mv /var/www/modul-3 /var/www/granz.channel.a15.com
```

konfigurasi nginx
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.a15.com
ln -s /etc/nginx/sites-available/granz.channel.a15.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.a15.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;  # Sesuaikan versi PHP dan socket
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.a15.com

service nginx restart
```
-   Result
    ```
    lynx localhost
    ```
    </br><img src="img/6.png?raw=true" alt="Alt text" title="1a" width="400">

## 7.Kepala suku dari Bredt Region memberikan resource server sebagai berikut: Lawine, 4GB, 2vCPU, dan 80 GB SSD. Linie, 2GB, 2vCPU, dan 50 GB SSD. Lugner 1GB, 1vCPU, dan 25 GB SSD. aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

```
echo ' upstream worker {
    server 192.176.3.4;
    server 192.176.3.5;
    server 192.176.3.6;
}

server {
    listen 80;
    server_name granz.channel.a15.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lbphp
```

-   Result
    ```
    ab -n 1000 -c 100 http://granz.channel.a15.com/ 
    ```
    </br><img src="img/7.png?raw=true" alt="Alt text" title="1a" width="400">

## 8. Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:

### 8.a. Nama Algoritma Load Balancer
-   Round Robin
    </br>Request per second : 399.51 [#/sec] (mean)
    </br><img src="img/8a1.png?raw=true" alt="Alt text" title="1a" width="400">

-   Least Connection
    </br>Request per second : 426.16 [#/sec] (mean)
    </br><img src="img/8a2.png?raw=true" alt="Alt text" title="1a" width="400">

-   IP Hash
    </br>Request per second : 419.45 [#/sec] (mean)
    </br><img src="img/8a3.png?raw=true" alt="Alt text" title="1a" width="400">
    
-   Generic Hash
    </br>Request per second : 364.71 [#/sec] (mean)
    </br><img src="img/8a4.png?raw=true" alt="Alt text" title="1a" width="400">

### 8.b. Grafik
</br><img src="img/8b.png?raw=true" alt="Alt text" title="1a" width="600">

### 8.c. Analisis
Least connection dapat melakukan handling paling baik namun hal tersebut datang dengan
konsekuensi CPU, memori yang diperlukan jadi lebih banyak sehingga jika kita ingin
mendapatkan hasil yang lebih hemat CPU dan memori, Generic Hash dan Run Robin dapat
menjadi pilihan. Banyak faktor error yang dapat mempengaruhi hasil di atas yang mana dalam
kasus praktikan, faktor error yang paling memungkinkan adalah keterlambatan jaringan internet
dan juga hardware issue. Secara teori, Least Connection memakan banyak memori sehingga memberikan RPS yang tinggi
diantara keempat algoritma, sedangkan Run Robbin dengan kesederhanaannya memberikan
kemudahan dalam setting sehingga sebagai gantinya RPS yang dihasilkan dari algoritma terkait,
tidak setinggi Least maupun algoritma lain.

## 9. Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

-   1 Worker
    </br>Request per second : 471.83 [#/sec](mean)
    </br><img src="img/9a.png?raw=true" alt="Alt text" title="1a" width="400">

-   2 Worker
    </br>Request per second : 440.13 [#/sec](mean)
    </br><img src="img/9b.png?raw=true" alt="Alt text" title="1a" width="400">

-   3 Worker
    </br>Request per second : 397.84 [#/sec](mean)
    </br><img src="img/9c.png?raw=true" alt="Alt text" title="1a" width="400">

-   Grafik
    </br><img src="img/9d.png?raw=true" alt="Alt text" title="1a" width="600">

-   Analisis
    </br>Semakin banyak worker yang dipakai akan berbanding terbalik dengan tingkat RPS ketika test benchmark dilakukan, dengan kata lain semakin banyak worker maka RPS tiap workernya dapat turun karena beban yang dibagi.

## 10. Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

-   Jalankan script berikut
    ```
    mkdir /etc/nginx/rahasisakita
    htpasswd -c /etc/nginx/rahasisakita/.htpasswd netics
    ```
-   Masukkan ajka15 sebagai password
-   Melakukan konfigurasi
    ```
    echo ' upstream worker {
    server 192.176.3.4;
    server 192.176.3.5;
    server 192.176.3.6;
    }
    server {
        listen 80;
        server_name granz.channel.a15.com;

        location / {
            proxy_pass http://worker;
        auth_basic "Authorized Content";
        auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;
        }
        
        location ~ /\.ht {
                deny all;
            }
    } ' > /etc/nginx/sites-available/lbphp
    ```
-   Testing 
    ```
    ab -A netics:ajka15 http://granz.channel.a15.com/
    ```
    </br><img src="img/10.png?raw=true" alt="Alt text" title="1a" width="400">

    ```
    lynx -auth=netics:ajka15 http://granz.channel.a15.com/
    ```
    </br><img src="img/10b.png?raw=true" alt="Alt text" title="1a" width="400">

## 11. Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. hint: (proxy_pass)

-   Melakukan konfigurasi
    ```
    echo ' upstream worker {
    server 192.176.3.4;
    server 192.176.3.5;
    server 192.176.3.6;
    }

    server {
        listen 80;
        server_name granz.channel.a15.com;

        location / {
            proxy_pass http://worker;
        auth_basic "Authorized Content";
        auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;
        }
        
        location ~ /\.ht {
                deny all;
            }

        location /its {
                    proxy_pass https://www.its.ac.id;
            }

    } ' > /etc/nginx/sites-available/lbphp
    ```

    </br><img src="img/11.png?raw=true" alt="Alt text" title="1a" width="600">

## 12. Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. hint: (fixed in dulu clinetnya)

-   Melakukann konfigurasi
    ```
    echo ' upstream worker {
    server 192.176.3.4;
    server 192.176.3.5;
    server 192.176.3.6;
    }

    server {
        listen 80;
        server_name granz.channel.a15.com;

        location / {
            proxy_pass http://worker;
        auth_basic "Authorized Content";
        auth_basic_user_file /etc/nginx/rahasisakita/.htpasswd;
        
        allow 192.176.3.69;
            allow 192.176.3.70;
            allow 192.176.4.167;
            allow 192.176.4.168;
            deny all;

        }
        
        location ~ /\.ht {
                deny all;
            }

        location /its {
                    proxy_pass https://www.its.ac.id;
            allow all;
            }

    } ' > /etc/nginx/sites-available/lbphp
    ```
-   Result
    </br><img src="img/12.png?raw=true" alt="Alt text" title="1a" width="600">
    </br>untuk memangkas waktu menambah 
allow 192.176.4.24;
supaya dapat mempercepat pengecekan
    </br><img src="img/12b.png?raw=true" alt="Alt text" title="1a" width="600">


## 13. Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern.
-   Menambahkan script
    ```
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
-   Mengganti [bind-address] pada file /etc/mysql/mariadb conf.d/50-server.cnf menjadi 0.0.0.0

    ```
    echo '#
    # These groups are read by MariaDB server. Use it for options that only the server (but not clients) should see
    #
    # See the examples of server my.cnf files in /usr/share/mysql

    # this is read by the standalone daemon and embedded servers
    [server]

    # this is only for the mysqld standalone daemon
    [mysqld]

    #
    # * Basic Settings
    #
    user                    = mysql
    pid-file                = /run/mysqld/mysqld.pid
    socket                  = /run/mysqld/mysqld.sock
    #port                   = 3306
    basedir                 = /usr
    datadir                 = /var/lib/mysql
    tmpdir                  = /tmp
    lc-messages-dir         = /usr/share/mysql
    #skip-external-locking

    # Instead of skip-networking the default is now to listen only on
    # localhost which is more compatible and is not less secure.
    bind-address            = 0.0.0.0

    #
    # * Fine Tuning
    #
    #key_buffer_size        = 16M
    #max_allowed_packet     = 16M
    #thread_stack           = 192K
    #thread_cache_size      = 8
    # This replaces the startup script and checks MyISAM tables if needed
    # the first time they are touched
    #myisam_recover_options = BACKUP
    #max_connections        = 100
    #table_cache            = 64
    #thread_concurrency     = 10

    #
    # * Query Cache Configuration
    #
    #query_cache_limit      = 1M
    query_cache_size        = 16M

    #
    # * Logging and Replication
    #
    # Both location gets rotated by the cronjob.
    # Be aware that this log type is a performance killer.
    # As of 5.1 you can enable the log at runtime!
    #general_log_file       = /var/log/mysql/mysql.log
    #general_log            = 1
    #
    # Error log - should be very few entries.
    #
    log_error = /var/log/mysql/error.log
    #
    # Enable the slow query log to see queries with especially long duration
    #slow_query_log_file    = /var/log/mysql/mariadb-slow.log
    #long_query_time        = 10
    #log_slow_rate_limit    = 1000
    #log_slow_verbosity     = query_plan
    #log-queries-not-using-indexes

    # The following can be used as easy to replay backup logs or for replication.
    # note: if you are setting up a replication slave, see README.Debian about
    #       other settings you may need to change.
    #server-id              = 1
    #log_bin                = /var/log/mysql/mysql-bin.log
    expire_logs_days        = 10
    #max_binlog_size        = 100M
    #binlog_do_db           = include_database_name
    #binlog_ignore_db       = exclude_database_name

    #
    # * Security Features
    #
    # Read the manual, too, if you want chroot!
    #chroot = /var/lib/mysql/
    #
    # For generating SSL certificates you can use for example the GUI tool "tinyca".
    #
    #ssl-ca = /etc/mysql/cacert.pem
    #ssl-cert = /etc/mysql/server-cert.pem
    #ssl-key = /etc/mysql/server-key.pem
    #
    # Accept only connections using the latest and most secure TLS protocol version.
    # ..when MariaDB is compiled with OpenSSL:
    #ssl-cipher = TLSv1.2
    # ..when MariaDB is compiled with YaSSL (default in Debian):
    #ssl = on

    #
    # * Character sets
    #
    # MySQL/MariaDB default is Latin1, but in Debian we rather default to the full
    # utf8 4-byte character set. See also client.cnf

    #
    character-set-server  = utf8mb4
    collation-server      = utf8mb4_general_ci

    #
    # * InnoDB
    #
    # InnoDB is enabled by default with a 10MB datafile in /var/lib/mysql/.
    # Read the manual for more InnoDB related options. There are many!

    #
    # * Unix socket authentication plugin is built-in since 10.0.22-6
    #
    # Needed so the root database user can authenticate without a password but
    # only when running as the unix root user.
    #
    # Also available for other users if required.
    # See https://mariadb.com/kb/en/unix_socket-authentication-plugin/

    # this is only for embedded server
    [embedded]

    # This group is only read by MariaDB servers, not by MySQL.
    # If you use the same .cnf file for MySQL and MariaDB,
    # you can put MariaDB-only options here
    [mariadb]

    # This group is only read by MariaDB-10.3 servers.
    # If you use the same .cnf file for MariaDB of different versions,
    # use this group for options that older servers don't understand
    [mariadb-10.3]' > 50-server.cnf

    cp 50-server.cnf /etc/mysql/mariadb.conf.d/50-server.cnf

    ```
-   Jalankan perintah ini
    ```
    mysql -u root -p

    CREATE USER 'kelompoka15'@'%' IDENTIFIED BY 'passworda15';
    CREATE USER 'kelompoka15'@'localhost' IDENTIFIED BY 'passworda15';
    CREATE DATABASE dbkelompoka15;
    GRANT ALL PRIVILEGES ON *.* TO 'kelompoka15'@'%';
    GRANT ALL PRIVILEGES ON *.* TO 'kelompoka15'@'localhost';
    FLUSH PRIVILEGES;
    ```

-   Result
    ```
    mariadb --host=192.176.2.2 --port=3306 --user=kelompoka15 --password=passworda15 dbkelompoka15 -e "SHOW DATABASES;"
    ```

    </br><img src="img/10.png?raw=true" alt="Alt text" title="1a" width="500">

## 14. Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

-   install composser
    ```
    wget https://getcomposer.org/download/2.0.13/composer.phar
    chmod +x composer.phar
    mv composer.phar /usr/local/bin/composer
    ```

-   git clone
    ```
    apt-get install git -y
    cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
    cd /var/www/laravel-praktikum-jarkom && composer update
    ```

-   konfigurasi tiap worker
    ```
    cd /var/www/laravel-praktikum-jarkom && cp .env.example .env
    echo 'APP_NAME=Laravel
    APP_ENV=local
    APP_KEY=
    APP_DEBUG=true
    APP_URL=http://localhost

    LOG_CHANNEL=stack
    LOG_DEPRECATIONS_CHANNEL=null
    LOG_LEVEL=debug

    DB_CONNECTION=mysql
    DB_HOST=192.176.2.2
    DB_PORT=3306
    DB_DATABASE=dbkelompoka15
    DB_USERNAME=kelompoka15
    DB_PASSWORD=passworda15

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
    cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
    cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
    cd /var/www/laravel-praktikum-jarkom && php artisan migrate
    cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
    cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
    cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
    cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
    chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
    ```

-   konfigurasi nginx
    ```
    echo 'server {

    listen [PORT];

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
    }' > /etc/nginx/sites-available/laravelworker
    ```

-   Testing
    ```
    lynx localhost:[PORT]
    ```
    </br><img src="img/14.png?raw=true" alt="Alt text" title="1a" width="500">

## 15, 16, 17. Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire. 

### a.POST /auth/register (15)

- melakukan konfigurasi
    ```
    echo '
    {
        "username": "kelompoka15",
        "password": "a15inilho"
    }' > register.json
    ```

-   Result
    ```
    ab -n 100 -c 10 -p register.json -T application/json http://192.176.4.4:8001/api/auth/register
    ```
-   Response  (jika sudah ada)
    </br><img src="img/15a1.png?raw=true" alt="Alt text" title="1a" width="700">

-   Response (error credential)
    </br><img src="img/15a2.png?raw=true" alt="Alt text" title="1a" width="700">

-   Testing (Testing)
    </br><img src="img/15a3.png?raw=true" alt="Alt text" title="1a" width="700">

### b.POST /auth/login (16)
- melakukan konfigurasi
    ```
    echo '
    {
    "username": "kelompoka15",
    "password": "a15inilho"
    }' > login.json
    ```
- result
    ```
    ab -n 100 -c 10 -p login.json -T application/json http://192.176.4.4:8001/api/auth/login
    ```

-   Response  (jika ditemukan)
    </br><img src="img/16a1.png?raw=true" alt="Alt text" title="1a" width="700">

-   Response (jika belum ada)
    </br><img src="img/16a2.png?raw=true" alt="Alt text" title="1a" width="700">

-   Testing
    </br><img src="img/16a3.png?raw=true" alt="Alt text" title="1a" width="700">

### c.GET /me (17)
-   Mendapatkan token
    ```
    curl -X POST -H "Content-Type: application/json" -d '{"username": "kelompoka15", "password": "a15inilho"}' http://192.176.4.4:8001/api/auth/login | jq -r '.token' > set_token.txt
    ```

-   Set global token
    ```
    token=$(cat set_token.txt); curl -H "Authorization: Bearer $token" http://192.176.4.4:8001/api/me
    ```

-   Jalankan perintah berikut
    ```
    ab -n 100 -c 10 -H "Authorization: Bearer $token" http://192.176.4.4:8001/api/me

    ```
    </br><img src="img/17.png?raw=true" alt="Alt text" title="1a" width="500">

## 18. Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.

-   Melakukan konfigurasi script
    ```
    echo 'upstream workers  {
        server 192.176.4.4:8001;
        server 192.176.4.5:8002;
        server 192.176.4.6:8003;
    }

    server {
            listen 80;
            server_name riegel.canyon.a15.com;

            location / {
            proxy_pass http://workers;
            }
    }' > /etc/nginx/sites-available/laravelworker
    ```
-   Testing
    ```
    ab -n 100 -c 10 -p login.json -T application/json http://riegel.canyon.a15.com/api/auth/login

    ```
-   Result
    </br><img src="img/18a.png?raw=true" alt="Alt text" title="1a" width="600">
    </br><img src="img/18b.png?raw=true" alt="Alt text" title="1a" width="600">

## 19. Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan -pm.max_children -pm.start_servers -pm.min_spare_servers -pm.max_spare_servers sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.

-   Percobaan pertama
    ```
    # First try
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

    service php8.0-fpm restart
    ```
    </br><img src="img/19a.png?raw=true" alt="Alt text" title="1a" width="700">

-   Percobaan kedua
    ```
    # Second try
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

    service php8.0-fpm restart
    ```
    </br><img src="img/19b.png?raw=true" alt="Alt text" title="1a" width="700">

-   Percobaan ketiga
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
    pm.max_children = 20
    pm.start_servers = 8
    pm.min_spare_servers = 4
    pm.max_spare_servers = 12' > /etc/php/8.0/fpm/pool.d/www.conf

    service php8.0-fpm restart
    ```
    </br><img src="img/19c.png?raw=true" alt="Alt text" title="1a" width="700">

## 20. Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.

-   Menggunakan algoritma least connection

    ```
    echo 'upstream workerss  {
        least_conn;
        server 192.176.4.4:8001;
        server 192.176.4.5:8002;
        server 192.176.4.6:8003;
    }

    server {
            listen 80;
            server_name riegel.canyon.a15.com;

            location / {
            proxy_bind 192.176.2.3;
            proxy_pass http://workerss;
            }
    }' > /etc/nginx/sites-available/laravelworker
    ```
-   Testing
    ```
    ab -n 100 -c 10 -p login.json -T application/json http://riegel.canyon.a15.com/api/auth/login
    ```
    </br><img src="img/20.png?raw=true" alt="Alt text" title="1a" width="700">