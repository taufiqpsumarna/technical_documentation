# Auto Update dan Reboot

Silahkan buat script baru pada Mikrotik, kemudian gunakan script dibawah ini

**Script Auto Reboot**

```text
/system reboot
```

**Script Auto Update**

```text
/system package update
check-for-updates once
:delay 5s;
:if ( [get status] = "New version is available") do={ install }
```

Setelah script dibuat, konfigurasi Scheduler pada mikrotik untuk memanggil script tersebut sesuaikan interval waktu yang dibutuhkan

