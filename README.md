1. 
```bash 
TASK [Print fact] *********************************************************************************************************************************************************************************ok: [localhost] => {
    "msg": 12
}
```
2. 
```bash
---
  default_fact: 12
  ```
3.
```bash
CONTAINER ID   IMAGE                          COMMAND                  CREATED          STATUS                PORTS            NAMES
fd7576cc8739   pycontribs/ubuntu:latest       "sleep 6000000"          14 seconds ago   Up 13 seconds                          ubuntu
8126b3e0b87c   pycontribs/centos:7            "sleep 6000000"          45 seconds ago   Up 44 seconds                          centos7
```
4. 
```bash
TASK [Print fact] *********************************************************************************************************************************************************************************ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}
```
5. 
```bash
---
  some_fact: "el {{default_fact}}"
  ```
```bash
---
 some_fact: "deb {{default_fact}}"
 ```
6.
```bash
TASK [Print fact] *********************************************************************************************************************************************************************************ok: [centos7] => {
    "msg": "el 12"
}
ok: [ubuntu] => {
    "msg": "deb 12"
}
```
7.
```bash
ansible-vault encrypt group_vars/el/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
ansible-vault encrypt group_vars/deb/examp.yml
New Vault password:
Confirm New Vault password:
Encryption successful
```
8.
```bash
sudo ansible-playbook site.yml -i inventory/prod.yml --ask-vault-password
Vault password: 
```
9.
```bash
buildah - Interact with an existing buildah container
chroot - Interact with local chroot
docker - Run tasks in docker containers
funcd - Use funcd to connect to target
iocage - Run tasks in iocage jails
jail - Run tasks in jails
kubectl - Execute tasks in pods running on Kubernetes.
libvirt_lxc - Run tasks in lxc containers via libvirt
local - execute on controller
lxc - Run tasks in lxc containers via lxc python library
lxd - Run tasks in lxc containers via lxc CLI
netconf - Provides a persistent connection using the netconf protocol
network_cli - Use network_cli to run command on network appliances
oc - Execute tasks in pods running on OpenShift.
paramiko_ssh - Run tasks via python ssh (paramiko)
persistent - Use a persistent unix socket for connection
saltstack - Allow ansible to piggyback on salt minions
ssh - connect via ssh client binary
winrm - Run tasks over Microsoft’s WinRM
zone - Run tasks in a zone instance
```
10.
```bash
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker
  local:
    hosts:
      localhost:
        ansible_connection: local
```
11.
```bash
TASK [Print fact] ************************************************************************************************************************************************************************************************************************************ok: [centos7] => {
    "msg": "el 12"
}
ok: [ubuntu] => {
    "msg": "deb 12"
}
ok: [localhost] => {
    "msg": "loc"
}
```