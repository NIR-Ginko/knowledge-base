# Installer bootstrap

* [Problem](#problem)
* [Solution](#solution)

* * *


## Problem

Installer fails to start Xorg because it can't automatically configure
the appropriate driver.


## Solution

Simple steps to get it up and running:
```
Xorg -configure
vi /xorg.conf.new
```
change the video driver from "vesa" to "fbdev".
```
mv /xorg.conf.new /etc/X11/xorg.conf
/usr/sbin/install2
```

