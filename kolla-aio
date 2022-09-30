```yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens18:
      dhcp4: no
      addresses: [10.0.0.182/24]
      gateway4: 10.0.0.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
#    ens18:
#      dhcp4: true
    ens19:
      dhcp4: false
  version: 2
-------------------

sudo usermod -aG sudo openstack
echo "openstack ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/openstack

lsblk,, #cek disk yg kosong/bukan os
sudo pvcreate /dev/vdb /dev/vdc
sudo vgcreate cinder-volumes /dev/vdb /dev/vdc
sudo vgs

sudo apt update && sudo apt upgrade -y
sudo apt install python3-dev libffi-dev gcc libssl-dev python3-pip -y

sudo apt install python3.8-venv -y
python3 -m venv ~/venv1
source ~/venv1/bin/activate

pip install -U pip
pip install 'ansible<5.0'
pip install git+https://opendev.org/openstack/kolla-ansible@stable/xena

sudo mkdir -p /etc/kolla
sudo chown $USER:$USER /etc/kolla

cp -r ~/venv1/share/kolla-ansible/etc_examples/kolla/* /etc/kolla
cp ~/venv1/share/kolla-ansible/ansible/inventory/* .
sudo mkdir /etc/ansible
sudo nano /etc/ansible/ansible.cfg
[defaults]
host_key_checking=False
pipelining=True
forks=100

kolla-genpwd

sudo nano /etc/kolla/globals.yml
kolla_base_distro: "ubuntu"
kolla_install_type: "source"
network_interface: "ens18"
enable_cinder: "yes"
kolla_internal_vip_address: "10.0.0.55"
enable_haproxy: "no"
keepalived_virtual_router_id: "55"
enable_cinder_backend_lvm: "yes"
nova_compute_virt_type: "qemu"

kolla_base_distro: "ubuntu"
kolla_install_type: "source"
kolla_internal_vip_address: "10.0.0.182"
network_interface: "ens18"
neutron_external_interface: "ens19"
enable_haproxy: "no"
enable_cinder: "yes"
enable_cinder_backend_lvm: "yes"
nova_compute_virt_type: "kvm"

verify
cat /etc/kolla/globals.yml | grep -v "#" |  tr -s [:space:]

kolla-ansible -i ./all-in-one bootstrap-servers 
kolla-ansible -i ./all-in-one prechecks
kolla-ansible -i ./all-in-one deploy

pip install python-openstackclient -c https://releases.openstack.org/constraints/upper/xena
kolla-ansible post-deploy
. /etc/kolla/admin-openrc.sh

~/venv1/share/kolla-ansible/init-runonce

