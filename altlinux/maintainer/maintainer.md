# Maintainer quickstart

* [Packages](packages.md)
* [Development environment](environment.md)
* [Packaging tutorial](packaging.md)

* * *

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


