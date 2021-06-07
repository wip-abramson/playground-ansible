# playground-ansible

Ansible playbook to provision playground for the [aries-juypter-playground](https://github.com/wip-abramson/aries-jupyter-playground). Currently configured for the Hyperledger Global Forum demo.

### Requirements

* Ansible installed on local machine. You can do that via pip. Using virtualenvs is recommended.
* A running Ubuntu 20.04 machine (that you have access to) reachable over the network/on some IP.

This is an Ansible version of [these notes](https://hackmd.io/@wip-abramson/BkD06KGq_). 

Instructions to run the playbooks are located in the top comment in the playbook itself. 

Instructions are made for Ubuntu 20.04 LTS running on Linode.

All you really need to do is change the IP address in the `hosts` file to the IP of your instance. 

Then take the ansible command from the top comment of the playbook, possibly adjusting the path to the keyfile you want to use and you are good to go. 

## SSH into Machine

### Add key to ssh-agent

```bash=
eval `ssh-agent`
```

```bash=
ssh-add /path/to/vm_ssh_key
```

```bash=
ssh pydentity@remotemachine
```

## Configure Agent


```bash
cd aries-jupyter-playground

```

Use vim to edit demo-participant environment file. Change:
* ACAPY_LABEL to some label you want your agent to identify itself with
* ACAPY_ENDPOINT to the remotemachines IP address and agent port. e.g. http://someipaddress:3020. Demo participant agent uses 3020

```bash
vi playground/demo-participant/.env
```

## Start Notebooks

You can start the demo-participant agent by running:

```
./manage.sh production &'
```


Note: You can also use `./manage start` to spin up two agents and use ngrok. This is useful for testing an interaction flow you are developing. The ultimate aim is that you can interact with other HGF attendees running their own agent on their own machine.

Replace production with `stop` to halt the containers and `down` to clear their state. You need to replace remotehost with the IP address for your machine.



First exit the remote machine

```bash
exit
```

## Port Forwarding

In order to get the notebook urls run
```
ssh pydentity@remotemachine 'aries-jupyter-playground/scripts/get_URLS.sh'
```

Now we still need to establish port forwarding to the remote machine in order to access the remote notebooks. This can be done like so:

```
ssh -N -f -L localhost:localport:remotehost:remoteport pydentity@remotemachineip
```

