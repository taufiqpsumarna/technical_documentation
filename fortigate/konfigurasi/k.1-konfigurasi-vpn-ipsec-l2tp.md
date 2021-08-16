# K.1 Konfigurasi VPN IPSEC / L2TP

### A. Pendahuluan

Layer 2 tunneling Protocol \(L2TP\) adalah pengembangan dari peer-to-peer tunneling Protocol \(PPTP\) dan Layer 2 forwarding Protocol \(L2F\).

> Pada tahun 90-an, setelah Microsoft mengembangkan PPTP dan Cisco merespon dengan L2F; Internet Engineering Task Force \(IETF\) mengarahkan kedua perusahaan tersebut untuk memilih salah satu protokol saja untuk menghindari persaingan antar dua protokol tersebut. Dan juga secara langsung memaksa mereka untuk memperbaiki kelemahan dari kedua protokol tersebut. **Setelah Microsoft dan Cisco berkerjasama, mereka menghasilkan protokol L2TP/IPsec.**

Sumber: [https://www.ramitan.com/review/kelebihan-dan-kekurangan-protokol-vpn-l2tp-ipsec/](https://www.ramitan.com/review/kelebihan-dan-kekurangan-protokol-vpn-l2tp-ipsec/)

### B. Konfigurasi

Sebelum memulai konfigurasi ada hal yang perlu diperhatikan yaitu:

* Akses Internet Sudah Berjalan Dengan Baik.
* ISP Mendukung VPN L2TP/IPSEC.
* Memiliki Static IP Publik \(Disarankan\).
* Sudah Membuat Firewall User dan User Group

Oke, setelah ketiga point diatas terpenuhi, lanjut untuk konfigurasi VPN Menggunakan Fortigate, Ikuti Langkah Sebagai Berikut:

1. Login Sebagai Admin Pada Fortigate
2. Pilih Menu VPN &gt; IPSec Wizard.
3. Kemudian Pilih Tab VPN Setup.
   1. Template Type **Remote Access.**
   2. Remote Device Type **Native.**
   3. Sesuaikan dengan perangkat yang digunakan untuk remote access.
   4. Klik Next.
4. Pada Tab Authentication
   1. Pilih Incoming **Interface \(WAN\)**
   2. Gunakan metode **Pre-Shared Key**
   3. Pilih User Group Yang Telah dibuat Sebelumnya
   4. Klik Next.
5. Pada Tab Policy & Routing
   1. Pilih **Local Interface \(LAN\)**
   2. Pilih **Local Address** \(Silahkan Buat Terlebih Dahulu Local Address VPN\)
   3. Pilih **Client Address Range / Remote Address**
   4. Klik Create.
6. Done.

#### Catatan:

Sampai tahap ini client sudah bisa menggunakan VPN IPsec yang telah dibuat, namun akses internet dan jaringan lokal belum terkonfigurasi, cara konfigurasinya sebagai berikut:

1. Pilih menu Policy & Objects
2. Kemudian ubah Policy \(VPN To Local\) services **All**
3. Setelah Itu Tambahkan Policy Agar client VPN dapat mengakses internet melalui interface WAN \(Untuk Alasan Keamanan Sangat Disarankan\).

![IPsec Wizard - VPN Setup](../../.gitbook/assets/image%20%2828%29.png)

![IPsec Tunnels](../../.gitbook/assets/image%20%289%29.png)

![Policy Tambahan](../../.gitbook/assets/image%20%281%29.png)

Allow All Address To Make L2TP Connection Then Allow Only **VPN Address** To Access Internet From Tunnel.

