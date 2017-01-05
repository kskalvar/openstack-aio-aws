OpenStack Ansible AIO on AWS
Kirk S. Kalvar
12/16/2016


Absolute minimum server resources (currently used for gate checks):
8 vCPU’s
16 GB RAM
80 GB free disk space on the root partition

ubuntu trusty 14.04 ami-2d39803a (c3.2xlarge)

# Update ubuntu
sudo -i
apt-get update
apt-get -y dist-upgrade

# install git
apt-get install -y git

# Install OpenStack Ansible (AIO)
cd /opt
git clone https://git.openstack.org/openstack/openstack-ansible -b stable/mitaka
cd /opt/openstack-ansible

# reboot
reboot

# install OpenStack AIO
sudo -i
cd  /opt/openstack-ansible
scripts/bootstrap-ansible.sh
scripts/bootstrap-aio.sh

tmux
time  scripts/run-playbooks.sh

# example attaching to a container
lxc-ls -f
lxc-attach -n aio1_utility_container-*
