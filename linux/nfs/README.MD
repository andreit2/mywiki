## Установка и настройка NFS-сервера в Centos 7
### Устанавливаем утилиту
```
sudo yum install nfs-utils
```
Добавляем правила в файерволл
```
sudo firewall-cmd --permanent --zone=public --add-service=nfs
sudo firewall-cmd --permanent --zone=public --add-service=mountd
sudo firewall-cmd --permanent --zone=public --add-service=rpc-bind
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```
Устанавливаем права на директорию, к которой будет доступ
```
sudo chown -R nfsnobody:nfsnobody /mnt/storage
sudo chmod -R 777 /mnt/storage
```
Отредактируем файл с настройками доступа к NFS-серверу
```
sudo nano /etc/exports
/mnt/storage           192.168.1.25(rw,sync,no_root_squash,no_subtree_check) 192.168.1.9(ro,sync,no_root_squash,no_subtree_check)
```
Пример настроек доступа к разным директориям
```
sudo nano /etc/exports
/srv/nfs4         192.168.33.0/24(rw,sync,no_subtree_check,crossmnt,fsid=0)
/srv/nfs4/backups 192.168.33.0/24(ro,sync,no_subtree_check) 192.168.33.3(rw,sync,no_subtree_check)
/srv/nfs4/www     192.168.33.110(rw,sync,no_subtree_check)
/data 192.168.1.100/24(rw,insecure,nohide,all_squash,anonuid=1000,anongid=1000,no_subtree_check)
```
rw — разрешение на запись
ro — только чтение
sync — синхронный режим доступа. sync (async) — указывает, что сервер должен отвечать на запросы только после записи на диск изменений, выполненных этими запросами. Опция async указывает серверу не ждать записи информации на диск, что повышает производительность, но понижает надежность
no_root_squash — по умолчанию пользователь root на клиентской машине не будет иметь доступа к разделяемой директории сервера. Этой опцией мы снимаем это ограничение.
no_all_squash — включение пользовательской авторизации
all_squash — все подключения будут выполнятся от анонимного пользователя
subtree_check (no_subtree_check) — в некоторых случаях приходится экспортировать не весь раздел, а лишь его часть. При этом сервер NFS должен выполнять дополнительную проверку обращений клиентов, чтобы убедиться в том, что они предпринимают попытку доступа лишь к файлам, находящимся в соответствующих подкаталогах. Такой контроль поддерева (subtree checks) несколько замедляет взаимодействие с клиентами, но если отказаться от него, могут возникнуть проблемы с безопасностью системы. Отменить контроль поддерева можно с помощью опции no_subtree_check. Опция subtree_check, включающая такой контроль, предполагается по умолчанию. Контроль поддерева можно не выполнять в том случае, если экспортируемый каталог совпадает с разделом диска;
anonuid=1000 – привязывает анонимного пользователя к «местному» пользователю;
anongid=1000 – привязывает анонимного пользователя к группе «местного» пользователя.

Добавляем службы rpcbind и nfs в автозагрузку и запускаем их
```
sudo systemctl enable rpcbind nfs-server
sudo systemctl start rpcbind nfs-server
```
Демон nfs-server автоматически перечитывает файл /etc/exports, но бывает, что надо вручную запустить перечитывание конфига
```
sudo exportfs -r
```
Команда exportfs показывает какие ресурс опубликованы
```
sudo exportfs
/mnt/storage    192.168.1.25
/mnt/storage    192.168.1.9
```
Если при вводе появляется ошибка — Function not implemented, значит, не запущены службы rpcbind и nfs-server

## Установка и настройка NFS-клиента
Устанавливаем софт
```
sudo yum install nfs-utils
```
Включаем и запускаем включаем службы rpcbind
```
sudo systemctl start rpcbind
sudo systemctl enable rpcbind
```
Создаем каталог, в который будет смонтирована шара и монтируем ее
```
sudo mkdir /mnt/nfs-share
sudo mount -t nfs 192.168.1.12:/mnt/storage /mnt/nfs-share
```
где 192.168.1.12 — ip-адрес NFS-сервера
Настраиваем автоматическое монтирование при перезагрузки сервера
```
sudo nano /etc/fstab
...
192.168.1.12:/mnt/storage  /mnt/nfs-share     nfs    defaults    0 0
```
