Download rpm
```
yumdownloder <name packeage>
```
for example
```
yumdownloader tree
```
Install Extra Packages for Enterprise Linux (EPEL)
```
yum install -y epel-release
```
How to see into rpm file 
```
rpm2cpio <rpm_file> | cpio -idmv
```
How to install rpm package
```
rpm -i <rpm_file>
```
