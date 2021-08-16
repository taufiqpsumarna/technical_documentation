# T.2 Proxmox Dan VM Tidak mendapatkan akses internet

### symptoms:

* Network Interface Sudah terkonfigurasi dengan baik
* Dapat melakukan ping gateway, dan dns 8.8.8.8
* Trace Route mendapatkan rute yang sesuai

Hal yang pertama harus pastikan adalah, pastikan konfigurasi interface telah sesuai sebagai referensi dapat melihat konfigurasi default proxmox interface _\(bridge vmbr0\)._

![Interface Bridged](../../.gitbook/assets/image%20%2845%29.png)

Jika semua sudah benar tetapi masih tidak mendapatkan internet, silahkan cek firewall NAT, Policy, dan perangkat end point, pastikan konfigurasi **Firewall NAT** sudah benar.

Jika konfigurasi **Firewall NAT** sudah sesuai maka proxmox maupun vm dapat mengakses internet.

{% hint style="info" %}
**90% Ini kesalahan konfigurasi firewall NAT yang mengizinkan traffic keluar menuju internet**
{% endhint %}

