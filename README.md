# Ansible playbooks to manage Raspberry Pi clusters

This repository contains a set of Ansible playbooks that help to set up and manage a Raspberry Pi cluster.

## How to run?

Install Ansible on a control node and define an inventory (**/etc/ansible/hosts**). For example:

```
# Raspberry Pi 8-node cluster
[rpies]
rpi[01:08].local	ansible_user=pi

[master]
rpi01.local	ansible_user=pi		token=xxxxxxyyyyyyyyyy

[workers]
#rpi02.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxx
rpi03.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi03.local
rpi04.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi04.local
rpi05.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi05.local
rpi06.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi06.local
rpi07.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi07.local
rpi08.local	ansible_user=pi		token=zzzzzzzzzxxxxxxxxxrpi08.local

[workers:vars]
master=rpi01.local:25000
```

Run a playbook as follows:

```bash
ansible-playbook some-playbook.yml --ask-pass
```

## Configuring

Change the target group name (the default is `rpies`) in the **.yml** files before running a playbook if needed.

## Available playbooks

* **ping.yml**: Pings all the machines
* **new-cluster.yml**: Updates the machines and expands their filesystem
* **shutdown.yml**: Shuts down all the machines
* **microk8s-prepare.yml**: Prepares for Kubernetes (Microk8s) installation
* **microk8s-install.yml**: Installs Kubernetes (MicroK8s)
* **microk8s-master.yml**: Generates join tokens in the master node
* **microk8s-workers.yml**: Makes workers join the cluster
* **temperature.yml**: Prints the temperature of each machine

## Related articles

* [Setting Up a Dedicated Database Server on Raspberry Pi](https://dzone.com/articles/set-up-a-dedicated-database-server-on-raspberry)
* [Building a 32-Core Raspberry Pi Cluster From Scratch](https://dzone.com/articles/building-a-24-core-raspberry-pi-cluster-from-scrat)
