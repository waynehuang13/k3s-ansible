# Build a Kubernetes cluster using k3s via Ansible
- backend is using etcd instead of default sqlite

## K3s Ansible Playbook

Build a Kubernetes cluster using Ansible with k3s. The goal is easily install a Kubernetes cluster on machines running:

- [X] Debian
- [X] Ubuntu
- [] CentOS

on processor architecture:

- [X] x64

## System requirements

Deployment environment must have Ansible 2.4.0+
Master and nodes must have passwordless SSH access

## Usage

First create a new directory based on the `sample` directory within the `inventory` directory:

```bash
cp -R inventory/sample .
```

Second, edit `hosts.ini` to match the system information gathered above. For example:

```bash
[master]
192.16.86.191

[worker]
192.16.86.[191:...]

[k3s_cluster:children]
master
worker
```

If needed, you can also edit `group_vars/all.yml` to match your environment.

Start provisioning of the cluster using the following command:

```bash
ansible-playbook k3s.yml -i hosts.ini -b -u wayne -K
```

## Kubeconfig

To get access to your **Kubernetes** cluster just

```bash
scp wayne@master_ip:~/.kube/config ~/.kube/config
```
