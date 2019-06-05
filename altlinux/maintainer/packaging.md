# Packaging tutorial


## Contents

* [What is Sisyphus and Gear](#what-is-sisyphus-and-gear)
* [Package build quickstart](#package-build-quickstart)
* [The TRUE packaging way](#the-true-packaging-way)

* * *


## What is Sisyphus and Gear

The Sisyphus package is a Git repository with `.gear` service directory
which contents describe the process of building the package.

There are lots of similar repositories used by various projects like
Fedora so the appoarch described is not really unique.


## Package build quickstart

When you checked out the repository with **.spec** file you may simply
build RPM package from package root directory like:

```sh
gear-rpm -ba
```

You'll get the RPM package in `${HOME}/RPM/RPMS/<package>.rpm`.


## The TRUE packaging way

In order to build package from gearrepo you need to invoke `gear-hsh`
command just like `gear-rpm` - do it in gearrepo catalog.

