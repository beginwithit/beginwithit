# Beginwithit



# Lesson 1

Document everything, you are going to forget it.
Thats why we are going to use this method to learn new things.

## Overview

- Windows WSL
- Unix/Linux basic commands
- VIM
- Markdown - MD
- Todo

### Windows WSL

To install WSL check: https://docs.microsoft.com/en-us/windows/wsl/install-win10

To start WSL go to Start > Ubuntu and the Terminal will open.

### Unix/Linux basic commands

The basic command to begin with are:

- ls - lists all the files in the current directory
- cd - change directory - cd ..
- touch - creates a file
- rm - remove
- history - show history of commands
- mkdir - creates/make directory
- mv - move source dest(can be used to rename dir/file)
- vi or vim - opens a file in the vim editor
- which - shows where a command is in the filesystem
- pwd - shows the location of the current dir
- man vi - manual for example vi(can be anything)

### VIM

press `I` to enter INSERT MODE to edit the text
press ESC to exit the INSERT MODE
:wq - save and exit
:q - exit

### Markdown - MD

````
# h1
## h2 .
"-" list
````

### Todo

Look up some basic commands in Linux, VIM, MD...

and SSH



 # Lesson 2

In this Lesson we will learn something about SSH, how we connect to a server and how we add a new user to a server incl. his SSH key.

## SSH - Secure Shell

Generating your own SSH key:

``ssh-keygen -t rsa -b 4096 -C "comment" ``

Under "comment" you can enter anything you want.

The SSH key is stored in ./ssh - you can check with ls -la ./ssh what is inside.

There is always one private and one public (.pub) key, we will need to transfer the .pub key to the server we want to connect to.

You can show the content of the SSH .pub key with:

``cat ./ssh/xxxx.pub``

cat means concatenate and we will use it to read data from files in Linux. This command can also show the content of multiple files at once if you add them as additional parameters.

To create a new user on a server we can use:

``useradd -m perk``

This will add the user perk on the server and create his home folder.

To give the user permissions to connect to the server add the users xxx.pub SSH key into the ~/.ssh/authorized_keys file

Example on server:

````
useradd -m perk

mkdir ~/.ssh/

vi ~/.ssh/authorized_keys

PASTE THE XXX.pub KEY IN VIM AND :wq

chmod 400 ~/.ssh/authorized_keys

chown -R perk:perk ~/.ssh
````

To connect via ssh use:

````
ssh do1.deseop.net
````

/etc/hosts - Local NS entries

/etc/resolv.conf - DNS Configuration - points where to check for DNS servers

nslookup - first checks hosts then resolv.conf(?!)

hint - Linux Unix folder structure(cd /)

top - task manager for linux

ps auxww - check



# Lesson 3

To install and setup check:

https://help.ubuntu.com/lts/serverguide/git.html

Today we will create our first rep "[beginwithit](https://github.com/perk-sh/beginwithit)" and we will push our local work to repo.

````
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/perk-sh/beginwithit.git
git push -u origin master
````


