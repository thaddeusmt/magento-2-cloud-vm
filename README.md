# magento-2-cloud-vm

Vagrant with Ansible for Magento Cloud projects.

This is a VirtualBox Vagrant VM configured to look similar the platform.sh Magento Cloud environment.

It is built on Debian Jessie, with PHP 7.0, Nginx and MariaDB.

There are a lot of manual commands right now since Magento Cloud makes you do an interactive login. This might be consolidated so there is a 2nd Ansible playbook you can run after authentication that automates the rest of these steps.

Application code is in the shared local `/app` directory for easy editing in an IDE.

`{{ site_url }}`, below, should be a url like `mysite.local`, which will let you access the site in your browser.

In the `setup:install` command be sure to use the same `{{ mysql_database }}` etc that you set up in the `vars.yml` file. And set the `{{ admin_user }}` and other variables as you see fit.

## Get Started!

Quick run through on how to get started:

***Quick Note for Mac OS X Users:*** 
Make sure to install the bindfs vagrant plugin before starting. This manages the NFS user/group mapping between the guest and host, which is necessary for Magento to write to the filesystem properly. 
`vagrant plugin install vagrant-bindfs`
In the end, the application code should be owned by `vagrant:vagrant`. When ssh'd into the vm, if you see that the app code is owned by `501:dialout` or `501:2x`, something is wrong. Mostly likely the slow Magento experience will be your first clue.

1. Change local hosts file to: `10.22.22.100 {{ site_url }}` to access VM site via local browser
2. Install Vagrant and Virtualbox
3. Install Ansible locally
4. Rename `config.yml.example` to `config.yml`
5. Edit `config.yml`
6. Rename `provisioning/vars.yml.example` to `provisioning/vars.yml`
7. Edit `provisioning/vars.yml`
8. Run `vagrant up` to boot VM
9. `$ vagrant ssh` to log in to the VM
10. `$ git config --global user.name "{{ your name }}"`
11. `$ git config --global user.email {{ your e-mail address }}`
12. `$ magento-cloud auth:login`
13. `$ magento-cloud project:list` (to look up your magento_project_id)
14. `$ magento-cloud get -- {{ magento_project_id }} ~/app`
15. `$ sudo mv ~/app/* /app`
16. `$ cd /app`
17. `$ composer install`
18. `$ find var vendor pub/static pub/media app/etc -type f -exec chmod g+w {} \;`
19. `$ find var vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} \;`
20. `$ chown -R :vagrant .`
21. `$ chmod u+x bin/magento`
22. `$ cd /app/bin`
23. `./magento setup:install --base-url="http://{{ site_url }}" --db-host=localhost --db-name="{{ mysql_database }}" --db-user="{{ mysql_user }}" --db-password="{{ mysql_pass }}" --admin-firstname=Magento --admin-lastname=Admin --admin-email="{{ admin_email }}" --admin-user="{{ admin_user }}" --admin-password="{{ admin_password }}" --language=en_US --currency=USD --timezone=America/Los_Angeles --use-rewrites=1`
24. View you Magento install at {{ site_url }}

See here for more details on installing Magento Cloud locally if you run into issues:
http://devdocs.magento.com/guides/v2.1/cloud/access-acct/set-up-env.html
