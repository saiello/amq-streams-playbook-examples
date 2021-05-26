# amq-streams-playbook-examples

This repo provides a set of examples showing how to use [amq-streams role](https://github.com/saiello/amq-streams) and collecting different ways to configure it.


## Prerequisites

- Vagrant 
- Ansible

## Set Red Hat Customer portal credentials

```
export RHN_USERNAME=johndoe@example.com
export RHN_PASSWORD=*****
```


## How to use

Step into an example folder and exec `vagrant up`. 
The ansible provisioner is configured to use the playbook.yml and the generated inventory to setup the VMs.

## Examples

- single-kafka-server
- single-kafka-server-mtls
- single-kafka-server-oauth ( WIP )
- single-kafka-server-sasl-plain
- single-kafka-server-ssl
- cluster-kafka-colocated
- cluster-kafka-dedicated