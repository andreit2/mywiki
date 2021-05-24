Установка GUI GNOME на CentOS 7
```
yum update
sudo yum -y groups install "GNOME Desktop"
```
Программа, которая запускает графическую среду в большинстве систем Linux, называется X Window System. 
Итак, во-первых, вы должны указать X Window System, что GNOME — это графический интерфейс, используемый по умолчанию.
Поэтому введите эту команду:
```
echo "exec gnome-session" >> ~/.xinitrc
```
Теперь мы закончили установку GNOME и настройку системы X Window. Давайте проверим это, введя команду:
```
startx
```
