# Starter Drupal environment

The purpose of this Drupal web application is to provide an easy to modify and
deploy starter environment.


## Getting Started

### File Updates

* composer.json - (update Name, Description, Keywords, Authors)
* vagrant-config.yml - (copy default and update cpus, memory, and host IP)
* docker-variables.yml - (copy default and update AWS S3 information)
* manifest-variables.dev.yml - (copy default and update Name, Host, and Description)
* manifest-variables.prod.yml - (copy default and update Name, Host, and Description)

* scripts/cg-init.sh - (update APP_DEFAULT_NAME)
* scripts/cg-push.sh - (update APP_DEFAULT_NAME)
* scripts/cg-destroy.sh - (update APP_DEFAULT_NAME)

* private/hash_salt.txt - (update the random hash salt string)


### Development Environment

This Drupal site runs in a two container Docker environment maintained through
Docker Compose.  There are two containers; a PostgreSQL server and an Apache / PHP
Drupal web server, with a shared volume for the root project directory.

If you already have Docker Compose running locally on your machine, you can just
run the docker-compose process locally.  If you do not have Docker or prefer to
work in virtualized development environments, this repository comes with a
Vagrantfile that will build a Virtualbox virtual machine that automatically
spins up the proper containers and exposes the right ports to the host operating
system.


---
#### Vagrant Environment

1. **Virtualbox** - Install Virtualbox from: https://www.virtualbox.org/wiki/Downloads

2. **Vagrant** - Install Vagrant from: https://www.vagrantup.com/downloads.html

When using Vagrant, when SSHing into the virtual machine will automatically redirect
you to the project root directory (/var/www).  Docker, Docker Compose, Drush, Drupal
Console, PSQL Client, and PHP Composer come installed on the Vagrant virtual
environment initially.

When the Vagrant machine is first created all Docker containers specified in the
docker-compose configuration are created and started so the website will be viewable
at **localhost:8080**.

**To get started**

```bash
$ cd {project directory}
$ git submodule update --init --recursive
$ vagrant up
$ vagrant ssh
```
 
You are now in the shared project directory: **/var/www**

* **/var/www/web** live at **localhost:8080**
* First user: **admin**
* Password:   **admin987** (__please change!__)


---
#### Docker Environment

1. **Docker** - Install Docker from: https://www.docker.com/community-edition

2. **Docker Compose** - Install Docker Compose from: https://docs.docker.com/compose/install

Since this Drupal site is built on Docker, you can run the site directly from
your local Docker instance (provided you have Docker Compose installed).

If running within DOcker locally it is important to run **scripts/docker-compose.sh**
before running **docker-compose up** because it generates the final **docker-compose.yml**
file based on a separate variables list; **docker-variables.yml**.  The included
Vagrantfile runs this script automatically before calling docker-compose.

**To get started**

```bash
$ cd {project directory}
$ git submodule update --init --recursive
$ ./scripts/docker-compose.sh
$ docker-compose up -d
$ docker exec -it www_drupal-web_1 /bin/bash (__SSH into a running container__)
```

You are now within the shared project directory: **/var/www/web**
 
* **/var/www/web** live at **localhost:8080**
* First user: **admin**
* Password:   **admin987** (__please change!__)


---
### Common Operations



## Scope

Right now to keep things very simple for a MVP this serves {num} basic functions:




## Architecture

This is a PHP web platform built on Drupal 8.  Drupal was chosen because it
provides an easy means of exploring and editing things, such as what data
fields might be tracked over time or managing access without requiring software
updates and deployments.

Since this is a prototype and meant to be a starting point, there has been
little focus on creating custom modules or themes.  If this proves a useful
tool then that can be improved over time.

This portal is built for deployment to https://cloud.gov.  See INSTALL.md for
more information about how to install yourself into cloud.gov or Cloud Foundry.
