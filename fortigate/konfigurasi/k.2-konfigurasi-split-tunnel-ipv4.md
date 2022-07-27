# K.2 Konfigurasi Split Tunnel IPV4

![](<../../.gitbook/assets/image (55).png>)

### A. Pendahuluan

Pada Konfigurasi VPN Fortigate Firewall Tedapat Dua Cara Bagaimana Alur Traffic Internet, Yaitu Sebagai Berikut:

#### **Seluruh Traffic Melewati Fortigate Firewall**

Ketika user VPN mengakses internet maka traffic tersebut akan melalui fortigate terlebih dahulu kemudian dilanjutkan ke jaringan internet.

Pro

\+  Seluruh Traffic internet user VPN akan tercatat oleh sistem.

\+  Peraturan Akses Akan Sama Dengan User Jaringan Lokal

Cons

* Akan menghabiskan bandwidth internet
* Kinerja router akan lebih berat
* IP Public digunakan user VPN sehingga beresiko terkena blacklist

#### **Traffic Internet & Jaringan Lokal VPN Terpisah**

Ketika user VPN mengakses internet maka traffic tersebut **tidak** akan melalui fortigate terlebih dahulu tetapi langsung dialihkan ke jaringan internet, dan hanya traffic menujur jaringan lokal saja yang akan melalui router fortigate.

### B. Konfigurasi

Konfigurasi dilakukan ketika melakukan IPSEC/VPN Wizard, pastikan untuk menaktifkan opsi **Enable IPv4 Splite Tunnel**

![](<../../.gitbook/assets/image (43).png>)

Jika konfigurasi VPN sudah dilakukan, opsi **IPv4 Splite Tunnel** dapat diaktifkan dengan cara sebagai berikut:

Masuk kedalam menu **VPN > IPSec Tunnels,** Kemudian klik Convert To Custom Tunnel

![](<../../.gitbook/assets/image (8).png>)

Setelah itu checklist Mode Config dan Enable IPv4 Split Tunnel, Kemudian Pilih IP Address atau Jaringan Lokal yang dapat diakses oleh user VPN, dan jangan lupa untuk menentukan **Client Address Range**

![](<../../.gitbook/assets/image (15).png>)

![](<../../.gitbook/assets/image (50).png>)

