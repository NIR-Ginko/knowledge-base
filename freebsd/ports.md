# Working with port system

* [Python versions problem](#python-versions-problem)

* * *


## Python versions problem

As for `FreeBSD 11.2` the default Python interpreter version is 2.7.
The problem is that `python36` package is missing `sqlite3` import and
it cannot be built for Python 3.6 by default from
`/usr/ports/databases/py-sqlite3` because it tries to build it for
`Python 2.7`. All the answers I found were old and inactual.

The working solutions was to create `/etc/make.conf` and add the
following lines in order to allow port being built for the desired
interpreter version:
```
DEFAULT_VERSIONS=python=3.6
```

