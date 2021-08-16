# K.2 Instalasi SSL Certificate

## Persiapan

Pastikan Vendor SSL memberikan lima file yaitu: 

1. domain.csr
2. domain.crt
3. domain.key
4. domain\_ca\_crt
5. domain\_ca.bundle

Buat folder zip seluruh file diatas, kemudian upload ke server kemudian simpan zip \(**bundle.zip**\) di folder **/tmp/**

## Langkah-langkah instalasi

**1.Ekstrak paket file sertifikat**

```
$root@mail: cd /tmp/
$root@mail tmp: unzip bundle.zip
$root@mail tmp: cd bundle
```

**2.Duplikasi file sertifikat ke /opt/zimbra/ssl/zimbra/commercial/**

```text
$root@mail bundle: cp domain.csr /opt/zimbra/ssl/zimbra/commercial/commercial.csr
$root@mail bundle: cp domain.crt /opt/zimbra/ssl/zimbra/commercial/commercial.crt
$root@mail bundle: cp domain_ca.bundle /opt/zimbra/ssl/zimbra/commercial/commercial_ca.crt
```

**3.Restart service zimbra**

```text
$root@mail: su - zimbra -c 'zmcontrol restart'
```

{% hint style="info" %}
Untuk perpanjang sertifikat SSL, cukup install domain.crt saja tanpa install domain.csr dan domain\_ca.crt
{% endhint %}

sumber:

[https://wiki.zimbra.com/wiki/Administration\_Console\_and\_CLI\_Certificate\_Tools](https://wiki.zimbra.com/wiki/Administration_Console_and_CLI_Certificate_Tools)

