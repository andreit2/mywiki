## Installing and configuring NFS server / client in Centos 7
### Installing and configuring the NFS server
Install nfs-utils and rpcbind to setup NFSv3
```
sudo yum install rpcbind nfs-utils -y
```
Start nfs-server, rpcind services and check nfs status
```
sudo systemctl enable nfs-server --now
sudo systemctl enable rpcbind
```
Check the netstat output for listening TCP and UDP ports
```
sudo yum installnet-tools.x86_64 -y
sudo netstat -ntulp | egrep nfs\|rpc
[vagrant@nfss ~]$ sudo netstat -ntulp | egrep nfs\|rpc
tcp        0      0 0.0.0.0:39976           0.0.0.0:*               LISTEN      2822/rpc.statd
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      373/rpcbind
tcp        0      0 0.0.0.0:20048           0.0.0.0:*               LISTEN      2826/rpc.mountd
tcp6       0      0 :::49499                :::*                    LISTEN      2822/rpc.statd
tcp6       0      0 :::111                  :::*                    LISTEN      373/rpcbind
tcp6       0      0 :::20048                :::*                    LISTEN      2826/rpc.mountd
udp        0      0 0.0.0.0:928             0.0.0.0:*                           373/rpcbind
udp        0      0 0.0.0.0:20048           0.0.0.0:*                           2826/rpc.mountd
udp        0      0 0.0.0.0:58469           0.0.0.0:*                           2822/rpc.statd
udp        0      0 127.0.0.1:878           0.0.0.0:*                           2822/rpc.statd
udp        0      0 0.0.0.0:111             0.0.0.0:*                           373/rpcbind
udp6       0      0 :::928                  :::*                                373/rpcbind
udp6       0      0 :::52721                :::*                                2822/rpc.statd
udp6       0      0 :::20048                :::*                                2826/rpc.mountd
udp6       0      0 :::111                  :::*                                373/rpcbind
```
### Enable firewall
```
sudo systemctl enable firewalld
sudo firewall-cmd --permanent --zone=public --add-service=nfs
sudo firewall-cmd --permanent --zone=public --add-service=mountd
sudo firewall-cmd --permanent --zone=public --add-service=rpc-bind
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```
### Create share directory 
```
sudo mkdir -p /mnt/storage
sudo chown -R nfsnobody:nfsnobody /mnt/storage
sudo chmod -R 777 /mnt/storage
```
### Describe share directiry
```
sudo vi /etc/exports
/mnt/storage           192.168.1.25(rw,sync,no_root_squash,no_subtree_check)
```
The nfs-server daemon automatically rereads the  file /etc/exports
```
sudo exportfs -r
```
The exportfs command shows which resource has been published
```
sudo exportfs -v
```

### Installing and configuring the NFS client
```
sudo yum install nfs-utils -y
```
Turn on and start turn on rpcbind services
```
sudo systemctl start rpcbind
sudo systemctl enable rpcbind
```

```
sudo mkdir /mnt/nfs-share
sudo mount -o nfsvers=3  192.168.50.10:/mnt/storage /mnt/nfs-share
```
```
sudo nano /etc/fstab
```
