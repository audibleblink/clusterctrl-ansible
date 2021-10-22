# ClusterHAT Ansible Plays

Repo for setting up a 5 node Pi cluster with Ansible and the ClusterHAT

Plays will:

  - update all packages
  - install aptitude
  - modify `/boot/cmdline.txt` to enable container features
    - reboot if necessary
  - Install Docker prerequisites
  - Add Docker GPG and repo to apt
  - Install Docker
  - add the `pi` user to the `docker` group

## Usage

With inventory:
```
[clusterctrl_server]
hammond

[clusterctrl_nodes]
oneil
carter
tealc
danieljackson

[clusterctrl:children]
clusterctrl_server
clusterctrl_nodes
```

In either simple or structured directories run:

```bash
ansible-playbook [-v] clusterctrl.yml
```

## Docker Swarm Init

```bash
ansible clusterctrl_server -a "docker swarm init --advertise-addr 172.19.181.254"
```

```bash
ansible clusterctrl_nodes -a "docker swarm join --token ${TOKEN} 172.19.181.254:2377"
```

