# platformsh-vagrant
Vagrant with Ansible for Magento Cloud projects.

This is a Virtualbox Vagrant VM configured to look like the platform.sh Magento Cloud environment.

## Get Started!

Quick run through on how to get started

Edit config.yml

$ vagrant up
$ vagrant provision
$ vagrant ssh

````
composer install
./platform-vagrant setup
````

The project will be built at PROJECT_NAME.HOSTNAME_BASE. Example: myproject.platformsh.dev.
