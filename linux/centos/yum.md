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
```
yum install
yum search
yum update
yum downgrade # откат до версии
yum check-update 
yum remove
yum info
yum provides
yum shell
yum grouplist
yum groupinfo
yum history
yum history list
yum history info <number of record>
yum history undo <number of record>
yum-config-manager -add-repo URL
yum-config-manager --enable reponame
yum-config-manager --disable reponame
yum updateinfo list security all
yum updateinfo list security installed
yum -y update-security
yum update-minimal -security -y
yum update -cve <CVE>
yum updateinfo list cves
yum updateinfo list
yum info-sec
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
db_verify /var/lib/rpm/Packages
rpm --rebuilddb
yum clean all
yum repolist
yum instal rpmdevtools rpm-build yum-utils

yumdownloader --source redis
rpm -ihv redis.el2.src.rpm
rpmbuild -bb /rpmbuild/SPECS/redis.spec
yum-builddep redis -y
yum-builddep <package|specfile>
```
Свой репозиторий
```
sudo yum install createrepo
sudo mkdir -p /repos/CentOS/7/
sudo createrepo /repos/CentOS/7/
rsync -avz rsync://mirror.truenetwork.ru/centos/7.5.1804/repos/CentOS/7/
[local-base]
name=Local-Base
baseurl=file:///repos/CentOS/7/$basesearch/
enabled=0
```
```
docker run -name nginx -v /srv/nginx/:/usr/share/nginx/html/ -p 80:80 -d nginx
```
