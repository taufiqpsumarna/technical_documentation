---
description: Pada halaman ini akan menjelaskan bagaimana konfigurasi standar mikrotik.
---

# Mikrotik Basic Configuration

## Persiapan Sebelum Memulai

Sebelum memulai pastikan beberapa hal dibawah ini terpenuhi:

* IP Address sumber internet.
* Mikrotik Routerboard / X86.
* Software winbox.
* Kabel Ethernet.

## Langkah Pengerjaan

### A. Reset Mikrotik

Saya sarankan untuk melakukan reset total  ketika melakukan konfigurasi pada router mikrotik baru ataupun bekas pakai.

Untuk langkah reset mikrotik routerboard sebagai berikut: 

### Via Hardware

Setiap RouterBoard memiliki tombol reset fisik yang berbeda ada yang posisinya masuk kedalam sehingga kita perlu alat bantu untuk menekannya ada juga yang berupa tombol yang dapat kita tekan langsung. Tombol ini biasanya terletak dibagian samping dari casing RouterBoard. Cara meresetnya adalah :

1. Pastikan RouterBoard dalam kondisi mati
2. Tekan tombol reset selama kurang lebih 5-10 detik sambil menyalakan RouterBoard
3. Tunggu sampai lampu “USR” selesai berkedip lalu lepas tombol reset

![routerboard hap series](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img,w_319/https://belajarmikrotik.com/wp-content/uploads/2020/02/1.png)

### Via Software

Soft Reset merupakan cara me-reset RouterBoard via Software baik via GUI \(Winbox, Webfig\) atau CLI \(SSH, Telnet dll\).

a. Via GUI

![](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img,w_783/https://belajarmikrotik.com/wp-content/uploads/2020/02/3.png)

b. Via CLI

![](https://cdn.shortpixel.ai/client/to_webp,q_glossy,ret_img,w_503/https://belajarmikrotik.com/wp-content/uploads/2020/02/4.png)

no-defaults=yes adalah perintah agar router ketika proses reset, router tidak kembali ke setting default

sumber: [https://belajarmikrotik.com/cara-reset-mikrotik-routerboard/](https://belajarmikrotik.com/cara-reset-mikrotik-routerboard/)



### B. Konfigurasi Router

Topologi standar yang biasa digunakan adalah sebagai berikut:

* Sumber Internet
* Router
* Komputer Client

![Basic Topologi](../.gitbook/assets/image%20%2827%29.png)

Setelah menentukan topologi yang akan digunakan saatnya kita melakukan konfigurasi router:

1. **Login Mikrotik Via Winbox**

Terlebih dahulu nyalakan router, setelah router selesai booting gunakan kabel ethernet sambungkan ke port 2 untuk melakukan konfigurasi.

Setelah itu buka winbox kemudian klik Tab Neighbors

Klik MAC Address kemudian klik login, username admin password kosongkan

![](../.gitbook/assets/image%20%2819%29.png)

Tips:

* Ada beberapa kasus sumber internet yang menggunakan banyak IP Address Public silahkan konfigurasi src-nat pada core router \[chain: src-nat action src-nat to-address &lt;salah satu ip public&gt;\] hal ini akan memecahkan paket keluar yang looping. Dengan Topologi sebagai berikut \[Internet &gt; Modem &gt; Core &gt; Dist\].

