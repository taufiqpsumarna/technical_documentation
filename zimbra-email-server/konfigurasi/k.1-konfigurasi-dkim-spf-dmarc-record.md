---
description: >-
  Salah satu upaya dalam menangani spam atau fake email yang dikirim dari email
  server, maka kita harus konfigurasi DKIM, SPF, DMARC Record pada domain server
  yang kita miliki.
---

# K.1 Konfigurasi DKIM,SPF,DMARC Record

## A.Pendahuluan

**SPF\(Sender Policy Framework\),** adalah sistem validasi email yg didisain untuk mencegah spam dengan cara mendeteksi spoofing, dengan mem-verifikasi alamat IP pengirim. Dengan SPF kita bisa tahu bahwa sebuah email terkirim dari sebuah alamat IP \(email server\) yang memang diijinkan untuk mengirim email tsb dari domain si sender.

_Setiap email terkirim yg bukan dari list tsb di atas, bisa dipastikan palsu atau spoofed_

![SPF \(Sender Policy Framework\)](../../.gitbook/assets/image%20%2841%29.png)

**DKIM \(DomainKeys Identified Mail\)** adalah cara agar mail server tujuan bisa memverifikasi apakah ini email yang valid yang berasal dari nama domain tertentu. Jadi fungsinya mencegah spoofing dan phishing email. Dan sama dengan SPF ini nanti dipasangkan pada DNS record untuk nama domainnya.

_DKIM menggunakan pasangan kunci private/publik untuk men“sign” semua email keluar secara otomatis._

![DKIM \(DomainKeys Identified Mai\)](../../.gitbook/assets/image%20%2847%29.png)

### 1.\) Membuat DKIM Record

Untuk membuat DKIM hanya bisa dilakukan menggunakan command line. Jalankan perintah berikut dengan menggunakan user **zimbra**. Jika zimba dibangun multiserver, maka perintah ini dijalankan pada server yang terdapat service MTA.

```text
$zimbra@email: /opt/zimbra/libexec/zmdkimkeyutil -a -d contoh.co.id
```

### 2.\) Membuat SPF Record



Source:

{% embed url="https://www.ilmuzimbra.com/memahami-domainkeys-identified-mail-dkim/" %}

{% embed url="https://www.ilmuzimbra.com/memahami-sender-policy-framework-spf/" %}

{% embed url="https://www.ilmuzimbra.com/membuat-dan-validasi-dkim-zimbra-pada-dns/" %}

{% embed url="https://www.ilmuzimbra.com/tips-zimbra-membuat-dan-validasi-spf-pada-dns/" %}

{% embed url="https://wiki.zimbra.com/wiki/Best\_Practices\_on\_Email\_Protection:\_SPF,\_DKIM\_and\_DMARC" %}



