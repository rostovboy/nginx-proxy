https://francoisromain.medium.com/host-multiple-websites-with-https-inside-docker-containers-on-a-single-server-18467484ab95


Проект разворачивает jwilder/nginx-proxy на сервере

В данном конфиге прокси и сайты-контейнеры будут находится в домашней директории пользователя devops в папке www.
При необходимости необходимо заменить путь /home/devops/www на свой

Сначала нужно создать сеть:

docker network create nginx-proxy

а затем:

cd /home/devops/www/nginx-proxy/

docker-compose up -d