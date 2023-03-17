---
title: Connection through SSH
parent: Computing
---


# Connection through SSH

The `ssh` command is a very useful tool to connect to other computers when working in
the terminal in Ubuntu. We summarise a few useful aspects here.


## The main command

The normal use of the `ssh` command is simple and looks as follows:

```bash
# SYNTAX: ssh [-p <port>] [<username>@]host [-v]

# connect to computer 'tn1.uhn' as user 'test_user'
ssh test_user@tn1.uhn
```


## The ssh configuration file

In order to shorten the `ssh` command, it is advised to create a configuration file
in which all options of the call to `ssh` are defined **per connection**. The file must
be stored in `${HOME}/.ssh/config` and can look like this:

```bash
# Configuration for hosts 'tn3.uhn' and 'tn4.uhn'
Host tn3.uhn tn4.uhn
    User    test_user
    Port    22
    IdentityFile    ~/.ssh/id_rsa

# Configuration for host tn1.uhn
Host tn1.uhn
    User    test_user_2
    Port    8022
    IdentityFile    ~/.ssh/id_rsa_test_user_2

# ...
```


## The ssh public / private key pair

When connecting to another computer via `ssh`, the user needs to authenticate themselves.
While it is possible to define a password that is send to the host computer for authentication,
it is advised to use a pair of **personal** identification keys. These keys come in pairs whereby
one is **private** and remains locally on the computer where the user created it, while the other
is **public** and needs to be distributed to other computers (or webservices like github) for
authentication purposes. The central idea is that encryption with one of the two keys can only
be decrypted with the respective other. This relationship allows for digital authentication in
many ways.

In order to create an ssh-key pair, execute the following command. Note, that it is **strongly**
recommended to use a password for the key.
```bash
sshkeygen

# When prompted,
# 1. specify the path where the keys will be stored
# 2. provide a self-chosen password
```
The keys should be stored in `${HOME}/.ssh/`. Be careful not to overwrite existing key pairs
when re-executing `sshkeygen`. The default location suggested by `sshkeygen` (accept by pressing 'enter')
works well and results in

 * the public key at `${HOME}/.ssh/id_rsa.pub`,
 * the private key at `${HOME}/.ssh/id_rsa`.

Remember to not share or move the private key file. Even the permissions are crucial
and should not be modified.


## The authorized keys file

When connecting to a host computer with ssh-key authentication, it needs to be assured
that one's own public key is available in the file `${HOME}/.ssh/authorized_keys` on the
host computer. This can be done by copying the **content** of the public key file to
the `authorized_keys` in the home folder on the host system. Note that the file permissions
need to be set in a particular way (google it or check for other users' examples). If the
public key is not listed in the `authorized_keys` file or the file permissions of the latter
are not as expected, the `ssh` command will terminate and comment by `permission denied`.
