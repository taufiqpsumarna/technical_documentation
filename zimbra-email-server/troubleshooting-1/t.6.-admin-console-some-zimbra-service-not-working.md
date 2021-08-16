# T.6. Admin Console: Some Zimbra Service Not Working

Server Status yang ada di menu Monitor pada Zimbra Admin Console berwarna merah \(Red X\) atau not running.

Setelah dilakukan pengecekan menggunakan akses remote langsung ke server \(s

```text
# su -  zimbra
$ zmcontrol status
Host mail.contoh.id
        amavis                  Running
        antispam                Running
        antivirus               Running
        convertd                Running
        dnscache                Running
        ldap                    Running
        logger                  Running
        mailbox                 Running
        memcached               Running
        mta                     Running
        opendkim                Running
        proxy                   Running
        service webapp          Running
        snmp                    Running
        spell                   Running
        stats                   Running
        zimbra webapp           Running
        zimbraAdmin webapp      Running
        zimlet webapp           Running
        zmconfigd               Running
```

{% hint style="info" %}
yang pertama kali saya pikirkan ketika melihat error tersebut ialah adanya masalah dengan logger server zimbra.
{% endhint %}

### Resolution \#1

Dugaan berikutnya ialah ada issue rsyslog pada sisi OS, berikut ialah konfigurasi yang kami lakukan utnuk mengatasi Red X di Zimbra Admin Console .

* Buka file **rsyslog.conf** yang berada pada direktori **/etc**

```text
nano/etc/rsyslog.conf
```

* Disable line berikut, pastikan **backup** untuk menghindari hal-hal yang tidak diinginkan.

```text
cp /etc/rsyslog.conf /etc/rsyslog.conf.bak
```

```text
#$ModLoad imjournal 
# provides access to the systemd journal
#$IMJournalStateFile imjournal.state
#$IncludeConfig /etc/rsyslog.d/*.conf
```

* Pada line ke 40, rubah status **OmitLocalLogging** dari **on** ke **off**
* Stop rsyslogd dan hapus file imjournal.state dari direktori **/var/lib/rsyslog**

```text
$OmitLocalLogging off
```

```text
systemctl stop rsyslog.servicerm -rf /var/lib/ryslog
```

* Start service rsyslog kembali untuk memastikan service rsyslog sudah berjalan kembali

```text
systemctl start rsyslog.service
```

* Dan semua service zimbra yang berada di Zimbra Admin Console saat ini sudah hijau kembali \(Running\).

![Server Status Zimbra Admin Console](https://lh4.googleusercontent.com/vjSR7BoPoGJhu5xcWFtW0fVdFuD1994mm_8QWARmOsUZ-Akjo95QuA5eXWDonaRLGppSdYdpOHaHIZh-vdV_KWpcHALxXNbZ4We4AXGbBVaBF09uk9uSpO1ZEXXwTaYeZ-B0D5oQ)

Source: [https://rizkiana.id/mengatasi-red-x-di-zimbra-admin-console/](https://rizkiana.id/mengatasi-red-x-di-zimbra-admin-console/)

### Resolution \#2

**Jalankan perintah sebagai root**

To restart and enable cron service the permanently. 

```text
service crond restart 
chkconfig crond on
```

Opening rsyslog.conf file and uncomment the following. 

```text
nano/etc/rsyslog.conf 
```

Uncomment these two lines 

```text
$modload imupd 
$UDPServerRun514 
```

To restart and enable rsyslog service the permanently. 

```text
service rsyslog restart 
chkconfig rsyslog on 
```

To update /etc/rsyslog.conf file. 

```text
/opt/zimbra/libexec/zmsyslogsetup 
```

Login zimbra account and to run command line the following. 

```text
su - zimbra 
zmupdateauthkeys 
zmcontrol restart
```

Running the command line above zimbra ldap server, zimbra mailbox server, zimbra mta server in environment. if error then you can zimbra restart service.

Source: [https://www.huuphan.com/2016/11/zimbra-some-services-are-not-running.html](https://www.huuphan.com/2016/11/zimbra-some-services-are-not-running.html)

### Resolution \#3



