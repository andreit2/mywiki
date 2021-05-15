Install zfs in Centos
```
yum install -y yum-utils
sudo yum -y install http://download.zfsonlinux.org/epel/zfs-relea
gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfson
yum-config-manager --enable zfs-kmod
yum-config-manager --disable zfs
yum repolist --enabled | grep zfs && echo ZFS repo enabled
yum install -y zfs
```
zpool create pname_pool1 mirror sdb sdc
zpoll list
zpool status
zpool dstroy name_pool1
echo disk{1..6} | xargs -n 1 fallocate -l 500M
zpool create name_pool2 $PWD/disk[1-5]
zpool create mir mirror $PWD/disk[1-5]
zpool create raid raidz1 $PWD/disk[1-3]
zpool create raid raidz2 $PWD/disk[1-2]
zpool create raid raidz3 $PWD/disk[1-3] # less disks
zpool create raid raidz3 $PWD/disk[1-5]
