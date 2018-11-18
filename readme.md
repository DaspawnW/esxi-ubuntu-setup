# Ubuntu Setup for ESXi

This is an ansible playbook I use for my ESXi instances to have a base common setup.

It does the following things:

* Install python (required for ansible provisioning)
* Install ubuntu universe as repository
* Install some additional packages (e.g. jq)
* Disable SSH access with username and password
* Disable SSH access with root
* Disable password for ubuntu user to become root (not for production use)
* Mount second sdb device if it's present

# How to execute

Please replace the ip address listed in hosts file with the ip address of your instance.

```
[server]
192.168.178.52     ansible_connection=ssh        ansible_user=ubuntu
```

Then execute the following command:

```
ansible-playbook -i hosts -v -b -c ssh --ask-pass --ask-sudo-pass provision.yml
```

The ask-pass and ask-sudo-pass are only required for the first run, because then the sudo escalation is secured via password.