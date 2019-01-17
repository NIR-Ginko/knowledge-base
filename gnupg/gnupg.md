# Working with GNU Privacy Guard 2

## Contents

* [Key generation](#key-generation)
* [Key deletion](#delete-key)
* [Mutt and Neomutt integration problems](#mutt-and-neomutt-integration-problems)
* [Add emails to the key](#add-emails-to-the-key)
* [Signing your commits in Git and GitHub](#signing-your-commits-in-git-and-github)
* [Configuring Git to sign your commits](#configuring-git-to-sign-your-commits)
* [Torubleshooting guide](#troubleshooting-guide)


* * *


## Key generation

```
gpg2 --full-generate-key
```


## Key deletion

```
gpg2 --list-secret-keys
gpg2 --delete-secret-key <key_id>
gpg2 --list-key
gpg2 --delete-key <key_id>
```


## Mutt and Neomutt integration problems

In order for Mutt/Neomutt to work you need to set to configure your
`~/.gnupg/gpg.conf`:

```
pinentry-mode loopback
```

but you won't be able to perform ordinary operations with your keys
unless you delete this option. For example, you won't be able to delete
the key.


## Add emails to the key

You may have multiple emails but be lazy enough to create additional
keys for this purpose. You may add extra emails to the existing key.
The emails are called **identities**:

```
gpg2 --list-keys
gpg2 --edit-key <key_id>
adduid
save
```

The `adduid` command called from **GNUPG** shell will allow you to add
extra emails.


## Signing your commits in Git and GitHub

So, you have your awesome and very cryptic key and you want to sign the
Git commit you've made. Let's get the key ID:

```
gpg2 --list-secret-keys --keyid-format LONG
```

You'll get a list of keys. The key ID is the line with `sec` statement
looking like:

```
sec rsa4096/<key_id> 2019-01-01 [expires: 2019-01-02]
```

Copy the `<key_id>` part and use it like:

```
gpg2 --armor --export <key_id> > somefile.asc
```

The key is really long so it's worth to pipe it into the `somefile.asc`.
Now you may go to the GitHub to the **Settings** page, select
**SSH and GPG keys** element from the list on the left, press the
**New GPG key** button under **GPG keys** section and paste the
`somefile.asc` contents into the text field.


## Configuring Git to sign your commits

Get the public key ID using command:

```
gpg2 --list-keys --keyid-format LONG
```

The line with public key ID will look like:

```
pub rsa4096/<key_id> 2019-01-01
```

Get the key ID and configure Git to use the desired key like:

```
git config --global gpg.program gpg2
git config --global user.signkey <key_id>
```

To automatically sign the commits from now on you should configure the
additional Git property:

```
git config --global commit.gpgsign true
```


## Troubleshooting guide

I had problems signing Git commits at first. To debug the Git command
invoke it like:

```
env GIT_TRACE=1 git commit -S
```

It said:

```
gpg: skipped <username>: No secret key
[GNUPG:] INV_SGNR 9 Igor NIR Chudov <nir@nir.org.ru>
[GNUPG:] FAILURE sign 17
```

It turned out that the name (uid) specified it the key was not matching
with Git global property `user.name`. I adjusted the `user.name`
property (because it's easier) and everything started to work just fine.


