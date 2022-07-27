# K.5 Konfigurasi PolicyD Zimbra

PolicyD merupakan salah satu fitur untuk pencegahan spam pada zimbra. Namun secara default, PolicyD tidak otomatis di install ketika instalasi zimbra. Untuk itu harus manual untuk mengaktifkannya. PolicyD ini salah satu fitur untuk menjaga reputasi Ip Mail server selalu baik.

Policyd ini berbasis web based untuk konfigurasinya, secara default tidak ada tampilan login dan password. Sehingga harus dibuatkan secara manual.

### Step 1: To active cbpolicyd on zimbra 8.6

> $su - zimbra\
> $zmprov ms \`zmhostname\` +zimbraServiceInstalled cbpolicyd +zimbraServiceEnabled cbpolicyd

{% hint style="info" %}
Untuk menonaktifkan gunakan command berikut ini:

zmprov ms `zmhostname` -zimbraServiceInstalled cbpolicyd -zimbraServiceEnabled cbpolicyd

zmcontrol restart
{% endhint %}

### Step 2: To acctive cbpolicyd webui

> cd /opt/zimbra/httpd/htdocs/ && ln -s ../../cbpolicyd/share/webui\
> vim /opt/zimbra/cbpolicyd/share/webui/includes/config.php

To add "**$DB\_DSN="sqlite:/opt/zimbra/data/cbpolicyd/db/cbpolicyd.sqlitedb**";" in config.php file.\
**The ouput:**\


```

<?php

# mysql:host=xx;dbname=yyy
#
# pgsql:host=xx;dbname=yyy
#
# sqlite:////full/unix/path/to/file.db?mode=0666
#
$DB_DSN="mysql:host=localhost;dbname=cluebringer";
$DB_DSN="sqlite:/opt/zimbra/data/cbpolicyd/db/cbpolicyd.sqlitedb";
$DB_USER="root";
#$DB_PASS="";
$DB_TABLE_PREFIX="";


#
# THE BELOW SECTION IS UNSUPPORTED AND MEANT FOR THE ORIGINAL SPONSOR OF V2
#

$DB_POSTFIX_DSN="mysql:host=localhost;dbname=postfix";
$DB_POSTFIX_USER="root";
$DB_POSTFIX_PASS="";

?>


```

### Step 3: To restart services

> su - zimbra -c "zmcontrol restart"\
> su - zimbra -c "zmapachectl restart"
>
> or
>
> `su - zimbra -c "zmcontrol restart" && su - zimbra -c "zmapachectl restart"`

### Step 4: To access cbpolicyd webui.

> http://IP-OF-Zimbra:7780/webui/index.php

Source:

[https://www.huuphan.com/2017/02/how-to-install-cbpolicyd-on-zimbra-86.html](https://www.huuphan.com/2017/02/how-to-install-cbpolicyd-on-zimbra-86.html)
