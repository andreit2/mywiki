At first we can create new file such as nano new_app.service

[Service]
WorkingDirectory=/opt/dev.kavalier.com.ua/projectKavaler/
ExecStart=/usr/bin/node /opt/dev.kavalier.com.ua/projectKavaler/server.js
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=node-server
User=andreit
Group=andreit

[Install]
WantedBy=multi-user.target

cp new_app.service /lib/systemd/system/
systemctl daemon-reload
systemctl enable new_app.service
systemctl start new_app.service
