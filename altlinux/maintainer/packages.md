# Packages

Ookay. By default ALT Linux is incapable of finding the necessary packages
so we have to push it a bit so it'll work:

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo shutdown -r now
```

and after reboot:

```
$ sudo apt-get install git \
	gear \
	hasher \
	hasher-priv \
	hasher-rich-chroot \
	hasher-rich-chroot-user-utils \
	build-environment \
	rpm-utils \
	rpm-build \
	rpm-build-licenses
```

