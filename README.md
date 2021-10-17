# rhpds-controller
This is a small repo for controlling/deploying RHPDS from Ansible CLI

You will need to update the vars.yml with your creds and run the playbook.

```$ ansible-playbook orderservice.yml -e rhpdsuser=user -e rhpdspass=pass```
