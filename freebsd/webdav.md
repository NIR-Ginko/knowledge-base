# Working with WebDAV resources


## Contents

* [Installing WebDAV](#installing-webdav)
* [Mounting Yandex.Disk resource](#mounting-yandex.disk-resource)

* * *


## Installing WebDAV

The easiest way is to install this obsolete port:

```
cd /usr/ports/sysutils/fusefs-wdfs
sudo make install clean
```

You will also need to configure the `/boot/loader.conf`:

```
fusefs_load=YES
```

and load the kernel module:

```
sudo kldload fuse
```


## Mounting Yandex.Disk resource

Take Yandex.Disk mount as an example:

```
sudo mkdir /mnt/yadisk
sudo wdfs "https://webdav.yandex.ru" "/mnt/yadisk" -u "username@yandex.ru" -p password
```

