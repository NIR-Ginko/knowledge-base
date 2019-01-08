# ALT Linux notes

* [Installer bootstrap](#installer-bootstrap)
* [Bootloader installation](#bootloader-installation)
* [OS configuration](#os-configuration)
* [Maintainer quickstart](#maintainer-quickstart)
  * [Packages](#packages)
  * [Environment configuration](#environment-configuration)
    * [Hasher user](#hasher-user)
    * [Hasher configuration](#hasher-configuration)
    * [Git configuration](#git-configuration)
    * [RPM configuration](#rpm-configuration)
    * [Hasher initialization](#hasher-initialization)
* [Packaging tutorial](#packaging-tutorial)

* * *


## Installer bootstrap

I've experienced problems with starting installer in BHyVe. This is
the only OS which has such kind of problems.

**Problem**:

Installer fails to start Xorg because it can't automatically configure
the appropriate driver.

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


## Bootloader installation

There is also a problem with installing boot loader because ALT Linux
is unable to correctly install EFI boot loader in auto-partitioning
mode so it will boot only in case rescue CD is used.

**Problem**

The problem is ALT Linux installs its UEFI boot loader into
```
FS0:\EFI\altlinux
```
but it does not check if
```
FS0:\EFI\boot
```
is present at all.

The solution is pretty simple:
```
FS0:\
cp EFI\altlinux EFI\boot
cp EFI\boot\grubx64.efi EFI\boot\bootx64.efi
```

The main point of frustration that such a simple part of installation
process has not been done yet.


## OS configuration

`sudo` is not configured for the default user despite the fact it is
installed by default. WTF?!

Configure `sudo` like:
```
$ su
# vim /etc/sudoers
```
and add the following line at the end of file:
```
<username> ALL=(ALL) NOPASSWD: ALL
```


## Maintainer quickstart


### Packages

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


### Environment configuration


#### Hasher user

Add your user to hasher:

```
$ sudo /usr/sbin/hasher-useradd <user>
```

Logout and then login again to apply new groups information.


#### Hasher configuration

create the `~/hasher/config` file with the following contents:

```
USER=nir
packager="`rpm --eval %packager`"
no_sisyphus_check="packager,buildhost,gpg"
apt_config="$HOME/.hasher/apt.conf
mount=/dev/pts,/proc
```


#### Git configuration

Then configure Git like:

```
git config --global user.name "Igor NIR Chudov"
git config --global user.email "nir@sarfsc.ru"
```


#### RPM configuration

Add something like the sample below to your `~/.rpmmacros`:

```
%packager Igor NIR Chudov <nir@sarfsc.ru>
```


#### Hasher initialization

Run the following commands:

```
$ mkdir ~/hasher
$ mkdir ~/.hasher
$ hsh --initroot-only ~/hasher
```

to finish the setup process.


## Packaging tutorial

The Sisyphus package is a Git repository with `.gear` service directory
which contents describe the process of building the package.


