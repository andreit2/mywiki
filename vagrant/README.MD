Установка vagrant на Centos 7
```
wget https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_x86_64.rpm
yum install 2.2.16/vagrant_2.2.16_x86_64.rpm
```


```
vagrant plugin install vagrant-vbguest

vagrant plugin install vagrant-scp

vagrant global-status

vagrant scp zfs_task1.tar.gz server:/home/vagrant
```
