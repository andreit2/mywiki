Установка vagrant на Centos 7
```
wget https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_x86_64.rpm && \
yum install 2.2.16/vagrant_2.2.16_x86_64.rpm
```
Установка vagrant на Ubuntu
```
curl -O https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.deb && \
sudo dpkg -i vagrant_2.2.6_x86_64.deb
```

```
vagrant plugin install vagrant-vbguest

vagrant plugin install vagrant-scp

vagrant global-status

vagrant scp zfs_task1.tar.gz server:/home/vagrant
```

```
vboxmanage list vms
vagrant package --base [machine name as it shows in virtual box] --output /Users/myuser/Documents/Workspace/my.box
vagrant box add my my.box
vagrant box list
vagrant halt my
vagrant up my
vagrant box remove my
```
```
vagrant cloud provider create andreit/hw05c virtualbox 1
vagrant cloud auth login
vagrant cloud provider upload andreit/hw05s virtualbox 1 nfss.box
```
