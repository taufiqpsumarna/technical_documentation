# Quality Of Service

## A.\) Pendahuluan

Kali ini saya akan membahas tentang konfigurasi Quality Of Service pada router mikrotik, sebelum lanjut kita jelaskan dulu apa itu QoS \(Quality Of Service\)

> QoS \(Quality Of Service\) mengacu pada teknologi apa pun yang mengelola lalu lintas data untuk mengurangi packet loss \(kehilangan paket\), latency, dan jitter pada jaringan. QoS mengontrol dan mengelola sumber daya jaringan dengan menetapkan prioritas untuk tipe data tertentu pada jaringan.
>
> source: [https://onlinelearning.binus.ac.id/computer-science/post/qos-quality-of-services/](https://onlinelearning.binus.ac.id/computer-science/post/qos-quality-of-services/)

Singkatnya QoS Adalah cara bagaimana cara mengelola traffic yang berjalan pada sebuah jaringan agar berjalan dengan lancar walaupun kondisi jaringan sedang full load, untuk lebih jelasnya silahkan lihat ilustrasi bagaimana QoS Bekerja dibawah ini.

![Ilustrasi QoS](../../.gitbook/assets/image%20%2824%29.png)

> Image Source: [https://ilicomm.com/how-to-use-quality-of-service-qos-to-get-faster-internet-when-you-really-need-it/](https://ilicomm.com/how-to-use-quality-of-service-qos-to-get-faster-internet-when-you-really-need-it/)

Terlihat bahwa sebelum QoS di terapkan traffic yang berjalan tidak beraturan atau tidak ada pembatas sama sekali, hal ini yang menyebabkan delay, jitter, dan buffering. tetapi setelah diterapkan QoS traffic sudah diberikan jalur khusus atau pembatas sehingga traffic yang berjalan akan berjalan lancar.

## B.\) Bagaimana Cara Menerapkan QoS

Sebelum menerapkan QoS ada beberapa hal yang harus diketahui diantaranya:

### B.1\) Tentukan tujuan utama QoS.

Tentukan tujuan utama dari QoS misalnya "saya akan melakukan prioritas terhadap traffic video conference supaya video conference berjalan dengan lancar" atau "User ada yang mengakses Internet Banking maka traffic Internet Banking saya prioritaskan".

### B.2\) Bandwidth internet yang digunakan.

Lakukan inspeksi terhadap kecepatan internet yang digunakan, bandwidth download dan upload perlu diperhatikan karena hal ini akan mempengaruhi bagaiman proposi bandwith yang akan digunakan.

### B.3\) Topologi Jaringan.

Hal yang wajib diketahui sebelum menerapkan QoS pada jaringan adalah Topologi Jaringan, kenali terlebih dahulu perangkay yang digunakan dalam jaringan, jumlah user, jenis topologi yang digunakan dll.

### B.4\) Klasifikasi Traffic Lokal dan Internet.

Setelah mengetahui tiga point diatas yang terakhir adalah ketahui terlebih dahulu traffic yang berjalan pada jaringan, biasanya saya melakukan klasifikasi traffic secara besar yaitu Traffic Lokal dan Internet.

Traffic Local: CCTV, Server, Intranet, Local VoIP, dll

Traffic Internet: Browsing, Streaming, Download/Upload \(Seluruh Traffic Yang Keluar Dari Jaringan Lokal\)

{% hint style="info" %}
Umumnya dalam QoS akan mempriotaskan beberapa service yang membutuhkan latensi dan stabilisasi yang baik seperti:

* Internet Banking
* Video Conference
* VoIP
* dll
{% endhint %}

