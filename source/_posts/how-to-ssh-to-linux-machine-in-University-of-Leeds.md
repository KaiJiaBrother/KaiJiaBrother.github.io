---
title: how to ssh to linux machine in University of Leeds
tags: University of Leeds
categories: Linux
abbrlink: cf3ac2d4
date: 2019-10-14 23:53:55
---
# Introduction

This guide will show you how to quickly and simply set up SSH so you can access the School of Computing facilities from the comfort of your own home.

Note: a basic familiarity with the command line will be required for this guide, as well as knowledge of how to use a terminal based text editor such as `vim` or `nano`.

<!-- more -->

# SSH
[SSH][1] is a protocol which allows, among other things, remote access to a machine through a command line interface. It uses a server - client architecture. Almost all modern Unix distributions (i.e. Linux and OSX) come with ``ssh`` preinstalled.

## Connecting to University Systems with ``ssh``

We will be connecting to a machine at the University called ``remote-access.leeds.ac.uk``, from there we will be able to connect to any of the Linux machines that you have access to.

To connect to the "remote-access" server using SSH type, replacing ``<your username>`` with your University username, the following:

	ssh <your username>@remote-access.leeds.ac.uk

You will be prompted to enter your password. Once you have done so you will be at a command prompt where any commands entered will be executed on the "remote-access" server. To close this or any other ``ssh`` connections type

	exit

or

	logout

or press control-d

The sole purpose of the "remote-access" server is to provide an entry point onto the University network and consequently:

1. You have almost no file storage space on the server (just under 5MB)
2. You won't be able to access your Linux files on this machine
3. The machine doesn't have any useful software installed.

The "remote-access" server should therefore be treated as a "pass-through" or stepping stone to get onto the machine you really want to use.

Now you are connected to the "remote-access" server you can ``ssh`` into any of the Linux machines on campus (provided you are authorised to use them!). The hostnames of the machines in DEC-10 are of the format ``comp-p30xx`` where xx is a two digit number between and 00-59.

You can do this by entering, after replacing _xx_ with your favourite (two digit) number:

	ssh comp-pc30xx

Please be considerate with your resource usage when other people are using the machine. You can check this by running the command ``w``, which will output something like the following:

```
 15:55:40 up 26 days,  4:25,  3 users,  load average: 0.33, 0.25, 0.17
USER     				 TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
sc15xx           :0       :0               14:59   ?xdm?   1:28m  0.17s gdm-session-wor
sc15xx           pts/0    :0               15:53    1:24   0.06s  0.01s /usr/bin/python
<your username>  pts/1    euras01hv.leeds. 15:55    0.00s  0.04s  0.00s w

```

If you see any usernames in the list other than your own then you are sharing that machine and must refrain from using an excessive amount of memory or CPU time. Most of the work you will do in your 1st year won't be intensive enough to impact other users, e.g. editing and compiling your small C programs.

# Advanced Usage

The following sections don't offer any additional functionality, but should make it slightly quicker to log in, i.e. fewer keystrokes.

## ``ssh`` configuration file

Although it is perfectly fine to connect to the remote-access server and then manually use ``ssh`` to get onto the machine you wish to use, there is a slightly nicer way of doing this. ``ssh`` uses a simple configuration text file within which you can define commonly used hosts and various settings for each of them. The configuration file is located in the ``.ssh`` directory within your home directory, i.e. ``~/.ssh/`` and is called ``config``. _Note that this is a "hidden" directory and will only appear when you run ``ls`` with the ``-a`` option!_

Open the file in your favourite text editor (mine is ``vim``) and enter the following, **replacing ``<your username>`` with your university username, e.g. ``sc15xx``**:

```
Host remote-access
	HostName remote-access.leeds.ac.uk
	Port 22
	User <your username>

```

The configuration defined a host called "remote-access" and provides the url of the server, the port to connect to (ssh default is 22) and the username of the user you wish to connect as. You can have multiple hosts defined in your config file.

To use this configuration, save the file as ``~/.ssh/config``. Then in a terminal enter:

	ssh remote-access

You will be prompted for a password. Once you have entered your password and pressed enter everything should be as it was if you had done it without using the config file.


## Setting up SSH keys

Typing in your password can become bothersome so it is nice to have a way to automate this. One way is to set up a RSA key pair. This uses public key cryptography to authenticate your login. [An RSA key has two parts, a public and private key][2]. *The private key must be kept private*; guard it with your life. First we must create a set of RSA keys. To do this enter:

	ssh-keygen -t rsa

you will be asked to provide a file name to save the key as. There is a default location provided in brackets so all you have to do is press enter. You will be prompted to enter a passphrase, i.e. a password. It's up to you whether you want to use a passphrase or not (although it is recommended). Entering a passphrase does have its benefits: the security of a key still depends on the fact that it is not visible to anyone else. Should a passphrase-protected private key fall into an unauthorized users possession, they will be unable to log in to its associated accounts until they figure out the passphrase. The only downside is that the first time you want to use the key after logging on you will have to enter the passphrase. If you choose to enter a passphrase or not press `enter` and it will generate your key. The key is located in ``~/.ssh/id_rsa``.

Now you will have to copy the public part of the key to the server. Assuming you have followed the above instructions, enter:

	ssh-copy-id remote-access

You will be presented with a notice whether this has been successful. Now that you have copied your public key to the server you will be able to login without being prompted for a password.

## Automatic SSH proxying through "remote-access" Server

The gain access to any of the machines in DEC-10 from off-campus by just entering ``ssh comp-pc30xx`` enter following hosts into your ``ssh`` config file:

```

Host remote-access
        HostName remote-access.leeds.ac.uk
        User <your username>

Host comp-pc*
        ProxyCommand  ssh remote-access nc %h %p


```

The configuration tells ssh that for any host that starts with ``comp-pc``, i.e. the machines in DEC-10, it should proxy the connection via the remote-access machine. Diagrammatically:

```
+-----+                  +---------------+                +--------------+
| you |                  | remote-access |                | comp-pc30xx  |
+-----+                  +---------------+                +--------------+
|     <============== ssh-over-netcat tunnel ==============>             |
+-----+                  +---------------+                +--------------+
```
Now you may simply enter:

	ssh comp-pc30xx

where xx is a number between 00-59 and you will have a remote shell on the specified machine!


 [1]: http://en.wikipedia.org/wiki/Secure_Shell
 [2]: https://en.wikipedia.org/wiki/RSA_(cryptosystem)
