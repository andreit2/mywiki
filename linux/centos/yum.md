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
rpm package command
```
rpm -i <rpm_file> # install pakage from file
rpm -e <name_pakage> # delete pakage
rpm -q --scripts <rpm_name_package> # shows scriplets, for example rpm -q --scripts nginx
rpm -q nginx
rpm -qi nginx 
rpm -ql ngix # shows all files
rpm -qR ngix #shows all dependencies
rpm -qf /etc/nginx/nginx.conf # shows us which package the file belongs to
rpm -Vv nginx # shows modified files
  5 - check sum
  S - size
  L - simboliс link
  D - data change file
  U - user
  G - group 
  M - mode including permissions and file type
  ? - file could not be read
```
