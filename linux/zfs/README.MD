Шаги установки в CentOS 8
```
sudo yum install -y yum-utils
sudo yum install langpacks-en glibc-all-langpacks -y
sudo yum -y install http://download.zfsonlinux.org/epel/zfs-relea
gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfson
sudo yum-config-manager --enable zfs-kmod
sudo yum-config-manager --disable zfs
sudo yum repolist --enabled | grep zfs && echo ZFS repo enabled
sudo yum install -y zfs
```
Создание пула устройств хранения данных ZFS
```
zpool create name_pool1 mirror sdb sdc
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
zpool create hybrid mirror $PWD/disk[12] mirror $PWD/disk[34]
zpool create hybrid2 raidz2 $PWD/disk[1-3] raidz2 $PWD/disk[4-6]
zfs list
zfs create name_pool/name_dir
zfs destroy name_pool/name_dir
```
Скорость от типа pool
RAID-0 (fastest)
RAID-1
RAIDZ-1
RAIDZ-2
RAIDZ-3 (slowest)
```
zpool create hybrid mirror $PWD/disk[12] mirror $PWD/disk[34]
zpool create hybrid2 raidz2 $PWD/disk[1-3] raidz2 $PWD/disk[4-6]
```
Создание pool с SLOG и L2LARC
Создать сразу
```
zpool create storage mirror sdb sdc \
  log mirror nvme0n1 nvme0n2 \
  cache nvme0n3 nvme0n4
```
Добавить позже
```
zpool create storage mirror sdb sdc
zpool add storage cache nvme0n3 nvme0n4 # L2ARC
zpool add storage log mirror nvme0n1 nvme0n2 # SLOG
```
Создание файловой системы
ФС создается поверх пула
```
zfs create storage/userdir
zfs create storage/data
```
ФС Может быть вложенной
```
zfs create storage/data/video
zfs create storage/data/music
```
смотрим что примонтировано, по умолчание файловая система монтируется в директори пула 
```
mount -t zfs
zfs get mounted
ls /name_pool/name_dir
```
поменять через параметр:mountpoint, директория должна быть пустой
```
zfs set mountpoint=/home/testuser name_pool/name_dir/name_dir1
```
По умолчанию файловая система (dataset) займет все предоставленное место
```
dd if=/dev/urandom of=/home/testuser/file bs=1M
df -h
zfs list
```
Квоты устанавливают лимит на количество
данных в ФС
```
zfs get quota
zfs set quota=500M storage/data/media
```
Гарантирует доступное место файловой системе
```
zfs list # before
zfs set reservation=5G storage/data/video
zfs list # after
```
Параметр размер блока
```
zfs create storage/data/movies
zfs create storage/data/torrents
zfs set recordsize=1M storage/data/movies
zfs set recordsize=64K storage/data/torrents
```
Наследование параметров
```
zfs set checksum=sha256 storage/data/movies
zfs get checksum
zfs set checksum=skein storage/data
zfs get checksum
```
Параметры кэширования
```
zfs set primarycache={all|metadata|none} # ARC
zfs set secondarycache={all|metadata|none} # L2ARC
```
ZFS может сжимать данные при записи на файловую систему и разжимать их при чтении
только новые данные сжимаются. Старые не перепаковываются
```
zfs create storage/src
zfs create storage/src/compressed
zfs set compression=on storage/src/compressed
zfs get compression,compressratio
zfs set compress=gzip pool/fs
zfs set compress=gzip-1 pool/fs
zfs set compress=gzip-9 pool/fs
zfs set compress=lz4 pool/fs
zfs set compress=lzjb pool/fs
zfs set compress=zle pool/fs
```
