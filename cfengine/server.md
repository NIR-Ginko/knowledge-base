# Configuring CFEngine 3 server

## Contents

* [Installation](#installation)
* [Setup keys](#setup-keys)
* [Setup executables](#setup-executables)
* [Create server configuration files](#create-server-configuration-files)
* [CFEngine Policy Hub bootstrap](#cfengine-policy-hub-bootstrap)

* * *


## Installation

Install CFEngine 3 on FreeBSD like:

```
pkg install cfengine cfengine-masterfiles
echo 'cf_serverd_enable="YES"' >> /etc/rc.conf
echo 'cf_monitord_enable="YES"' >> /etc/rc.conf
echo 'cf_execd_enable="YES"' >> /etc/rc.conf
```


## Setup keys

Run the following command from **root**:

```
cf-keys
```

to create key files **localhost.pub** and **localhost.priv** in
`/var/cfengine/ppkeys` directory.


## Setup executables

Create executable directory:

```
mkdir /var/cfengine/bin
```

and symlink the necessary files to it:

```
cd /var/cfengine/bin
ln -s /usr/local/bin/cf-agent
ln -s /usr/local/bin/cf-check
ln -s /usr/local/bin/cf-execd
ln -s /usr/local/bin/cf-key
ln -s /usr/local/bin/cf-monitord
ln -s /usr/local/bin/cf-net
ln -s /usr/local/bin/cf-promises
ln -s /usr/local/bin/cf-runagent
ln -s /usr/local/bin/cf-serverd
ln -s /usr/local/bin/cf-upgrade
```


## Create server configuration files

First, copy **CFEngine masterfiles** like:

```
cd /var/cfengine
cp -r /usr/local/share/examples/cfengine-masterfiles/masterfiles /var/cfengine/masterfiles
```


## CFEngine Policy Hub bootstrap

Run

```
cf-agent -B 192.168.8.100
```

To self-bootstap CFEngine server (also known as **Policy Hub**).
Substitute `192.168.8.100` part with your's host interface.

In order to bootsrap the server `/var/cfengine/masterfiles/promises.cf`
file must be present.

