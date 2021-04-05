перевірка конфігурації<br>
nginx -t<br>
активувати конфігурацію веб сервера<br>
ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/ <br>

запуск nginx в виводом STDOUT i STDERR в консоль, цей режим хороший для дебагу 
nginx -g 'daemon off:'
