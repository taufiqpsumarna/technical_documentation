# T.1. Centos 7: Welcome To Emergency Mode

Kejadian yang sangat ditakuti oleh server administrator adalah **SERVER TIDAK DAPAT BERJALAN DENGAN NORMAL** apalagi hal ini terjadi ketika server kehilangan daya listriknya, membuat sistem operasi pada server kehilangan beberapa data menyebabkan server error, salah satunya sebagai berikut:

![Welcome To Emergency Mode](../../.gitbook/assets/image%20%2811%29.png)

Jujur hal ini membuat saya tidak bisa tidur selama seminggu haha, dan akhirnya saya menemukan solusinya, silahkan perhatikan langkah untuk troubleshootingnya sebagai berikut

## Problem Cause

* Tidak mematikan server secara benar sesuai SOP.
* Server tiba-tiba kehilangan daya listrik.
* xfs\_want\_corrupted\_goto at line &lt;number&gt;
* failed to mount /sysroot

## Troubleshooting

#### 1. Masuk ke terminal console server, cek penyebab gagal booting

```
# journalctl -xe
```

#### 2. Perhatikan Log

```
[    5.487436] localhost mount[570]: mount: mount /dev/mapper/centos-root on /sysroot failed: Structure needs cleaning
[    5.487681] localhost systemd[1]: sysroot.mount mount process exited, code=exited status=32
[    5.487851] localhost systemd[1]: Failed to mount /sysroot. <==Penyebab Masalah Ada Disini==>
[    5.488055] localhost systemd[1]: Dependency failed for Initrd Root File System.
[    5.488227] localhost systemd[1]: Dependency failed for Reload Configuration from the Real Root.
[    5.488387] localhost systemd[1]: Job initrd-parse-etc.service/start failed with result 'dependency'.
[    5.488548] localhost systemd[1]: Triggering OnFailure= dependencies of initrd-parse-etc.service.
[    5.488709] localhost systemd[1]: Job initrd-root-fs.target/start failed with result 'dependency'.
[    5.488883] localhost systemd[1]: Triggering OnFailure= dependencies of initrd-root-fs.target.
[    5.489053] localhost systemd[1]: Unit sysroot.mount entered failed state.
[    5.489213] localhost systemd[1]: Closed Open-iSCSI iscsiuio Socket.
[    5.489373] localhost systemd[1]: Stopping Open-iSCSI iscsiuio Socket.
[    5.489534] localhost systemd[1]: Reached target Initrd File Systems.
[    5.489697] localhost systemd[1]: Starting Initrd File Systems.
[    5.489859] localhost systemd[1]: Stopped dracut pre-mount hook.
```

Perhatikan dengan seksama, biasanya yang menyebabkan error ditandai dengan tulisan berwarna merah.

**3. Repair file sistem yang corrupt**

```text
# xfs_repair -v -L /dev/mapper/centos-root-app
xfs_repair -v -L /dev/mapper/centos-root-home
xfs_repair -v -L /dev/dm-1
xfs_repair -v -L /dev/dm-0
reboot
```

Jalankan perintah diatas satu per satu, dan tunggu hingga proses perbaikan data selesai.

_Notes: waktu proses repair data tergantung tingkat kerusakan data pada server, harap bersabar ketika proses repair berlangsung._

## Conclusion

Untuk menghindari kejadian tersebut terulang kembali, alangkah baiknya server menggunakan sistem UPS agar listrik tetap stabil dan jika server perlu dinonaktifkan, dinonaktifkan sesuai prosedur yang benar.

Sumber:

{% embed url="https://forums.centos.org/viewtopic.php?t=73815" %}

[https://unix.stackexchange.com/questions/337289/how-to-repair-centos-failed-to-mount-sysroot](https://unix.stackexchange.com/questions/337289/how-to-repair-centos-failed-to-mount-sysroot)



