https://francoisromain.medium.com/host-multiple-websites-with-https-inside-docker-containers-on-a-single-server-18467484ab95


Проект разворачивает jwilder/nginx-proxy на сервере

В данном конфиге прокси и сайты-контейнеры будут находится в домашней директории пользователя devops в папке www.
При необходимости заменить путь /home/devops/www на свой

Сначала нужно создать сеть:

docker network create nginx-proxy

а затем:

cd /home/devops/www/nginx-proxy/

docker-compose up -d

Чтобы проект попал в зону видимости nginx-proxy, в его .env файле должны быть следующие настройки:


VIRTUAL_HOST=your-website.tld,www.your-website.tld
LETSENCRYPT_HOST=your-website.tld,www.your-website.tld
LETSENCRYPT_EMAIL=your-email@domain.tld

также в docker-compose.yml должен быть указан порт в expose или ports


Чтобы указать индивидульные настройки nginx для домена, необходимо в директории ngnix-proxy/vhost.d создать файл с названием домена, например, чтобы сделать перенаправление www на non-www, создаем файл www.your-website.tld и в нем указываем: 


server_name www.your-website.tld;

return 301 \$scheme://your-website.tld\$request_uri;

затем перезапускаем nginx-proxy (docker-compose down и docker-compose up -d)





