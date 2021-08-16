# HetrixTools - Server Uptime Monitoring

![Logo HetrixTools](../../.gitbook/assets/image%20%2848%29.png)

## Pendahuluan

**HetrixTools** adalah sebuah layanan yang dapat kita gunakan untuk monitoring website apakah sedang up atau down \(Uptime Monitor\), selain itu kita bisa juga monitoring apakah IP address atau domain diblacklist \(Blacklist Monitor\).

HetrixTools menyediakan paket Free selamanya, tentunya dengan batasan tertentu dibandingkan yang berbayar. Tapi paket gratis ini sudah cukup untuk kebutuhan personal atau UKM.

Uptime Monitor Free bisa digunakan untuk monitoring 10 website, 10 server \(system monitoring\), pengecekan setiap 1 menit dilakukan dari 4 lokasi server, uptime report history tidak terbatas, dan bisa monitoring kapan domain dan SSL habis masa aktifnya dan tersedia juga berbagai channel notifikasi yang tersedia.

Blacklist Monitor Free bisa digunakan untuk monitoring 32 IPv4/domain, dan pengecekan setiap 24 jam.

## **Konfigurasi HetrixTools**

### A.\) Cara Membuat Uptime Monitor di HetrixTools

1. Daftar dan login Uptime Monitor.
2. Klik menu **Tools-&gt;Uptime Monitors**
3. Klik tombol **Add Monitor**.
4. Pilih **Monitor Type** = Website Monitor \(nama domain\). Pilihan lain yaitu Ping/Service Monitor \(ping protokol tertentu\), dan SMTP Monitor \(mail server\).
5. Masukkan **Monitor Name** = nama website.
6. Masukkan **Website Link** = url website.Menambah Uptime Monitor
7. Pilih 3 **Monitor From** = lokasi server yang melakukan pengecekan status website.
8. Terakhir klik **Add Monitor**.

![Konfigurasi Website Monitoring](https://musaamin.web.id/wp-content/uploads/2019/05/01.cara-monitoring-website-dengan-hetrixtools_tambah-uptime-monitor-min.jpg)

![Lokasi Website Monitoring](https://musaamin.web.id/wp-content/uploads/2019/05/02.cara-monitoring-website-dengan-hetrixtools_lokasi-server-monitor-min.jpg)

### B.\) Peringatan Habis Masa Aktif SSL dan Domain

Fitur ini tidak langsung aktif, tunggu 15-30 menit sampai HetrixTools mendapatkan informasi SSL, domain, dan nameserver.

1. Klik nama website, fitur ini
2. SSL Cert. Expiration = pilih kapan peringatan SSL habis masa aktif dikirimkan.
3. Domain Expiration = pilih kapan peringatan domain habis masa aktif dikirimkan.
4. Domain NameServers = kirim peringatan jika terjadi perubahan di nameserver.

![SSL dan domain expire monitoring](https://musaamin.web.id/wp-content/uploads/2019/05/03.cara-monitoring-website-dengan-hetrixtools_ssl-domain-expire-min.jpg)



### C.\) Setting Channel Notifikasi

Terdapat 12 channel atau metode pengiriman notifikasi, secara default yang aktif adalah email, memakai alamat email yang kita masukkan saat pendaftaran akun HetrixTools.

**Mengaktifkan Notifikasi ke Telegram**

1. Klik foto/nama akun -&gt; **Contact Lists**.
2. Klik icon Edit di kolom **Actions**.
3. Klik Telegram.
4. Ikuti panduan [Telegram Integration](https://docs.hetrixtools.com/telegram-integration/). Cara HetrixTools Bot, Start bot, lalu jalankan perintah /start di chat bot untuk mendpatkan nomor Chat ID.Mendapatkan Chat ID HetrixTools Bot
5. Masukkan nomor yang didapatkan dari HetrixTools Bot ke form edit Contact List – kolom Telegram.Edit Contact List – Telegram
6. Klik **Send test notification** untuk menguji pengiriman notifikasi ke Telegram.
7. Terakhir klik **Edit** untuk menyimpan perubahan.

![Channel Notifikasi](https://musaamin.web.id/wp-content/uploads/2019/05/04.cara-monitoring-website-dengan-hetrixtools_edit-contact-list-min.jpg)

![Notifikasi Via Telegram](https://musaamin.web.id/wp-content/uploads/2019/05/10.cara-monitoring-website-dengan-hetrixtools_hehtrixtools-bot.jpg)

![Notifikasi Via Email](https://musaamin.web.id/wp-content/uploads/2019/05/07.cara-monitoring-website-dengan-hetrixtools_notifikasi-website-up-min.jpg)

### D.\)Install HetrixTools Agent

Untuk mengaktifkan system monitoring server, install HetrixTools agent di Linux server.

1. Klik icon **Setting**di kolom **Actions** -&gt; **Install Monitoring Agent**.
2. Centang **Run agent as root**, **VIew Running Processes?**, **Monitor services?** = masukkan nama service dipisahkan dengan koma maksimal 10 service, misal nginx, php7.2-fpm, mysql, ssh, **Monitor drive health?** = monitoring kondisi disk.
3. Copy **Install Code**, paste di Linux server.
4. Tunggu beberapa menit sampai agent terhubung ke HetrixTools.

![Opsi Monitoring System](https://musaamin.web.id/wp-content/uploads/2019/05/08.cara-monitoring-website-dengan-hetrixtools_install-hetrixtools-agent-min.jpg)

![Monitoring System Server](https://musaamin.web.id/wp-content/uploads/2019/05/09.cara-monitoring-website-dengan-hetrixtools_system-monitorin-min.jpg)

{% hint style="info" %}
Saat Ini saya menggunakan **HetrixTools** sebagai tools monitoring service yang berjalan di kantor, HetrixTools memiliki fitur yang lumayan lengkap seperti:

* Uptime Monitoring
* Service Monitoring
* Website Monitoring
* SSL / Domain Expired Monitoring
* IP Blacklist Monitoring
{% endhint %}

Source: [https://musaamin.web.id/cara-monitoring-website-dengan-hetrixtools/](https://musaamin.web.id/cara-monitoring-website-dengan-hetrixtools/)

