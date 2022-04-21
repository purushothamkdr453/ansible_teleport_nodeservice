# Ansible Playbook for installing teleport node service in target virtual machines
 
## Introduction

As we all know that we need to run teleport agent/service process in all targets inorder to connect to teleport cluster. This repo contains an ansible role which will help you in running teleport node service in target virtual machines.

**Note**: This playbook is tested with ansible version 2.9.23

## Pre-requisites

- capin
- authtoken

`capin` & `authtoken` are required for teleport node service. These have to be generated on teleport cluster side. Execute the below command to generate `capin` & `authtoken`

```
tctl tokens add --type=node --ttl=1h
```
**Note** you can adjust the ttl value according to your needs.

## Execution

Navigate to `ansible-teleport` directory.

```
cd ansible-teleport
```

Update the `inventory` & `group_vars` according to your needs. in mycase I have setup inventory based on the cloud & environment i.e cloud is parent and environment is a children of the cloud. for ex: lets say you are using aws cloudplatform & having different environment like dev, acceptance, staging, production then `aws` is the parent which will have all the envs as children. Take alook at the inventory(
hosts) for more clarity.

**Note** also update `group_vars` according to your needs, these variables will be applied to teleport node service.

After once all the details are updated. Execute the below command to install node service on teleport.

```
ansible-playbook main.yml -i ./hosts --extra-vars "authservers=["teleport.devopsbypr.in:443"] capin=sha256:8aa02a0cad93c83e049c14340a8f33976871fcba0a7939c627728989dd1 authtoken=3d42473daa767198s0a1"
```

**Note** in the above command replace `authservers` `capin` & `authtoken` details.
