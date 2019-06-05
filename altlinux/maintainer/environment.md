# Development environment

* [Hasher user](#hasher-user)
* [Hasher configuration](#hasher-configuration)
* [Git configuration](#git-configuration)
* [RPM configuration](#rpm-configuration)
* [Hasher initialization](#hasher-initialization)

* * *

## Hasher user

Add your user to hasher:

```
sudo /usr/sbin/hasher-useradd <user>
```

Logout and then login again to apply new groups information.


## Hasher configuration

create the `~/hasher/config` file with the following contents:

```
USER=nir
packager="`rpm --eval %packager`"
no_sisyphus_check="packager,buildhost,gpg"
apt_config="$HOME/.hasher/apt.conf
mount=/dev/pts,/proc
```


## Git configuration

Then configure Git like:

```
git config --global user.name "Igor Chudov"
git config --global user.email "nir@altlinux.org"
```


## RPM configuration

Add something like the sample below to your `~/.rpmmacros`:

```
%packager Igor Chudov <nir@altlinux.org>
%_gpg_name nir@altlinux.org
```


## Hasher initialization

Run the following commands:

```
$ mkdir ~/hasher
$ mkdir ~/.hasher
$ hsh --initroot-only ~/hasher
```

to finish the setup process.

