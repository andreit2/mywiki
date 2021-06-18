Install VNC on Centos
Устанавливаем графическую оболочку GNOME
```
yum groupinstall "GNOME Desktop" -y
```
Далее устанавливаем VNC-сервер
```
yum install tigervnc-server -y
```
Запускаем vnc-сервер командой
```
vncserver
```
Открываем доступ к подключению
```
firewall-cmd --permanent --zone=public --add-service vnc-server
firewall-cmd --reload
```
или так
```
firewall-cmd --add-port=5901/tcp
firewall-cmd --add-port=5901/tcp --permanent
```
Теперь в VNC-клиенте вбиваете адрес ip_адрес_сервера:5901
5901 — порт по умолчанию.
Для остановки VNC используйте простую команду:
```
vncserver -kill :1
```
