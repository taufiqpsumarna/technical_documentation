---
description: >-
  Biasanya hal ini terjadi ketika folder zimbra tidak dapat diakses oleh zimbra
  user
---

# T.5. Permission Denied

## Memperbaiki permission pada folder zimbra

Silahkan menghentikan seluruh service zimbra terlebih dahulu:

```bash
$ su zimbra
$ zmcontrol stop
```

Kemudian setelah itu jalankan command untuk memperbaiki folder permission zimbra

```
$ /opt/zimbra/libexec/zmfixperms --extended --verbose
```

Kemudian restart server, sebelum menjalankan kembali server zimbra, setelah server reboot, coba untuk memulai service zimbra kembali

```bash
$ su - zimbra -c "zmcontrol restart"

// Kemudian cek seluruh service pada zimbra

$ su - zimbra -c "zmcontrol status"
```

{% hint style="info" %}
 Jika seluruh service zimbra telah berjalan dengan normal, seharusnya email server sudah mulai berjalan dengan normal kembali.
{% endhint %}



