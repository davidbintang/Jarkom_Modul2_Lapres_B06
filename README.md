# Jarkom_Modul2_Lapres_B06

## SOAL

![image](https://user-images.githubusercontent.com/60419316/98804307-99b5b600-2448-11eb-9010-68e7223879b8.png)

Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci
Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server
yang berada di MALANG, MOJOKERTO dan PROBOLINGGO. Server MALANG akan digunakan
sebagai DNS Server Master, MOJOKERTO akan digunakan sebagai DNS Server Slave dan
PROBOLINGGO akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan
untuk testing oleh Bibah yaitu GRESIK dan SIDOARJO. Untuk menyambungkan semua jaringan
tersebut Bibah memberi router di SURABAYA.

Kalian diminta untuk membuat sebuah website utama dengan (1) alamat http://semeruyyy.pw yang
memiliki (2) alias http://www.semeruyyy.pw, dan (3) subdomain http://penanjakan.semeruyyy.pw
yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO serta dibuatkan (4)
reverse domain untuk domain utama. Untuk mengantisipasi server dicuri/rusak, Bibah minta dibuatkan
(5) DNS Server Slave pada MOJOKERTO agar Bibah tidak terganggu menikmati keindahan Semeru
pada Website. Selain website utama Bibah juga meminta dibuatkan (6) subdomain dengan alamat
http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP
Server PROBOLINGGO. Bibah juga ingin memberi petunjuk mendaki gunung semeru kepada anggota
komunitas sehingga dia meminta dibuatkan (7) subdomain dengan nama
http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.

Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. (8)
Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web
dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya
kurang bagus, maka (9) diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.
(10) Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang
memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur
folder sebagai berikut:

/var/www/penanjakan.semeruyyy.pw  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;/public/javascripts  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;/public/css  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;/public/images  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;/errors

(11) Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya
tidak dibolehkan. (12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada
folder /errors untuk mengganti error default 404 dari Apache. (13) Untuk mengakses file assets
javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts.
Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets
menjadi http://penanjakan.semeruyyy.pw/js.
Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena
menunggu pengerjaan website selesai. (14) sedangkan web http://naik.gunung.semeruyyy.pw
sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada
/var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw
bersifat private (15) Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar
diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya
aman dan tidak sembarang orang bisa mengaksesnya.
Saat Bibah mengunjungi IP PROBOLINGGO, yang muncul bukan web utama
http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. (16) Karena
dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan
secara otomatis ke http://semeruyyy.pw. (17) Karena pengunjung pada
/var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar
yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

## JAWABAN

### 1. Membuat DNS

- Membuat topologi berdasarkan foto pada soal.

#### Instalasi bind

- Buka _MALANG_ dan update package lists dengan menjalankan command:

  ```
  apt-get update
  ```

- install aplikasi bind9 pada _MALANG_ dengan command :

  ```
  apt-get install bind9 -y
  ```

#### Pembuatan Domain

Membuat website utama dengan alamat domain **semerub06.pw**.

- Lakukan perintah pada _MALANG_ dengan command :

  ```
   nano /etc/bind/named.conf.local
  ```

- Isi konfigurasi domain **semerub06.pw** sesuai dengan syntax berikut:

  ```
  zone "semerub06.pw" {
  	type master;
  	file "/etc/bind/jarkom/semerub06.pw";
  };
  ```

- Buat folder **jarkom** di dalam **/etc/bind**

  ```
  mkdir /etc/bind/jarkom
  ```

- Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **semerub06.pw**

  ```
  cp /etc/bind/db.local /etc/bind/jarkom/semerub06.pw
  ```

- Kemudian buka file **semerub06.pw** dan edit seperti gambar berikut dengan IP _MALANG_ , yaitu `10.151.83.58

  ```
  nano /etc/bind/jarkom/jarkom2020.com
  ```
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no1-2.png) 
  
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no1.png)



- Restart bind9 dengan perintah

  ```
  service bind9 restart
  ```


- Untuk mencoba koneksi DNS, lakukan ping domain **semerub06.pw** dengan melakukan perintah berikut pada client _GRESIK_ dan _SIDOARJO_

  ```
  ping semerub06.pw
  ```


### 2. Menambah alias menggunakan Record CNAME

- Buka file **semerub06.pw** pada server _MALANG_ dan tambahkan konfigurasi seperti pada gambar berikut:

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no2.png)

- Kemudian restart bind9 dengan perintah

  ```
  service bind9 restart
  ```

- Lalu cek dengan melakukan **ping www.semerub06.pw**.
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no2-2.png)


### 3. Membuat Subdomain http://penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO `10.151.83.60`

- Edit file **/etc/bind/jarkom/semerub06.pw** lalu tambahkan subdomain untuk **semerub06.pw** yang mengarah ke IP _MALANG_.

  ```
  nano /etc/bind/jarkom/semerub06.pw
  ```

- Tambahkan konfigurasi seperti pada gambar ke dalam file **semerub06.pw**.

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no3.png)

- Restart service bind

  ```
  service bind9 restart
  ```

- Coba ping ke subdomain dengan perintah berikut dari client _GRESIK_

  ```
  ping penanjakan.semerub06.pw

  ```
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no3-2.png)


### 4. Reverse domain untuk domain utama

- Edit file **/etc/bind/named.conf.local** pada _MALANG_

  ```
  nano /etc/bind/named.conf.local
  ```

- Lalu tambahkan konfigurasi berikut ke dalam file **named.conf.local**

  ```
  zone "83.151.10.in-addr.arpa" {
      type master;
      file "/etc/bind/jarkom/83.151.10.in-addr.arpa";
  };
  ```

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no4.png)

- Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **83.151.10.in-addr.arpa**

  ```
  cp /etc/bind/db.local /etc/bind/jarkom/83.151.10.in-addr.arpa
  ```

- Edit file **83.151.10.in-addr.arpa** menjadi seperti gambar di bawah ini

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no4-2.png)

- Kemudian restart bind9 dengan perintah

  ```
  service bind9 restart
  ```

- Untuk mengecek apakah konfigurasi sudah benar atau belum, lakukan perintah berikut pada client _GRESIK_

  ```
  // Install package dnsutils
  // Pastikan nameserver telah dikembalikan ke settingan awal
  apt-get update
  apt-get install dnsutils

  //Kembalikan nameserver agar tersambung dengan MALANG
  host -t PTR "IP MALANG"
  ```

### 5. Membuat DNS Server Slave pada MOJOKERTO

#### Konfigurasi Pada Server MALANG

- Edit file **/etc/bind/named.conf.local** dan sesuaikan dengan syntax berikut

  ```
  zone "semerub06.pw" {
      type master;
      notify yes;
      also-notify { 10.151.83.59; }; // Masukan IP MOJOKERTO tanpa tanda petik
      allow-transfer { 10.151.83.59; }; // Masukan IP MOJOKERTO tanpa tanda petik
      file "/etc/bind/jarkom/semerub06.pw";
  };
  ```

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no5.png)

- Lakukan restart bind9

  ```
  service bind9 restart
  ```

#### Konfigurasi Pada Server MOJOKERTO

- Buka _MOJOKERTO_ dan update package lists dengan menjalankan command:

  ```
  apt-get update
  ```

- Setalah melakukan update silahkan install aplikasi bind9 pada _MOJOKERTO_ dengan perintah:

  ```
  apt-get install bind9 -y
  ```

- Kemudian buka file **/etc/bind/named.conf.local** pada MOJOKERTO dan tambahkan syntax berikut:

  ```
  zone "semerub06.pw" {
      type slave;
      masters { 10.151.83.58; }; // Masukan IP MALANG tanpa tanda petik
      file "/var/lib/bind/semerub06.pw";
  };
  ```



- Lakukan restart bind9

  ```
  service bind9 restart
  ```


### 6. & 7. Delegasi Subdomain

#### Konfigurasi Pada Server _MALANG_

- Pada _MALANG_, edit file **/etc/bind/jarkom/semerub06.pw** dan ubah menjadi seperti di bawah ini sesuai dengan pembagian IP _MALANG_ `10.151.83.58`

  ```
  nano /etc/bind/jarkom/semerud04.pw
  ```

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no6.png)

- Kemudian edit file **/etc/bind/named.conf.options** pada _MALANG_.

  ```
  nano /etc/bind/named.conf.options
  ```

- Kemudian comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**

  ```
  allow-query{any;};
  ```

![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no6-2.png)

- Kemudian edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

  ```
  zone "semerub06.pw" {
      type master;
      file "/etc/bind/jarkom/semerub06.pw";
      allow-transfer { 10.151.83.59; }; // Masukan IP MOJOKERTO tanpa tanda petik
  };
  ```
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no6-3.png)

- Setelah itu restart bind9

  ```
  service bind9 restart
  ```

#### Konfigurasi Pada Server _MOJOKERTO_

- Pada _MOJOKERTO_ edit file **/etc/bind/named.conf.options**

  ```
  nano /etc/bind/named.conf.options
  ```

- Kemudian comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**

  ```
  allow-query{any;};
  ```

- Lalu edit file **/etc/bind/named.conf.local** 

- Kemudian buat direktori dengan nama **delegasi**

- Copy **db.local** ke direktori pucang dan edit namanya menjadi **gunung.semerub06.pw**

  ```
  mkdir /etc/bind/delegasi
  cp /etc/bind/db.local /etc/bind/delegasi/its.jarkom2020.com
  ```

- Kemudian edit file **gunung.semerub06.pw** 

- Restart bind9

  ```
  service bind9 restart
  ```

#### Testing


   dapat kita amati pada kolom keempat terdapat record yang menggunakan titik pada akhir kata dan ada yang tidak. Penggunaan titik berfungsi sebagai penentu FQDN (Fully-Qualified Domain Name) suatu domain.

   Contohnya jika "**jarkom2020.com.**" di akhiri dengan titik maka akan dianggap sebagai FQDN dan akan dibaca sebagai "**jarkom2020.com**" , sedangkan ns1 di atas tidak menggunakan titik sehingga dia tidak terbaca sebagai FQDN. Maka ns1 akan di tambahkan di depan terhadap nilai $ORIGIN sehinga ns1 akan terbaca sebagai "**ns1.jarkom2020.com**" . Nilai $ORIGIN diambil dari penamaan zone yang terdapat pada _/etc/bind/named.conf.local_.

### 8.Domain semerub06.pw dengan DocumentRoot /var/www/semerub06.pw
Langkah awalnya dengan membuat direktori pada /var/www, dengan perintah 
```
mkdir /var/www/semerub06.pw
```
Setelah itu buatlah file config untuk file semerub06.pw, yaitu dengan menjalankan perintah
```
cp /etc/apache2/site-available/default /etc/apache2/sites-available/semerub06.pw.
```
Lalu buka file tersebut dengan
```
nano /etc/apache2/sites-available/semerub06.pw
```
dan ubah file menjadi seperti gambar dibawah ini : 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no8-2.png)
   Setelah itu, save dan exit. Lalu aktifkan file tersebut dengan perintah `a2ensite semerub06.pw` dan berikutnya perintah `service apache2 restart`.

Lalu jalankan perintah berikut ini :

```bash
cd /var/www/semerub06.pw
wget 10.151.36.202/semeru.pw.zip
unzip semeru.pw.zip
cd semeru.pw
mv * ../
rm -r semeru.pw semeru.pw.zip
```

Struktur folder semerub06.pw akan terlihat sebagai berikut: 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no8.png)
Akses website http://semerub06.pw/index.php/home, sehingga akan menampilkan : ![semerud04.pw](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no8-3.png)

### 9. Mod Rewrite untuk domain semerub06.pw/home
Buatlah file .htaccess pada folder /var/www/semerub06.pw. Dan isikan file tersebut seperti pada gambar berikut:
   ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no9.png)

```
Keterangan:
RewriteEngine On -> mengaktifkan modul rewrite pada apache
RewriteCond %{REQUEST_FILENAME} !-d -> aturan tidak akan jalan ketika yang diakses adalah directory
RewriteRule &([^\.]+)$ index.php/$1 [NC,L] -> segala url yang berawalan /index.php/nama_page akan bisa diakses menjadi /nama_page
```

### 10. Memasukkan Konten ke /var/www/semerub06.pw
Langkah awalnya dengan membuat direktori pada /var/www, dengan perintah `mkdir /var/www/penanjakan.semerub06.pw`. Setelah itu buatlah file config untuk file semerub06.pw, yaitu dengan menjalankan perintah 
```
cp /etc/apache2/site-available/default /etc/apache2/sites-available/penanjakan.semerub06.pw
```
Lalu buka file tersebut dengan
```
nano /etc/apache2/sites-available/penanjakan.semerub06.pw
```
dan ubah file menjadi seperti gambar dibawah ini :
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no10.png)
    Setelah itu, save dan exit. Lalu aktifkan file tersebut dengan perintah `a2ensite semerub06.pw` dan berikutnya perintah `service apache2 restart`.

Lalu jalankan perintah berikut ini :

```bash
cd /var/www/penanjakan.semerub06.pw
wget 10.151.36.202/penanjakan.semeru.pw.zip
unzip penanjakan.semeru.pw.zip
cd penanjakan.semeru.pw
mv * ../
rm -r penanjakan.semeru.pw penanjakan.semeru.pw.zip
```

Struktur folder semerud04.pw akan terlihat sebagai berikut: ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no10-2.png)
Akses website http://penanjakan.semerud04.pw, sehingga akan menampilkan : 

### 11. folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan
Ketikkan `nano /etc/apache2/sites-available/penanjakan.semerub06.pw` dan ubah file.
    Restart dengan 
    
```
    service apache2 restart
```

    Lalu akses melalu http://penanjakan.semerub06.pw/public. Lalu akses lagi salah satu folder seperti http://penanjakan.semerub06.pw/public/css 

### 12. Error Code 404
Untuk menampilkan custom file error, buka /etc/apache2/sites-available/penanjakan.semerub06.pw dengan command
```
nano /etc/apache2/sites-available/penanjakan.semerub06.pw
```
Lalu comment ErrorLog serta tambahkan command 
```
ErrorDocument 404 /errors/404.html
```
 ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no12.png)
 
kemudian test dengan memasukkan subdomain asal, maka akan menampilkan :
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no12-2.png)

### 13. Konfigurasi Virtual Host
Jalankan perintah 
```
nano /etc/apache2/sites-available/penanjakan.semerub06.pw
```
Lalu ubah isi file pada bagian Alias /js seperti pada gambar berikut : ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no13.png)

Lalu restart dengan `service apache2 restart`. Akses url http://penanjakan.semerub06.pw/js sehingga akan menampilkan
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no13-2.png)

### 14. Membuat Domain di host 8888
Jalankan perintah 
```
nano /etc/apache2/ports.conf
```
Lalu ubah file seperti berikut 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no14-2.png)
Setelah itu membuat direktori pada /var/www, dengan perintah 
```
mkdir /var/www/naik.gunung.semerub06.pw
```
Setelah itu buatlah file config untuk file semerub06.pw, yaitu dengan menjalankan perintah 
```
cp /etc/apache2/site-available/default /etc/apache2/sites-available/naik.gunung.semerub06.pw
```
Lalu buka file tersebut dengan 
```
nano /etc/apache2/sites-available/naik.gunung.semerub06.pw
```
dan ubah file menjadi seperti gambar dibawah ini : 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no14.png)
Setelah itu, save dan exit. Lalu aktifkan file tersebut dengan perintah `a2ensite naik.gunung.semerub06.pw` dan berikutnya perintah `service apache2 restart`.

Lalu jalankan perintah berikut ini :

```bash
cd /var/www/naik.gunung.semerud04.pw
wget 10.151.36.202/naik.gunung.semeru.pw.zip
unzip naik.gunung.semeru.pw.zip
cd semeru
mv * ../
rm -r semeru naik.gunung.semeru.pw.zip
```

Struktur folder naik.gunung.semerub06.pw akan terlihat sebagai berikut: ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no14-3.png)

Akses website http://naik.penanjakan.semerub06.pw:8888, sehingga akan menampilkan :
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no14-4.png)

### 15. Menambah Password pada naik.gunung.semerub06.pw
Jalankan perintah 
```
htpasswd -c /etc/apache2/htpasswd semeru
```
dan isi password dengan `kuynaikgunung`. Lalu ubah file menjadi seperti berikut ini : ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no15-2.png) 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no15.png)
Lalu restart dengan 
```
service apache2 restart
``` 
Akses website http://naik.penanjakan.semerud04.pw:8888, sehingga akan menampilkan : ![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no15-3.png)

### 16. Setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semerub06.pw 
Jalankan 
``` 
nano /etc/apache2/sites-available/semerub06.pw
``` 
dan ubah file menjadi berikut : 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no16-2.png)
Restart dengan `service apache2 restart`

buat file .htaccess pada /etc/apache2/sites-available/semerub06.pw dan isi dengan syntax berikut :
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no16.png)
dan akses http://10.151.83.60/ sehingga akan menampilkan 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no8-3.png)

### 17. Tiap pencarian yang mengandung string "semeru" akan di direct ke "semeru.jpg"
Buka file .htaccess pada /var/www/penanjakan.semerub06.pw dan ubah menjadi seperti berikut isi filenya : 
![image](https://raw.githubusercontent.com/davidbintang/Jarkom_Modul2_Lapres_B06/main/img/no17.png)

```
Keterangan:
RewriteEngine On -> mengaktifkan modul rewrite pada apache
RewriteCond %{REQUEST_FILENAME} -f -> Mengecek apakah request image yang kita buat memang ada di folder /public/images
RewriteCond %{REQUEST_URI} ! /public/images/semeru.jpg [NC] -> mengecek apakah file yang sedang kita buka merupakan file semeru.jpg
RewriteRule ^public/images/(.*)semeru(.*).jpg$ /public/images/$1semeru.jpg[L,R] -> Jika membuka file yang mengandung substring semeru pada folder /public/images, akan di redirect ke /public/images/semeru.jpg selama kedua kondisi diatas terpenuh
```
