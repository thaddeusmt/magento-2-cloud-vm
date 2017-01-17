# magento-2-cloud-vm

Vagrant with Ansible for Magento Cloud projects.

This is a Virtualbox Vagrant VM configured to look similar the platform.sh Magento Cloud environment.

## Get Started!

Quick run through on how to get started

1. Change local hosts file to: `10.22.22.100 {{ site_url }}` to access VM site in local browser
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
13. `$ magento-cloud get -- {{ magento_project_id }} ~/app`
14. `$ sudo mv ~/app/* /app`
15. `$ cd /app`
16. `$ composer install`
17. `$ find var vendor pub/static pub/media app/etc -type f -exec chmod g+w {} \;`
18. `$ find var vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} \;`
19. `$ chown -R :vagrant .`
20. `$ chmod u+x bin/magento`
21. `$ cd /app/bin`
22. `./magento setup:install --base-url="http://{{ site_url }}" --db-host=localhost --db-name="{{ mysql_database }}" --db-user="{{ mysql_user }}" --db-password="{{ mysql_pass }}" --admin-firstname=Magento --admin-lastname=Admin --admin-email="{{ admin_email }}" --admin-user="{{ admin_user }} --admin-password="{{ admin_password }}" --language=en_US --currency=USD --timezone=America/Los_Angeles --use-rewrites=1`
23. View you Magento install at {{ site_url }}

See here for more details on install Magento Cloud locally if you run into issues:
http://devdocs.magento.com/guides/v2.1/cloud/access-acct/set-up-env.html
