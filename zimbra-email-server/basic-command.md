---
description: Zimbra 8.6.0_GA_1153.FOSS dengan sistem operasi Linux Centos 7
---

# Basic Command

## Masuk Ke Control Panel CLI Zimbra

```
root@mail: su - zimbra
```

## Zimbra Service Basic Command

```bash
# Cek Status Service Zimbra
zimbra@mail: zmcontrol status

# Stop Service Zimbra
zimbra@mail: zmcontrol stop

# Start Service Zimbra
zimbra@mail: zmcontrol start

# Cek Restart Service Zimbra
zimbra@mail: zmcontrol restart
```

{% hint style="info" %}
Shortcut Zimbra Command Sebagai Root

```bash
root@mail: su - zimbra -c 'zmcontrol <command_syntax>'
```
{% endhint %}



