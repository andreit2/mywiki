перевірка конфігурації\
nginx -t\
nginx -s reload \
активувати конфігурацію веб сервера\
`ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/`

запуск nginx в виводом STDOUT i STDERR в консоль, цей режим хороший для дебагу 
nginx -g 'daemon off:'
`https://www.nginx.com/blog/using-free-ssltls-certificates-from-lets-encrypt-with-nginx/`
