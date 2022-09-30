
# update & upgrade
sudo apt update && sudo apt upgrade -y

# set up ulimit
sudo nano /etc/security/limits.conf
> ubuntu soft core -1       
> ubuntu soft nofile 1048576


install microk8s
> sudo apt install snapd

> sudo snap install microk8s --classic

 
setup akses microk8s

* sudo usermod -a -G microk8s ubuntu
* sudo chown -f -R ubuntu ~/.kube
* echo "alias kubectl='microk8s kubectl'" >> ~/.bashrc

set up password
* sudo passwd $USER
* PASSWORD
* PASSWORD


sign up
> su - $USER

> PASSWORD

cek status microk8s

> microk8s status --wait-ready

add-node to cluster

> microk8s add-node

result

```bash
From the node you wish to join to this cluster, run the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05

Use the '--worker' flag to join a node as a worker not running the control plane, eg:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05 --worker

If the node you are adding is not reachable through the default interface you can use one of the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 10.23.209.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 172.17.0.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
Joining a node to the cluster should only take a few seconds. Afterwards
```
