# Team Integration System prototype

This is a VERY early experiment into a functional TIS prototype.


## Getting Started

### File Updates

* **composer.json** - (_update Authors_)
* **vagrant-config.yml** - (_copy default and update cpus, memory, and host IP_)
* **docker-variables.yml** - (_copy default and update AWS S3 information_)
* **manifest-variables.dev.yml** - (_copy default and update Name, Host, and Description_)
* **manifest-variables.prod.yml** - (_copy default and update Name, Host, and Description_)


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

When using Vagrant, when SSHing into the virtual machine, you will automatically redirect
you to the project root directory (**/var/www**).  Docker, Docker Compose, Drush, Drupal
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
* Password:   **admin987** (_please change!_)


---
#### Docker Environment

1. **Docker** - Install Docker from: https://www.docker.com/community-edition

2. **Docker Compose** - Install Docker Compose from: https://docs.docker.com/compose/install

Since this Drupal site is built on Docker, you can run the site directly from
your local Docker instance (_provided you have Docker Compose installed_).

If running within Docker locally it is important to run **scripts/docker-compose.sh**
before running **docker-compose up** because it generates the final **docker-compose.yml**
file based on a separate variables list; **docker-variables.yml**.  The included
Vagrantfile runs this script automatically before calling docker-compose.

**To get started**

```bash
$ cd {project directory}
$ git submodule update --init --recursive
$ ./scripts/docker-compose.sh
$ docker-compose up -d
$ docker exec -it www_drupal-web_1 /bin/bash   # SSH into a running container
```

You are now within the shared project directory: **/var/www/web**

* **/var/www/web** live at **localhost:8080**
* First user: **admin**
* Password:   **admin987** (_please change!_)


---
### Common Operations

#### Vagrant Controls

* Run from the **host** machine
* Run from the **/var/www** directory

```bash
$ vagrant status       # Check the status of the virtual machine

$ vagrant up           # Create a new or run an existing virtual machine
$ vagrant provision    # Re-provision development environment from specs in Vagrantfile
$ vagrant ssh          # SSH into a running virtual machine

$ vagrant halt         # Stop and save an existing virtual machine
$ vagrant destroy      # Completely destroy an existing virtual machine
```

More on the [vagrant commands](https://www.vagrantup.com/docs/cli/)


#### Docker Controls

* Run on either the **vagrant** or **host** machine (_if installed and used_)
* Run from the **/var/www** directory

```bash
$ docker ps -a                           # List all of the containers on the virtual machine

$ docker logs www_drupal-web_1           # Display recent log entries from the www_drupal-web_1 container
$ docker logs www_drupal-web_1 --follow  # Follow log entries from the www_drupal-web_1 container

$ docker exec -it www_drupal-web_1 bash  # SSH into the running www_drupal-web_1 container

$ docker-compose up -d                   # Create and run all site containers in the background
$ docker-compose build                   # Rebuild all docker images in the docker-compose file
```

More on the [docker commands](https://docs.docker.com/engine/reference/commandline/cli/)


#### Site Configuration Management

* Run from the Drupal web **docker** container
* Run from the **/var/www/web** directory

```bash
$ drush cex   # Export site configurations to top level **config** directory
$ drush cim   # Import site configurations from top level **config** directory
```


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
