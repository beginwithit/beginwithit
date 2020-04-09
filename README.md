# Begin with it

Begin with **i**nformation **t**echnology.

**Begin with it** initiated as a mentoring session between a senior IT allrounder and an IT enthusiast.

It starts with an common foundation - **Linux**. And goes up to managing your own cloud server with **Docker** and Traefik as Loadbalancer. With an outlook to **Terraform**.

This is for everybody who wants to (re-)start with infomation technology - it doesn't matter if you are coming from a Linux, Mac or Windows background.

The complete program is completely open source (as the technologies used) and free as a beer.

## Contents 

### Linux

Lesson X-X

Visual Enhancement

* starship

### Docker

Lesson X-X

### Terraform

Lesson X-X


## Lesson 1: Linux basics

Document everything, you are going to forget it.
Thats why we are going to use this method to learn new things.

### Overview

- Windows WSL
- Unix/Linux basic commands
- Vim
- Markdown (md)
- Todo

### Windows WSL

To install WSL check: https://docs.microsoft.com/en-us/windows/wsl/install-win10

To start WSL go to Start > Ubuntu and the Terminal will open.

### Unix/Linux basic commands

The basic command to begin with are:

- `ls` - lists all the files in the current directory
- `cd` - change directory - cd ..
- `touch` - creates a file
- `rm` - remove
- `history` - show history of commands
- `mkdir` - creates/make directory - can add -p to create a path if one fir doesnt exist
- `mv` - move source dest(can be used to rename dir/file)
- `vi` or `vim` - opens a file in the vim editor
- `which` - shows where a command is in the filesystem
- `pwd` - shows the location of the current dir
- `man vi` - manual for example vi(can be anything)
- run or combine more commands at once with ``;`` or ``&&`` 
- `head` outputs first few lines of a file with -n you can specify how much rows you want to see(default 10)
- `tail` outputs the last few lines of a file, can also use -n
- `cat` - concatenates files and sends them to the standard output stream

### Vim

press `I` to enter INSERT MODE to edit the text
press `ESC` to exit the INSERT MODE
`:wq` - save and exit
`:q` - exit

### Markdown (md)

````
# h1
## h2 .
"-" list
````

### Todo

Look up some basic commands in Linux, vim, Markdown, SSH etc.



## Lesson 2: Secure Shell and linux advance

In this Lesson we will learn something about SSH (Secure Shell), how we connect to a server and how we add a new user to a server incl. his SSH key.

### SSH - Secure Shell

Generating your own SSH key:

``ssh-keygen -t rsa -b 4096 -C "comment" ``

Under "comment" you can enter anything you want.

The SSH key is stored in ./ssh - you can check with ls -la ./ssh what is inside.

There is always one private and one public (.pub) key, we will need to transfer the .pub key to the server we want to connect to.

You can show the content of the SSH .pub key with:

``cat ./ssh/xxxx.pub``

`cat` means concatenate and we will use it to read data from files in Linux. This command can also show the content of multiple files at once if you add them as additional parameters.

To create a new user on a server we can use:

``useradd -m perk``

This will add the user perk on the server and create his home folder.

To give the user permissions to connect to the server add the users xxx.pub SSH key into the ~/.ssh/authorized_keys file

Example on server:

````
useradd -m perk

mkdir ~/.ssh/

vi ~/.ssh/authorized_keys

# Paste the XXX.pub key in vim and save&close (:wq)

chmod 400 ~/.ssh/authorized_keys

chown -R perk:perk ~/.ssh
````

To connect via ssh use:

````
ssh example.net
````

### Linux advance

`/etc/hosts` - Local NS entries

`/etc/resolv.conf` - DNS Configuration - points where to check for DNS servers

`nslookup` - first checks hosts then resolv.conf(?!)

Look up Linux Unix folder structure (cd /)

`top` - task manager for linux

`htop` - improved and interactive top

`ps auxww` - check



## Lesson 3: Git and GitHub

To install and setup check:

https://help.ubuntu.com/lts/serverguide/git.html

Today we will create our first repository "[beginwithit](https://github.com/fperk/beginwithit)" and we will push our local work to repo.

````
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/perk-sh/beginwithit.git
git push -u origin master
````

Save git repo and global credentials

````
git config credential.helper store
git config --global credential.helper store
````

Saves the credentials in ~/.git-credentials


Always check ``git status`` if the change is not staged for commit, you need to run ``git add filename.xx`` and after that you can commit and push the file to the repository.

More about GitHub @ https://guides.github.com/activities/hello-world/

### Linux advance

`sudo tail -f /var/log/`

`sudo tail -f /var/log/*.log`



## Lesson 4: Docker

In this Lesson we installed Docker and ran a couple of containers.

Check how to install on this Link : `https://docs.docker.com/install/`

We are using ubuntu so we used this method:

````
https://docs.docker.com/install/linux/docker-ce/ubuntu/
````

After that Docker Engine is up and ready for you to try it out. You can run a simple test with:

````
docker run -d -P --name iamfoo containous/whoami
````

Now you can run `docker ps` or `docker inspect --format '{{ .NetworkSettings.Ports }}'  iamfoo`and see which port was assigned to that container and try to open it:

````
curl example.net:32768
Hostname: def812f594ef
IP: 127.0.0.1
IP: 172.17.0.4
RemoteAddr: IPAddress:53196
GET / HTTP/1.1
Host: example.net:32768
User-Agent: curl/7.58.0
Accept: */*
````

And here we see that the test worked.

Some basic docker commands:

````
docker run - runs and/or installs container
docker stop - stops container
docker ps - shows running containers
docker ps -a - shows all installed containers
docker rm - removes a container
docker logs - shows specific containers logs
docker inspect - shows specific container config
````

Docker stores his files in `cd /var/lib/docker` but we wont touch that.

After that we ran the Ghost CMS to test that out before out next test.

````
docker run -d --name some-ghost -e url=http://localhost:3001 -p 3001:2368 ghost
````

In our case:

````
docker run -d --name ghost -e url=http://example.net -p 80:2368 ghost
````

In this case the `80:2368` means that it will use the hosts port 80 but in the container it will be 2368.

### Linux advance

`vim` - `SHIFT + G` - goes to last line

        `SHIFT + A` - goes last character in the line and enters `INSERT MODE`

`cat /etc/group` - show all groups

`sudo usermod -aG docker perk` - adds user perk to docker group

`last` - check login records

`/` - search inside `man` or `vi` - n - for next result

`users` - check which users are logged in

`tr` - translate - replaces xxx with xxx in a file

`grep` - search for "something" in a file - ie `history | grep docker`


## Lesson 5: Docker behind Traefik 

Traefik (Loadbalancer/Reverse proxy)


In this lesson we will setup Traefik which is a loadbalancer/reverse proxy, you can find more on:

https://docs.traefik.io/v2.2/

And we will use it in this project to redirect our *.domain traffic and to monitor our traffic and containers.

To run Traefik you can use:

````
docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.yml:/etc/traefik/traefik.yml \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik:v2.2
````

where it binds the ports 8080 and 80 for traefik and adds two volumes to our host. More info on:

`https://hub.docker.com/_/traefik`

However we didnt used that method because we wanted to add a acme and Auth to our Traefik.

So we added some labels and ENV variables(https://docs.traefik.io/reference/static-configuration/env/)

Our command looked like this:

````
docker run -d --name traefik \
  -p 443:443 \
  -p 80:80 \
  -e "TRAEFIK_ACCESSLOG=true" \
  -e "TRAEFIK_PROVIDERS_DOCKER=true" \
  -e "TRAEFIK_API_DASHBOARD=true" \
  -e "TRAEFIK_ENTRYPOINTS_WEB_ADDRESS=:80" \
  -e "TRAEFIK_ENTRYPOINTS_WEBSECURE_ADDRESS=:443" \
  -e "TRAEFIK_CERTIFICATESRESOLVERS_LE_ACME_EMAIL=email@email.com" \
  -e "TRAEFIK_CERTIFICATESRESOLVERS_LE_ACME_HTTPCHALLENGE_ENTRYPOINT=web" \
  -e "TRAEFIK_CERTIFICATESRESOLVERS_LE_ACME_STORAGE=/acme/acme.json" \
  -l "traefik.http.routers.api.rule=Host(\`traefik.example.net\`)" \
  -l "traefik.http.routers.api.service=api@internal" \
  -l "traefik.http.routers.api.tls=true" \
  -l "traefik.http.routers.api.tls.certresolver=le" \
  -l "traefik.http.routers.api.middlewares=auth" \
  -l 'traefik.http.middlewares.auth.basicauth.users=username:ha$hedpw' \
  -v /var/data/docker/traefik/acme/:/acme/ \
  -v /var/run/docker.sock:/var/run/docker.sock \
  traefik:v2.2
````

So up here we created a container with the following configuration:

- Name: Traefik
- Ports: 443 and 80
- Has access to other containers logs
- Uses dockers backend(daemon)
- Enabled API dashboard
- Setup Entrypoints over :80 and :443
- added a certificate resolver config and stored the data in a .json file
- setup the API access via web with a basic auth
- and setup two volumes, one for the certificate and one for the docker socket
- in the last line we specified which version we will use

After we did that, traefik was up and running and we could access the API with a working https cert.

PS. For the password we used `htpasswd -nb username password` to create a ha$h (installed with `sudo apt-get install apache2-utils`)

So as a test we ran two whoami containers one with and one without traefik to see the difference.

With traefik:

````
docker run -d --name whoami \
  -l "traefik.http.routers.whoami.rule=Host(\`w.example.net\`)" \
  -l "traefik.http.routers.whoami.tls=true" \
  -l "traefik.http.routers.whoami.tls.certresolver=le" \
  containous/whoami
````

Without traefik:

````
docker run -d --name whoami_notraefik -P \
  -l "traefik.enable=false" \
  containous/whoami
````

and we accessed both via curl to see if anything changed:

With traefik:

````
curl https://w.example.net
Hostname: e430d0d2a76e
IP: 127.0.0.1
IP: 172.17.0.3
RemoteAddr: 172.17.0.2:52016
GET / HTTP/1.1
Host: w.example.net
User-Agent: curl/7.58.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: IPAddress
X-Forwarded-Host: w.example.net
X-Forwarded-Port: 443
X-Forwarded-Proto: https
X-Forwarded-Server: 7ea8c6a488df
X-Real-Ip: IPAddress
````

Without traefik:

````
curl example.net:32768
Hostname: def812f594ef
IP: 127.0.0.1
IP: 172.17.0.4
RemoteAddr: IPAddress:53202
GET / HTTP/1.1
Host: IPAddress:32768
User-Agent: curl/7.58.0
Accept: */*
````

We can see that when we access the whoami container with traefik we get the X-Forwarded For header which is a standard header for identifying the IP address of a client connecting to a web server through an proxy or load balancer.


### Linux advance

`netstat -tulpn` - check which ports are used/listened to

`sudo cat /var/data/docker/traefik/acme/acme.json | **grep** main` same as `sudo **grep** "main" /var/data/docker/traefik/acme/acme.json`

`CTRL + X` + `CTRL + E` - edit the current command in vi

In VIM `:s/whoami/ghost/g` + `ENTER` - replace whoami in the whole vim file with ghost

`df -h` - check Filesystem

`clear` - clean terminal

`ssh -A` - bring ssh keys to another session

`ssh-add -l` - show your ssh keys



## Resources



## Todo

- [ ] create an universal git repo for servers to have a standard config which we can access fast.
  `/etc/update-mot.d/`
- [ ] create a site > gatsby or jekyll
- [ ] update motd
- [ ]  
