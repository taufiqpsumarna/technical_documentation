# K.4 Anti-Spam / Fake Email

### A.\) Sender Must Login/Anti Fake Mail

Sender must login adalah suatu metode untuk memaksa user yang hendak mengirimkan email harus login terlebih dahulu pada Zimbra mail server, selain itu juga memaksa user agar antara from dan _**sasl\_username**_ sama-sama menggunakan alamat yang sama.

**Apa efek apabila sender must login tidak dipasang?**  
Jika ada salah satu user pada Zimbra mail server passwordnya terkena hack/compromise, by default Zimbra mail server akan mengijinkan identitas from address berbeda dengan user yang berada pada smtp autentikasi yang digunakan. Berikut adalah contoh log-nya :

```text
zimbra1 postfix/smtpd[29431]: B28914D5978: client=xxxxx.server.com[w.x.y.z], sasl_method=LOGIN, sasl_username=user
zimbra1 postfix/cleanup[5522]: B28914D5978: message-id=<20090420154255.B28914D5978@zimbraserver.com>
zimbra1 postfix/qmgr[20690]: B28914D5978: from=<spam@spam.com>, size=6026, nrcpt=10 (queue active)
zimbra1 postfix/cleanup[3983]: 2BA56465D28: message-id=<20090420154255.B28914D5978@zimbraserver.com>
```

```text
su - zimbra2.zmprov mcf zimbraMtaSmtpdSenderLoginMaps  proxy:ldap:/opt/zimbra/conf/ldap-slm.cf +zimbraMtaSmtpdSenderRestrictions reject_authenticated_sender_login_mismatch3
nano /opt/zimbra/conf/zmconfigd/smtpd_sender_restrictions.cf
```

Tambahkan _**reject\_sender\_login\_mismatch**_ setelah _**permit\_mynetworks**_ sehingga seperti berikut :

```text
permit_mynetworks, reject_sender_login_mismatch
```

Simpan dan tunggu beberapa menit untuk Zimbra melakukan apply konfigurasi yang baru saja dilakukan. Jika tidak mau menunggu, dapat lakukan manual restart service postfix 

```text
postfix reload
```

Berikut adalah contoh log setelah melakukan improvement tersebut :

```text
Sep  7 09:21:07 mail postfix/smtps/smtpd[16910]: NOQUEUE: reject: RCPT from unknown[192.168.26.2]: 553 5.7.1 <spam@spam.com>: Sender address rejected: not owned by user admin@xxxxxxx; from=
```

Maksud dari log diatas adalah user admin hendak mengirimkan email, namun pada bagian from diubah menjadi alamat email spam@spam.com dan ditolak oleh Zimbra mail server.

{% hint style="info" %}
Setelah konfigurasi ini dijalankan username dan email pada server wajib sama dan tidak boleh ada perbedaan. \(ex: taufiq.permana = taufiq.permana@domain.com
{% endhint %}



source: [https://imanudin.com/2014/09/08/tips-improvement-anti-spam-zimbra-sender-must-loginanti-fake-mail-pada-zimbra-8-5/](https://imanudin.com/2014/09/08/tips-improvement-anti-spam-zimbra-sender-must-loginanti-fake-mail-pada-zimbra-8-5/)

### B.\) Rejecting false "mail from" addresses

By default **any connection** made to ZCS postfix and declares "mail from: local sender" \(even if it is not\) - the connection/email is accepted for local delivery. This wiki provides steps to block such connections. Once following is configured, postfix will accept "mail from: local sender" _**only if the connection made from a hosts in "mynetworks" OR the sender is sasl authenticated.**_

{% hint style="info" %}
MTA Trusted Network dan Sender Must Login Harus Harus Dikonfigurasi Terlebih Dahulu.
{% endhint %}

Modify "smtpd\_sender\_restrictions". We are adding a check before allowing a normal smtp connection. Allowing hosts in mynetwork, then allowing sasl authenticated too. Then a check for local domain address. If its true - the connection will be rejected.

```text
su - zimbra
zmprov mcf zimbraMtaSmtpdRejectUnlistedRecipient yes
zmprov mcf zimbraMtaSmtpdRejectUnlistedSender yes
zmmtactl restart
zmconfigdctl restart
```



source: [https://wiki.zimbra.com/wiki/Rejecting\_false\_%22mail\_from%22\_addresses](https://wiki.zimbra.com/wiki/Rejecting_false_%22mail_from%22_addresses)

### C.\) Limitasi Maximum Recipients

Salah satu ciri-ciri email spam adalah mengirimkan email dengan jumlah recipients yang cukup banyak. Bisa sampai lebih dari 100 recipients dalam 1 email. Untuk mengatasi hal ini terjadi, seorang admin harus melakukan Limitasi Maximum Recipients Zimbra.

Pada defaultnya, zimbra mengizinkan email dengan jumlah penerima **sebanyak 1.000.** 

Berikut adalah cara untuk melakukan Limitasi Maximum Recipients Zimbra, Jalankan perintah berikut pada server yang terinstall service mta.

```text
su - zimbra
///jumlah limitasi sebanyak 32 penerima dalam satu email///
postconf -e smtpd_recipient_limit=32
postfix reload
```

source: [https://www.ilmuzimbra.com/tips-limitasi-maximum-recipients-zimbra/](https://www.ilmuzimbra.com/tips-limitasi-maximum-recipients-zimbra/)

### D.\) Konfigurasi DNS Lookup dan Reverse Lookup

Konfigurasi Enable DNS Lookups

![Enable DNS Lookup](../../.gitbook/assets/image%20%2816%29.png)

Konfigurasi Enable Reverse DNS Lookup / Reverse DNS

```text
su - zimbra
zmprov mcf +zimbraMtaRestriction "reject_unknown_client_hostname"
zmprov mcf +zimbraMtaRestriction "reject_unknown_sender_domain"
```

