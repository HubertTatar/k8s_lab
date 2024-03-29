# Cluster

- Calico https://docs.tigera.io/calico/latest/about/
- Crio https://cri-o.io/

Flow of text processing

```mermaid
flowchart TD
    Control_Plane ---> Node_1
    Control_Plane ---> Node_2
```

See settings.yaml to control resources and number of nodes.

# Install

### Install dependencies:
 - https://www.virtualbox.org/wiki/Downloads
 - https://developer.hashicorp.com/vagrant/install

### Run cluster

Modify host only adapters for Virutalbox

    sudo mkdir -p /etc/vbox/
    echo "* 0.0.0.0/0 ::/0" | sudo tee -a /etc/vbox/networks.conf

Create vms/Restart after halt:

    vagrant up

Shutdown:

    vagrant halt

Remove:

    vagrant destroy -f

### Log to machines

    vagrant status
    vagrant ssh {node}


### Change user from vagrant to root
    
    sudo su

### Change root pass

    sudo -i
    passwd


    /etc/ssh/sshd_config
    PermitRootLogin yes


### Login as root
    
    Vagrantfile
    config.ssh.username = 'root'
    config.ssh.password = 'vagrant'
    config.ssh.insert_key = 'true'

Links:
 - https://github.com/techiescamp/vagrant-kubeadm-kubernetes/
 - https://github.com/techiescamp/kubernetes-learning-path