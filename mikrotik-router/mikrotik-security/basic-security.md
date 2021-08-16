# Basic Security

## A.\) Pendahuluan

Untuk mengamankan router mikrotik agar terhindar dari orang yang tidak memiliki izin dalam mengakses router yang kita miliki apalagi ketika router ditempatkan sebagai gateway internet, maka ada **tujuh** hal yang harus dilakukan yaitu:

1. Mengganti User Default
2. Mematikan Service Yang Tidak Diperlukan
3. Mengubah Port Service Default
4. Nonaktifkan Interface Service Mikrotik Neighbors Discovery Protocol \(MNDP\)
5. Mengaktifkan Firewall Akses Router \(Opsional\)
6. Non-Aktifkan BTest Server.
7. Non-Aktifkan MAC Server.
8. Mengamankan Router Secara Fisik.

## B.\) Konfigurasi

### B1.Mengganti User Default

Hal yang satu ini mungkin sedikit disepelekan oleh kebanyakan orang, tetapi hal ini sangat penting dilakukan karena orang pasti akan mencoba pertama kali akses menggunakan username dan password default. Untuk konfigurasi pada winbox dapat dilakukan pada menu **System &gt; Users.**

### B2.Mematikan Service Yang Tidak Diperlukan

Sama seperti sebelumnya service router yang berjalan juga perlu dilakukan pengamanan yaitu dengan mematikan service yang tidak diperlukan. Untuk konfigurasi pada winbox dapat dilakukan pada menu **IP &gt; Services.**

### B3.Mengubah Port / Allow From Service Default

Setelah mematikan service yang tidak diperlukan kemudian ubah port dan allow List default service yang akan kita gunakan. Untuk konfigurasi pada winbox dapat dilakukan pada menu **IP &gt; Services.**

### B4.Nonaktifkan MNDP

Mikrotik Neighbor Discovery Protocol \(MNDP\) adalah sebuah protocol yang berjalan pada layer 2 \(Data-Link Layer\).

Perangkat yang support MNDP, CDP \(Cisco Discovery Protocol\) atau LLDP\(Link Layer Discovery Protocol\) dapat menemukan atau mengetahui informasi router lain seperti informasi identity Router, MAC-Address,dan IP-Address.

Seiring perkembangan RouterOS mulai dari versi **RouterOS 6.41 ke atas** terjadi perubahan dalam melakukan konfigurasi Discovery interface. Pada versi sebelumnya kita hanya perlu melakukan disable pada interface yang tidak ingin terlihat dan melihat Neighboor pada menu Discovery interface.

Tetapi pada versi terbarunya kita diharuskan membuat interface list terlebih dahulu dan kemudian di assign pada **Tab IP&gt;Neighbors.**

Source: [https://citraweb.com/artikel\_lihat.php?id=356](https://citraweb.com/artikel_lihat.php?id=356)

#### **Konfigurasi Interface List**

![Interface Lists ](../../.gitbook/assets/image%20%282%29.png)

#### **Assign Interface Pada Neigbors**

![Discovery Settings](../../.gitbook/assets/image%20%2832%29.png)

{% hint style="danger" %}
Jika menggunakan parameter Not \(!\) maka interface selain dari itu yang akan dibolehkan untuk menggunkan discovery protocol.
{% endhint %}

### B5.Mengaktifkan Firewall Akses Router

Opsi ini bersifat opsional karena dengan **tidak** menggunakan opsi ini maka kita dapat mengakses router dari mana saja tetapi jika akses perangkat router sangat ketat maka opsi ini bisa digunakan.

```text
Contoh:
// Hanya membolehkan akses router dari network tertentu jika bukan drop

//Allow
ip firewall filter chain=input src-address=192.168.x.x/24 dst-port=80,8291 action=allow
//Deny 
ip firewall filter chain=input src-address=!192.168.x.x/24 dst-port=80,8291 action=allow
```

### B6.Non-Aktifkan BTest Server

### B.7.Non-Akitfkan MAC Server

Dengan melakukan disable pada discovery interface bukan berarti Router tidak bisa di remote menggunakan MAC-Address. Jika sebelumnya sudah menyimpan atau mengetahui MAC-Address Router, masih bisa di remote menggunakan MAC-Address. Jika menginginkan Router tidak bisa diremote menggunakan MAC-Address baik melalui Winbox ataupun via telnet, matikan Fitur MAC-Server di Router. _**Tools -&gt; MAC-Server**_ 

![MAC Server](../../.gitbook/assets/image%20%2854%29.png)

{% hint style="info" %}
Sama seperti MNDP opsi allowed interface dapat dikonfigurasi, artinya MAC Server dapat berjalan pada interface yang terpilih saja.
{% endhint %}

### B8.Mengamankan Router Secara Fisik

Mikrotik adalah perangkat hardware elektronik sebagaimana perangkat elektronik lainnya yang membutuhkan perawatan Fisik seperti :

* Proteksi kabel power agar jangan terlalu sering di cabut pasang.
* Ruang pendingin untuk menjaga suhu perangkat mikrotik.
* Perlindungan terhadap lonjangan listrik menggunakan UPS, atau yang melewati POE sebaiknya gunakan Arester.





Source: [http://mikrotik.co.id/artikel\_lihat.php?id=263](http://mikrotik.co.id/artikel_lihat.php?id=263)





