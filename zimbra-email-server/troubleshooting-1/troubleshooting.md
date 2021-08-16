---
description: Zimbra 8.6.0_GA_1153.FOSS dengan sistem operasi Linux Centos 7
---

# T.1. Service Zimbra Tidak Berjalan

## Problem Cause

Biasanya ada dua kemungkinan penyebab service zimbra tidak berjalan yaitu sebagai berikut:

* Port service zimbra digunakan oleh service lain.
* Kesalahan konfigurasi service zimbra.
* PID file pada _/opt/zimbra/log/\*_ tidak ditemukan.

## Troubleshooting

#### 1. Cek service dan port yang berjalan

```
$root@mail: ss -tulnp
$root@mail: netstat -tulnp
```

#### 2. Cek service dan port yang berjalan

```
$root@mail: ss -tulnp
$root@mail: netstat -tulnp
```

**3. Jika ditemukan service yang berjalan hentikan**

```text
$root@mail: kill <PID Number>
```

**4. Restart service zimbra**

```text
$root@mail: su - zimbra -c 'zmcontrol restart'
```

## Conclusion

Coba cek ada beberapa service pada server yang berjalan sendiri ketika server reboot solusinya ubah settingan port pada service yang berjalan sendiri tadi, kita dapat menggunakan command kill &lt;PID Number&gt; jika ditemukan proses yang menyebabkan service zimbra tidak berjalan dengan lancar.



