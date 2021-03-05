## Ansible roles for default OS init + kubernetes bootstrap

1. Copy invetory.example as inventory & edit

```
[all]
k8s-1.novalocal ansible_ssh_host=10.126.100.88
k8s-2.novalocal ansible_ssh_host=10.126.100.89

[all:vars]
ansible_user=centos
ansible_ssh_common_args='-o StrictHostKeyChecking=no'

[docker]

some-wierd-docker-only-machine ansible_ssh_host=10.126.100.90

[docker:vars]
ansible_user=centos
ansible_ssh_common_args='-o StrictHostKeyChecking=no'

[kube-master]
k8s-1.novalocal

[kube-node]
k8s-2.novalocal

[k8s-cluster:children]
kube-master
kube-node

```

2. run `ansible-playbook -i inventory playbook.yml`

3. drink coffe

  ...

  PROFFIT

---
#### Kubernetes config default location on master node - `/etc/kubernetes/admin.conf`

#### TO DO:
 - [ ] INFO! fix handlers
 - [x] WARNING! fix default cgroup driver to systemd
 - [ ] INFO! optimize some ugly shit in roles