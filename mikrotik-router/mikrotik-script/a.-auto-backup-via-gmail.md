# Auto Backup via Gmail

### Pre-Configure

Pastikan untuk mengaktifkan fitur less secure apps dan menonaktifkan 2FA pada gmail sebelum melanjutkan konfigurasi selanjutnya, bisa klik link berikut ini [https://myaccount.google.com/u/0/lesssecureapps](https://myaccount.google.com/u/0/lesssecureapps)

### 1. Konfigurasi Email Pada Router \( Tool &gt; Email \)

![](../../.gitbook/assets/image%20%283%29.png)

Keterangan

* Server : server di sini maksudnya adalah IP server email gmail disini saya menggunakan IP server **74.125.200.108**
* Port : gunakan port **587**
* Start TLS : pilih **yes**
* From: Subject Email
* User : Username Email
* Password : Password Email

### 2. Buat Script Auto Backup

![](../../.gitbook/assets/image%20%2820%29.png)

```text
:local identity [/system identity get name]
:local date [/system clock get date] 
:local time [/system clock get time]
:local day [ :pick $date 4 6 ]
:local month [ :pick $date 0 3 ]
:local year [ :pick $date 7 11 ]

:local months {"jan"="01";"feb"="02";"mar"="03";"apr"="04";"may"="05";"jun"="06";"jul"="07";"aug"="08";"sep"="09";"oct"="10";"nov"="11";"dec"="12"}
:local monthr {"jan";"feb";"mar";"apr";"may";"jun";"jul";"aug";"sep";"oct";"nov";"dec"}

:set month ($months->$month)
:set time ( [:pick $time 0 2].[:pick $time 3 5].[:pick $time 6 8] )

:local filename "$identity-$year$month$day-$time"
:put $filename

/system backup save name=$filename
:delay 5s
/tool e-mail send to="IT@unicorn.co.id" subject="Backup Router Core PT. Unicorn Tosan Perkasa" body="File Backup $identity ini dikirim secara otomatis via email admin@unicorn.co.id tanggal $date" file="$filename.backup" start-tls=yes
:delay 10s
/file remove $filename
```

{% hint style="info" %}
Script diatas akan membuat file backup dengan tipe \*.backup dan akan otomatis menghapus file backup tersebut dari router sehinggan penyimpanan router akan tetap bersih.
{% endhint %}

### 3. Konfigurasi Scheduler

Setelah membuat script AutoBackup saatnya mengatur timer untuk menjalankan script diatas silahkan akses menu \(system &gt; scheduler\)

![](../../.gitbook/assets/image%20%2842%29.png)

{% hint style="info" %}
Silahkan atur waktu mulai dan interval waktu yang dibutuhkan untuk menjalankan script tersebut, sesuaikan nama parameter On Event dengan judul script yang dibuat.
{% endhint %}

