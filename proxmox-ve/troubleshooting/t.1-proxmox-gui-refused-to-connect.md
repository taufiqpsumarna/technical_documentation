# T.1 Proxmox GUI Refused To Connect

Masalah ini terjadi ketika mengubah /etc/hosts 😅

![](../../.gitbook/assets/image%20%2813%29.png)

Format Penulisan **hosts** Seperti Ini, Pastikan hostname dan FQDN telah sesuai

```text
127.0.0.1 localhost
<IP of this server> <FQDN> <host name>
```

sumber: [https://forum.proxmox.com/threads/rebooted-proxmox-and-messed-up-etc-hosts-file.63268/](https://forum.proxmox.com/threads/rebooted-proxmox-and-messed-up-etc-hosts-file.63268/)

kemudian jalankan perintah berikut, untuk melakukan reset konfigurasi

```text
mv /var/lib/pve-cluster/config.db /var/lib/pve-cluster/config.db.old
reboot
```

sumber: [https://forum.proxmox.com/threads/pve-wont-start-after-a-crash-of-vm-an-host-in-the-night.45568/](https://forum.proxmox.com/threads/pve-wont-start-after-a-crash-of-vm-an-host-in-the-night.45568/)

Sesuaikan Storage Layout Seperti Gambar Dibawah Ini

![](../../.gitbook/assets/image%20%2852%29.png)

{% hint style="warning" %}
Solusi Terakhir Install Ulang Proxmox 😥
{% endhint %}

