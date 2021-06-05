# playground-ansible

Ansible playbook to provision playground for PyDentity

### Requirements

* Ansible installed on local machine. You can do that via pip. Using virtualenvs is recommended.
* A running Ubuntu 20.04 machine (that you have access to) reachable over the network/on some IP.

This is an Ansible version of [these notes](https://hackmd.io/@wip-abramson/BkD06KGq_). 

Instructions to run the playbooks are located in the top comment in the playbook itself. 

Instructions are made for Ubuntu 20.04 LTS running on Linode.

All you really need to do is change the IP address in the `hosts` file to the IP of your instance. Then take the ansible command from the top comment of the playbook, possibly adjusting the path to the keyfile you want to use and you are good to go. 

You can start the notebooks by running:

```
ssh remoteuser@remotemachine 'aries-jupyter-playground/manage.sh start'
```
or if you want to go via a jumphost (e.g. the remote machine is behind a firewall/only accessible via certain machine)
```
ssh -J jumpuser@jumphost remoteuser@remotemachine 'aries-jupyter-playground/manage.sh start'
```
replace start with stop to halt the containers. Obviously, you'll have to replace remoteuser and remotehost with a username and IP address respectively that fit your needs.

In order to get the urls run
```
ssh remoteuser@remotemachine 'aries-jupyter-playground/scripts/get_URLS.sh'
```

Now we still need to establish port forwarding to the remote machine in order to access the remote notebooks. This can be done like so:

```
ssh -N -f -L localhost:localport:localhost:remoteport remoteuser@remotemachineip
```