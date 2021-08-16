---
description: Zimbra 8.6.0_GA_1153.FOSS dengan sistem operasi Linux Centos 7
---

# T.2. PID File Not Found

## Problem Cause

* PID file pada /opt/zimbra/log/\* tidak ditemukan atau hilang.

## Troubleshooting

1. **Restart atau start service**

```text
$zimbra@mail: zmcontrol restart
```

**2. Kemudian kita cek status zimbra yang berjalan pada server**

```text
$zimbra@mail: zmcontrol status
```

_Dan jika ketika dilakukan cek service zimbra yang berjalan pada server, terdapat sebuah pemberitahuan bahwa service is not running, seperti dibawah ini._

```text
$zimbra@mail:
Host mail.domain.co.id
        antispam                Running
        antivirus               Running
        dnscache                Running
        ldap                    Running
        logger                  Running
        mailbox                 Stopped
                zmmailboxdctl is not running.
        mta                     Running
        opendkim                Running
        service webapp          Stopped
                zmmailboxdctl is not running.
        snmp                    Running
        stats                   Running
        zimbra webapp           Stopped
                zmmailboxdctl is not running.
        zimbraAdmin webapp      Stopped
                zmmailboxdctl is not running.
        zimlet webapp           Stopped
                zmmailboxdctl is not running.
        zmconfigd               Running
```

**3. Cek file log pada /var/log/zimbra.log**

```text
$root@mail: tail /var/log/zimbra.log
$root@mail: 
Sep 26 08:34:04 mail zmmailboxdmgr[2925]: stale pid 15273 found in /opt/zimbra/log/zmmailboxd_manager.pid: No such process
Sep 26 08:34:04 mail zmmailboxdmgr[2925]: assuming no other instance is running
Sep 26 08:34:04 mail zmmailboxdmgr[2925]: file /opt/zimbra/log/zmmailboxd.pid does not exist
Sep 26 08:34:04 mail zmmailboxdmgr[2925]: assuming no other instance is running
Sep 26 08:34:04 mail zmmailboxdmgr[2925]: no manager process is running
Sep 26 08:34:05 mail zmmailboxdmgr[2955]: stale pid 15273 found in /opt/zimbra/log/zmmailboxd_manager.pid: No such process
Sep 26 08:34:05 mail zmmailboxdmgr[2955]: assuming no other instance is running
Sep 26 08:34:05 mail zmmailboxdmgr[2955]: file /opt/zimbra/log/zmmailboxd.pid does not exist
Sep 26 08:34:05 mail zmmailboxdmgr[2955]: assuming no other instance is running
Sep 26 08:34:05 mail zmmailboxdmgr[2955]: no manager process is running
```

_Jika kita lihat, ternyata service zmailboxd\_manager.pid tidak ditemukan, itulah yang menyebabkan mengapa service zmailboxdctl tidak berjalan pada zimbra._

**4. Stop service zimbra**

Sebelum lanjut ke proses selanjutnya, berhentikan seluruh proses service zimbra.

```text
$zimbra@mail: zmcontrol stop
```

**5. Buat kembali PID file**

setelah melakukan stop service zimbra, kemudian kembalikan PID file yaitu dengan menghapus PID file lama pada /opt/zimbra/log/...

```text
#Cek kelengkapan PID zimbra
$root@mail: cd /opt/zimbra/log/
$root@mail: ls -la | grep

-rw-r-----   1 zimbra zimbra       6 Sep 26 08:09 amavisd.pid
-rw-r-----   1 zimbra zimbra       5 Sep 21 17:50 amavisd.pid.backup
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:08 amavis-mc.pid
-rw-r-----   1 zimbra zimbra       6 Sep 21 17:05 amaviz.pid
-rw-rw-r--   1 zimbra zimbra       6 Sep 26 08:11 clamd.pid
-rw-rw----   1 zimbra zimbra       6 Sep 26 08:10 freshclam.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:08 logswatch.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:10 opendkim.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:10 swatch.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:07 unbound.pid
-rw-r-----   1 zimbra zimbra       5 Sep 21 21:21 zmcheckversion.pid
-rw-r-----   1 zimbra zimbra       5 Oct  4  2019 zmclientcertmgr.pid
-rwxrwxrwx   1 zimbra zimbra       6 Oct 19  2015 zmconfigdctl.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:07 zmconfigd.pid
-rw-r-----   1 zimbra zimbra       4 Dec  1  2019 zmcpustat_pid
-rw-r--r--   1 zimbra zimbra       5 Sep 10 07:30 zmdnscachectl.pid
-rw-r-----   1 zimbra zimbra       4 Jul  5  2019 zmgsaupdate.pid
-rw-r--r--   1 zimbra zimbra       4 Sep 21 09:45 zmlogswatch.pid
-rw-r--r--   1 zimbra zimbra       6 Sep 26 08:11 zmmailboxd_java.pid
-rw-r--r--   1 zimbra zimbra       6 Sep 26 08:10 zmmailboxd_manager.pid
-rw-r-----   1 zimbra zimbra       5 Jul  5  2019 zmmysqlstatus.pid
-rw-r-----   1 zimbra zimbra       6 Sep 26 08:08 zmrrdfetch-server.pid
-rw-r-----   1 zimbra zimbra       5 Jul  2  2019 zmstat.pid
-rw-r--r--   1 zimbra zimbra       4 Sep 21 09:55 zmswatch.pid
```

**5. Rename PID file service zimbra yang bermasalah**

karena disini yang bermasalah merupakan zmailboxd\_manager.pid, silahkan rename file tersebut dengan akhiran .bak sesuaikan dengan nama pid file yang bermasalah pada server kamu.

```text
$root@mail: mv zmmailboxd_manager.pid zmmailbox_manager.pid.bak
```

**6. Restart service zimbra**

kemudian coba restart service zimbra

```text
$root@mail: su - zimbra -c 'zmcontrol start'
```

## Conclusion

Jika setelah menghapus pid file dan ketika cek service zimbra masih status _xxx is not running_ abaikan saja setelah saya cek ternyata itu bug, coba kamu cek zimbra webmail / outlook jika semua berjalan dengan normal itu artinya service zimbra berjalan baik.

