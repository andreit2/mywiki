```
sfc /scannow
DISM.exe /Online /Cleanup-image /ScanHealth
```

### Мониторинг состояния SSD дисков
```
wmic diskdrive get status
```
https://ab57.ru/cmdlist/wmic.html

### Windows 10 network commands
```
ping
ipconfig
getmac
hostname
nslookup
tracert [host]
netstat
arp /a
pathping [host]
```

```
ipconfig /flushdns
```
