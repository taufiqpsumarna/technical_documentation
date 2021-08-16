# Notifikasi Via Email

### Pre Configure

Lakukan konfigurasi email pada menu Tools &gt; Email dan Pastikan untuk mengaktifkan fitur less secure apps dan menonaktifkan 2FA pada gmail sebelum melanjutkan konfigurasi selanjutnya, bisa klik link berikut ini [https://myaccount.google.com/u/0/lesssecureapps](https://myaccount.google.com/u/0/lesssecureapps)

![](../../.gitbook/assets/image%20%283%29.png)

Keterangan

* Server : server di sini maksudnya adalah IP server email gmail disini saya menggunakan IP server **74.125.200.108**
* Port : gunakan port **587**
* Start TLS : pilih **yes**
* From: Subject Email
* User : Username Email
* Password : Password Email

Buka menu Tools &gt; Netwatch

Contoh dibawah ini adalah membuat notifikasi status jaringan internet, kita gunakan alamat IP DNS Google sebagai indikasi bahwa akses internet dapat diakses.

![Host 8.8.8.8](../../.gitbook/assets/image%20%2846%29.png)

**Script Internet UP**

```text
tool e-mail send to="IT@unicorn.co.id" subject="Core Router Update: Internet Connection Is UP" body="Notifikasi Ini ini dikirim secara otomatis via email admin@unicorn.co.id" start-tls=yes
```

**Script Internet DOWN**

```text
tool e-mail send to="IT@unicorn.co.id" subject="Core Router Update: Internet Connection Is DOWN" body="Notifikasi Ini ini dikirim secara otomatis via email admin@unicorn.co.id" start-tls=yes
```

{% hint style="info" %}
Parameter lainnya dapat dikembangkan dari script diatas
{% endhint %}

