OpenStack Ansible AIO on AWS
Kirk S. Kalvar
12/16/2016

Absolute minimum server resources (currently used for gate checks):
8 vCPU’s
16 GB RAM
80 GB free disk space on the root partition

ubuntu trusty 14.04 ami-2d39803a

# Update ubuntu
sudo -i
apt-get update
apt-get -y dist-upgrade

# install git
apt-get install -y git

# Install OpenStack Ansible (AIO)
cd /opt
git clone https://git.openstack.org/openstack/openstack-ansible -b stable/mitaka

# check branch
cd /opt/openstack-ansible
git branch

# reboot
reboot

# install OpenStack AIO
sudo -i
cd /opt/openstack-ansible
scripts/bootstrap-ansible.sh
scripts/bootstrap-aio.sh

# use tmux to install to protect against accidental disconnects
tmux
time scripts/run-playbooks.sh

# example attaching to utility container
lxc-ls 
lxc-attach -n aio1_utility_container-<container id>

# import image
source /root/openrc
wget http://download.cirros-cloud.net/0.3.1/cirros-0.3.1-x86_64-disk.img 
glance --os-image-api-version 1 image-create --name='cirros-0.3.1-x86_64' --is-public true --container-format=bare --disk-format=qcow2 < cirros-0.3.1-x86_64-disk.img

