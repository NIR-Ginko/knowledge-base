# OS configuration

* [Problem](#problem)
* [Solution](#solution)

* * *


## Problem

`sudo` is not configured for the default user despite the fact it is
installed by default. WTF?!


## Solution

Configure `sudo` like:
```
$ su
# vim /etc/sudoers
```
and add the following line at the end of file:
```
<username> ALL=(ALL) NOPASSWD: ALL
```

