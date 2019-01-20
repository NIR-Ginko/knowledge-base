# Working with SSH

## Contents

* [Notes](#notes)
* [Generate new key](#generate-new-key) 

* * *


## Notes

Don't avoid passwords for the key. When working with key use `ssh-agent`
and `ssh-add`.


## Generate new key

```
$ ssh-keygen -t rsa -b 4096 -C "<email>"
/usr/home/<username>/.ssh/key_<website>
```


