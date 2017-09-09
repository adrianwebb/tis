# Starter Drupal environment

The purpose of this Drupal web application is to provide an easy to modify and
deploy starter environment.

Update:

* composer.json - (update Name, Description, Keywords, Authors)
* vagrant-config.yml - (copy default and update cpus, memory, and host IP)
* docker-variables.yml - (copy default and update AWS S3 information)
* manifest-variables.dev.yml - (copy default and update Name, Host, and Description)
* manifest-variables.prod.yml - (copy default and update Name, Host, and Description)

* scripts/cg-init.sh - (update APP_DEFAULT_NAME)
* scripts/cg-push.sh - (update APP_DEFAULT_NAME)
* scripts/cg-destroy.sh - (update APP_DEFAULT_NAME)


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
