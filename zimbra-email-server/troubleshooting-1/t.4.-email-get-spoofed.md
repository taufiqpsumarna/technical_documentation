---
description: Zimbra 8.6.0_GA_1153.FOSS dengan sistem operasi Linux Centos 7
---

# T.4. Email Get Spoofed

Jika kalian pernah mendapatkan email yang tidak berasal dari orang sebenarnya / fake email seperti dibawah ini:

![Perhatikan From dan Alamat email pengirim](<../../.gitbook/assets/image (53).png>)

Jika kalian perhatikan header email, from "Rackspace.com" dan Alamat email aslinya itu tidak sesuai bukan? nah itulah yang disebut dengan email spoofing.

## Problem Cause

* **SPF (Sender Policy Framework)** domain tidak dikonfigurasi.
* **DKIM (Domain Key Identified Domain)** domain tidak dikonfigurasi.
* **DMARC (Domain Based Message Authentication Reporting And Conformance)** domain tidak dikonfigurasi.

Adapun Tujuan konfigurasi SPF, DKIM dan DMARC, adalah sebagai berikut:

**SPF** berfungsi menguraikan alamat IP valid yang disetujui untuk mengirim email untuk domain tertentu.&#x20;

**DKIM** mencegah email spoofing dikirim sebagai pesan keluar di domain. Ini dilakukan dengan memperbarui entri DNS dari domain email untuk menambahkan tanda tangan digital ke header pesan dan untuk memastikan bahwa email tidak berubah sejak email tersebut dikirim.

**DMARC** adalah otentikasi email, pelaporan dan protokol kebijakan yang menyediakan SPF dan DKIM informasi tentang domain email (keselarasan, kepatuhan, kegagalan, dll.).

## Troubleshooting

### Konfigurasi Domain

Untuk mencegah email agar tidak terkena email spoofing lakukan langkah berikut ini:

1. Lakukan Konfigurasi SPF
2. Lakukan Konfigurasi DKIM
3. Lakukan Konfigurasi DMARC

Berikut cara setting SPF, DKIM, DMARC record pada domain hosting:

{% embed url="https://www.niagahoster.co.id/kb/cara-mengaktifkan-spf-dan-dkim-di-cpanel-niagahoster" %}
Setting SPF dan DKIM Record
{% endembed %}

{% embed url="https://www.jetorbit.com/panduan/panduan-cara-menambah-dmarc-records-di-cpanel/" %}
Setting DMARC Record
{% endembed %}

### Aktifkan Fitur Sender Must Login/Anti Fake Mail

Sender must login adalah suatu metode untuk memaksa user yang hendak mengirimkan email harus login terlebih dahulu pada Zimbra mail server, selain itu juga memaksa user agar antara from dan sasl\_username sama-sama menggunakan alamat yang sama.

```
$root@mail: su - zimbra
$zimbra@mail: zmprov mcf zimbraMtaSmtpdSenderLoginMaps  proxy:ldap:/opt/zimbra/conf/ldap-slm.cf +zimbraMtaSmtpdSenderRestrictions reject_authenticated_sender_login_mismatch
$zimbra@mail: nano /opt/zimbra/conf/zmconfigd/smtpd_sender_restrictions.cf
```

Tambahkan _**reject\_sender\_login\_mismatch**_ setelah _**permit\_mynetworks**_ sehingga seperti berikut:

```
%%exact VAR:zimbraMtaSmtpdSenderRestrictions reject_authenticated_sender_login_mismatch%%
%%contains VAR:zimbraServiceEnabled cbpolicyd^ check_policy_service inet:localhost:%%zimbraCBPolicydBindPort%%%%
%%contains VAR:zimbraServiceEnabled amavis^ check_sender_access regexp:/opt/zimbra/postfix/conf/tag_as_originating.re%%
permit_mynetworks, reject_sender_login_mismatch
permit_sasl_authenticated
permit_tls_clientcerts
%%contains VAR:zimbraServiceEnabled amavis^ check_sender_access regexp:/opt/zimbra/postfix/conf/tag_as_foreign.re%%
```

Reload service postfix

```
$zimbra@mail: postfix reload
```

Jika semua sudah terkonfigurasi silahkan cek Email Deliverability dibawah ini:

[https://mxtoolbox.com/deliverability](https://mxtoolbox.com/deliverability)

## Conclusion

Pastikan untuk melakukan konfigurasi record DKIM, SPF, dan DMARC pada domain hosting, agar email tidak terkena email spoofing.

Jika masih gagal kamu bisa coba menggunakan cara dibawah ini:

{% embed url="https://wiki.zimbra.com/wiki/FromName_Spoofing" %}

[https://imanudin.com/2018/11/02/tips-block-email-spoofing-by-display-name/](https://imanudin.com/2018/11/02/tips-block-email-spoofing-by-display-name/)

Sumber:

{% embed url="https://securityboulevard.com/2020/01/email-spoofing-101-how-to-avoid-becoming-a-victim/" %}

{% embed url="https://wiki.zimbra.com/wiki/Enforcing_a_match_between_FROM_address_and_sasl_username_8.5" %}

