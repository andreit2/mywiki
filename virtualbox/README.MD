Install  VirtualBox on Centos 7
Step 1: Install vboxdrv Kernel Module
```
sudo yum install –y patch gcc kernel-headers kernel-devel make perl wget
sudo reboot
```
Step 2: Download VirtualBox Repository
```
sudo wget http://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo -P /etc/yum.repos.d
```
Step 3: Install VirtualBox 6.0
```
sudo yum install VirtualBox-6.0
sudo systemctl status vboxdrv
```
Step 4: Install Oracle VirtualBox Extension Pack (Optional)
```
wget http://download.virtualbox.org/virtualbox/6.0.4/Oracle_VM_VirtualBox_Extension_Pack-6.0.4.vbox-extpack

sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.0.4.vbox-extpack
```
show me list Virtual Machine
```
vboxmanage list vms
```
