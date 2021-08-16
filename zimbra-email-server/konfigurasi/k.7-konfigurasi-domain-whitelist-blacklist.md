# K.7 Konfigurasi Domain Whitelist / Blacklist

Pada halaman ini kita akan melakukan konfigurasi domain Whitelist / Blacklist, tujuannya adalah untuk mengizinkan atau memblokir email masuk dan keluar dari suatu domain.

{% hint style="info" %}
**Whitelist** sendiri artinya memperbolehkan atau mem-bypass dari seluruh filtering, baik email tersebut spam ataupun bukan spam.  **Blacklist** artinya melakukan penolakan email yang berasal dari email sender atau domain.
{% endhint %}

Pada versi 8.5 dan versi-versi seterusnya, ada perubahan pada tata letak konfigurasi. Pada versi ini konfigurasi dipindah ke **/opt/zimbra/data/spamassassin/localrules**

```text
su - zimbra
nano /opt/zimbra/data/spamassasin/localrules/sauser.cf
```

Buat file baru dengan nama **sauser.cf** pada directory tersebut dan isi file dengan format seperti berikut.

```text
//Contoh Format

blacklist_from sales@traveloforange.com
whitelist_from bill@yahoo.net
blacklist_from *@emn-mysavingsnow.net
```

Jika sudah, restart service amavisd dengan menggunakan user **zimbra**.

```text
zmamavisdctl restart
```

source: [https://www.ilmuzimbra.com/tips-blacklists-dan-whitelists-zimbra/](https://www.ilmuzimbra.com/tips-blacklists-dan-whitelists-zimbra/)

