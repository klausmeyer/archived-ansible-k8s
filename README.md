# Ansible k8s

Kubernetes setup in my homelab managed with ansible

## Assumptions / Requirements

Three machines:

* `k8s-node01` with `192.168.122.241`
* `k8s-node02` with `192.168.122.246`
* `k8s-node03` with `192.168.122.71`

All machines run debian buster

All machines have `deploy` user with password-less sudo

All machines have two disks:

* `/dev/vda` System & Containers
* `/dev/vdb` GlusterFS Volume

