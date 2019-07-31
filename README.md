# DevStack-Installation

Create a VM with Ubuntu 16.04 LTS

Add the following network settings for the VM if you want to add bridged network or else keep deafult network settings:
Adapter1=bridge (eth0), Adapter2=NAT (eth1)

Provide static address for the  adapters ...gedit /etc/network/interfaces
(auto lo
iface lo inet loopback

auto eth0 
iface eth0 inet static
address x.x.x.x (public ip address)
netmask 255.255.255.0
gateway x.x.x.x (public Gateway)
dns-nameservers 8.8.8.8 x.x.x.x

auto eth1
iface eth1 inet static
address 10.0.2.15
netmask 255.255.255.0
gateway 10.0.2.1
dns-nameservers 8.8.8.8 x.x.x.x)


Enter the following commands in CLI:
$ sudo useradd -s /bin/bash -d /opt/stack -m stack; echo "stack ALL=(ALL) NOPASSWD: ALL"| sudo tee /etc/sudoers.d/stack; sudo su - stack (not mandatory command)

$ sudo apt-get install cloud-init

$ git clone https://github.com/openstack-dev/devstack.git

$ cd devstack

$ git checkout stable/stein

Create a local.conf and copy the contents of /devstack/samples/local.conf into it.

Uncomment HOST_IP IPv4 address and put the static bridged IP address (in case if you have default network settings then put 10.0.2.15).

Change the passwords (in the same file)

Add FORCE=yes in the first line of /devstack/stack.sh file.

Change the git requirement address from 'git://...' to 'https://...' in /devstack/stackrc file

run ./stack.sh
