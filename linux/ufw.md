ufw allow ssh
ufw allow 22
ufw enable
ufw allow http
ufw allow 80
ufw allow https 
ufw allow 443
ufw allow 6000:6007/tcp
ufw allow 6000:6007/udp
ufw allow from 203.0.113.4
ufw allow from 203.0.113.4 to any port 22
ufw allow from 203.0.113.0/24
ufw allow from 203.0.113.0/24 to any port 22
ufw allow in on eth0 to any port 80
ufw allow in on eth1 to any port 3306
ufw deny http
ufw deny from 203.0.113.4
ufw status numbered
ufw delete 2
ufw delete allow http
ufw delete allow 80
ufw status verbose
ufw disable
ufw enable
ufw reset
ufw default deny incoming
ufw default allow outgoing
nano /etc/default/ufw
