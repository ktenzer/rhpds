# RHPDS Open Environments
This is a repo for controlling/deploying RHPDS open environments from Ansible CLI.

A huge thanks to Andrew Schoenfeld who provided the RHPDS controller we are using. The source for that can be found here: [RHPDS Controller](https://github.com/redawg/rhpds-controller).

One of the issues with open environments is you can only get a cookie-cutter OCP cluster or in general cannot really deploy the environments we need on day to day basis without a lot of work. Nobody wants to spend time to deploy clusters or environments manually through AWS CLI since environments only last 7 days or up to 28 with extentions. The solution is use Ansible to get more customization and deploy exactly what you want with zero effort.

## Using provided playbooks
All playbooks simply import roles. This will allow for adding use cases and reusability. All playbooks share a vars file and you will need to update the vars.yml if you are deploying OpenShift to add pullSecret as well as your sshKey. Other parameters can be overwritten at CLI.

Variables that need to be passed in are as follows:

```rhpdsuser - your RHPDS username```

```rhpdspass - your RHPDS password```

```serviceid - serviceid for your RHPDS open environment. Only required if you are re-using existing open environment. Once you deploy an open environment you will get back the serviceid, please save that number or note it if you want to reuse the open environment```

## Examples

### Deploy a blank RHPDS AWS Open Environment
```$ ansible-playbook order-aws-oe.yml -e rhpdsuser=user -e rhpdspass=pass```

### Deploy OpenShift into a new RHPDS open environment
```$ ansible-playbook order-aws-oe-with-ocp4.yml -e rhpdsuser=user -e rhpdspass=pass```

### Deploy OpenShift into a existing RHPDS open environment
```$ ansible-playbook deploy-ocp4-with-existing-oe.yml -e rhpdsuser=user -e rhpdspass=pass -e serviceid=30000000172923```

### Destroy OpenShift Cluster
```$ ansible-playbook destroy-ocp4.yml```

## OpenShift Install Logs
OpenShift install directory will be /tmp/ocp4. Your local AWS credentials file /home/user/.aws/credentials is updated automatically.

You can follow the OCP4 cluster install by simply opening a new terminal using tail.
```$ tail -f /tmp/ocp4/.openshift_install.log```
