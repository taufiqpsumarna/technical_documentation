# T.3. SMTP-Amaviz: Connection Refused

## Problem Cause

* service zmamavisdctl tidak berjalan.
* kesalahan konfigurasi zmamavisdctl.
* service zmamavisdctl rusak \(stale pid\)

{% hint style="info" %}
Versi Zimbra

Zimbra 8.6.0\_GA\_1153.FOSS dengan sistem operasi Linux Centos 7

Zimbra 8.6.0\_GA\_1242
{% endhint %}

## Troubleshooting 1

1. **Cek Log Zimbra**

```text
$root@mail: tail /var/log/zimbra.log
$root@mail: 
Apr 25 11:15:09 mail postfix/smtp[13534]: connect to 127.0.0.1[127.0.0.1]: Connection refused (port 10024)
Apr 25 11:15:10 mail postfix/smtp[13534]: 4B15324914C: to=<admin@domain.co.id>, relay=none, delay=0.61, delays=0.35/0.26/0/0, dsn=4.4.1, status=deferred (connect to 127.0.0.1[127.0.0.1]: Connection refused)
Apr 25 11:15:11 mail postfix/smtp[13534]: 4B15324914C: to=<admin@domain.co.id>, relay=none, delay=0.61, delays=0.35/0.26/0/0, dsn=4.4.1, status=deferred (connect to 127.0.0.1[127.0.0.1]: Connection refused)
Apr 25 11:15:11 mail postfix/smtp[13534]: 4B15324914C: to=<admin@domain.co.id>, relay=none, delay=0.61, delays=0.35/0.26/0/0, dsn=4.4.1, status=deferred (connect to 127.0.0.1[127.0.0.1]: Connection refused)
```

_Jika ditemukan log seperti diatas, artinya email yang masuk / keluar di tolak oleh server, karena service zimbra amaviz tidak berjalan atau kesalah konfigurasi amaviz._

**2.A. Kemudian kita coba restart seluruh service zimbra.**

```text
$root@mail: su - zimbra
$root@mail: zmcontrol restart
```

_Dan jika ketika dilakukan cek service zimbra yang berjalan pada server, terdapat sebuah pemberitahuan bahwa service is not running, seperti dibawah ini._

```text
$zimbra@mail: zmcontrol status
Host mail.domain.co.id
        antispam                Running
        antivirus               Running
        dnscache                Running
        ldap                    Running
        logger                  Running
        mailbox                 Running
        mta                     Running
        opendkim                Running
        service webapp          Running
        snmp                    Running
        stats                   Running
        zimbra webapp           Running
        zimbraAdmin webapp      Running
        zimlet webapp           Running
        zmconfigd               Running
```

Tadaa service zimbra berjalan dengan normal kembali, tetapi jika tetap bermasalah 10024 : connection refused terpaksa kita mematikan service anti virus pada zimbra mail server, tujuannya adalah untuk mem bypass email agar tidak diperiksa oleh Anti Virus Zimbra. \(Tidak Di Rekomendasikan\)

**2.B. Mematikan service Anti Virus  & Anti Spam**

```text
$zimbra@mail: zmprov ms `zmhostname` -zimbraServiceEnabled amavis
$zimbra@mail: zmprov ms `zmhostname` -zimbraServiceEnabled antivirus
$zimbra@mail: zmprov ms `zmhostname` -zimbraServiceEnabled antispam
```

Kita matikan tiga service zimbra agar pengiriman dan penerimaan email berjalan dengan normal kembali.

{% hint style="info" %}
Jika kalian ingin mengaktifkan tiga service diatas gunakan command dibawah ini.

```text
$zimbra@mail: zmprov ms `zmhostname` +zimbraServiceEnabled amavis
$zimbra@mail: zmprov ms `zmhostname` +zimbraServiceEnabled antivirus
$zimbra@mail: zmprov ms `zmhostname` +zimbraServiceEnabled antispam
```
{% endhint %}

**4. Restart service zimbra**

Setelah menonaktifkan service tersebut, restart service zimbra.

```text
$zimbra@mail: zmcontrol restart
```

**5. Cek Dengan Kirim / Terima Email**

Seharusnya semua email yang _deffered_ atau tertunda, sudah kembali berjalan dengan normal.



## Troubleshooting 2

**Full Troubleshooting step**

[https://www.slideshare.net/mvcp007/zimbra-troubleshooting-mails-not-being-delivered-or-deferred-or-connection-refused  
](https://www.slideshare.net/mvcp007/zimbra-troubleshooting-mails-not-being-delivered-or-deferred-or-connection-refused
)

## Troubleshooting 3 - Update Solution:

_18 Desember 2020_ 😆

**Pre-requirerity:**

**Fix Zimbra Permission:**

Confirm that all permissions are correct on the new server: 1. As root, run the zmfixperms command to repair any potential permissions problems with files under /opt/zimbra:

```text
$root@email: /opt/zimbra/libexec/zmfixperms
```

2. If you need to check /opt/zimbra/store and /opt/zimbra/index as well, you will need to use the -extended option. This will take much longer to run - potentially several hours in large environments - so run it only if necessary. Run this command as root:

```text
$root@email: /opt/zimbra/libexec/zmfixperms -extended
```

source: [https://wiki.zimbra.com/wiki/Fix\_the\_Zimbra\_Collaboration\_Permissions](https://wiki.zimbra.com/wiki/Fix_the_Zimbra_Collaboration_Permissions)

\*\*\*\*

**Fix FQDN Hostname amavizd.conf dan amavizd.conf**

Saya menemukan forum hal ini dapat memperbaiki penyebab service AV/AS tidak berjalan karena server tidak mengenali hostname nya sendiri.

> Postby andreychek » Tue Dec 13, 2005 1:18 pm
>
> Nov 17 11:26:18 tusd-exch01 postfix/smtp\[4507\]: connect to 127.0.0.1\[127.0.0.1\]: Connection refused \(port 10024\)
>
> Nov 17 11:26:18 tusd-exch01 postfix/smtp\[4508\]: connect to 127.0.0.1\[127.0.0.1\]: Connection refused \(port 10024\)
>
> Nov 17 11:32:15 tusd-exch01 postfix/smtp\[8380\]: C326360C1C: to=, relay=none, delay=3, status=deferred \(connect to 127.0.0.1\[127.0.0.1\]: Connection refused\)\[/QUOTE\]
>
> I discovered this can happen if Amavis doesn't understand one's FQDN. I solved it by setting the $myhostname var in /opt/zimbra/conf/amavisd.conf and /opt/zimbra/conf/amavisd.conf.in, as well as myhostname in /opt/zimbra/postfix/conf/main.cf.
>
> -Eric

```text
//Gunakan user root untuk konfigurasi hostname amavisd.conf
$root@email: nano /opt/zimbra/conf/amavisd.conf

*kemudian cek apakah $myhostname telah terkonfigurasi, jika sudah lanjut langkah selanjutnya*

//Gunakan user root untuk konfigurasi hostname amavisd.conf.in
$root@email: nano /opt/zimbra/conf/amavisd.conf.in
*kemudian cek apakah $myhostname telah terkonfigurasi*

kemudian save konfigurasi
```



source: [https://forums.zimbra.org/viewtopic.php?t=31771](https://forums.zimbra.org/viewtopic.php?t=31771)

\*\*\*\*

Setelah mencoba troubleshooting kembali akhirnya masalahnya ketemu juga, penyebab utama service Anti Virus & Anti Spam tidak berjalan karena MTA Trusted network tidak terkonfigurasi dengan baik adapun error log yang didapatkan adalah sebagai berikut:

```text
$zimbra@email: tail -f /var/log/zimbra.log | grep amavis
$zimbra@email: amavis[27561]: (!!)TROUBLE in pre_loop_hook: Invalid IPv4 network mask or CIDR prefix length: [127.0.0.0/8,XX.XX.XXX.XXX/32,XX.XXX.XXX.XX/32
amavis[27561]: (!)_DIE: Suicide () TROUBLE in pre_loop_hook: Invalid IPv4 network mask or CIDR prefix length: [127.0.0.0/8,XX.XX.XXX.XXX/32
```

Setelah melihat log tersebut didapatkan kesimpulan bahwa penyebab service AV / AS tidak berjalan karena kesalahan konfigurasi pada MTA Trustednetwork _`Invalid IPv4 network mask or CIDR prefix length`_

Cara memperbaikinya adalah sebagai berikut:

```text
$root@email: su - zimbra
/// Stop Zimbra Service Terlebih Dahulu ///
$zimbra@email: zmcontrol stop
$zimbra@email: zmcontrol status
$zimbra@email: ps aux | grep zimbra
/// Pastikan Zimbra Service Telah Berhenti Sepenuhnya ///
```

Gunakan MTA Trusted Network 127.0.0.0/8, IP Publik, IP Lokal Server, edit pada webadmin console atau Zimbra Console, kemudian restart service zimbra

```text
$zimbra@email: zmprov modifyServer <mail.contoh.co.id> zimbraMtaMyNetworks '127.0.0.0/8 192.168.1.0/24 182.xx.xx.xx/29'
$zimbra@email: postfix reload
$zimbra@email: zmcontrol restart
```

Setelah melakukan restart service zimbra akhirnya server email kembali berjalan dengan normal dan dapat menerima / mengirim email seperti semula. ✌😃



## Conclusion

Kejadian seperti ini dapat terjadi disebabkan oleh update zimbra yang tidak sempurna, untuk mengatasinya kamu bisa coba clean install server email zimbra dengan update yang kamu mau.

Ternyata pada versi 8.6.0 untuk pengisian MTA Trusted Network tidak menggunakan tanda \(,\) sebagai pemisahnya melainkan menggunakan spasi \( \) hal ini yang menyebabkan mengapa MTA Trusted Network telah terkonfigurasi tetapi tidak berfungsi dan menyebabkan error.

yang terpenting sebelum clean install adalah **BACKUP** seluruh data terlebih dahulu. **DIWYOR !**

**Sumber Referensi:**

[https://forums.zimbra.org/viewtopic.php?f=15&t=56832](https://forums.zimbra.org/viewtopic.php?f=15&t=56832)

[https://forums.zimbra.org/viewtopic.php?t=31771](https://forums.zimbra.org/viewtopic.php?t=31771)

[https://forums.zimbra.org/viewtopic.php?t=4468](https://forums.zimbra.org/viewtopic.php?t=4468)

[https://forums.zimbra.org/viewtopic.php?t=15888](https://forums.zimbra.org/viewtopic.php?t=15888)

{% embed url="https://wiki.zimbra.com/wiki/How\_to\_Disable\_Zimbra%27s\_AntiSpam\_and\_AntiVirus\_filtering" %}

{% embed url="https://forums.zimbra.org/viewtopic.php?t=62009" %}



