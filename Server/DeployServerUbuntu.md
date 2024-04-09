**Установка дополнительных моделей**
```bash
sudo apt-get install libpq-dev
```
---
**Создание пользователя**
```bash
adduser username
```
---
**обновление системы**
```bash
apt update
apt list --upgradable
apt upgrade
apt install sudo 
```
---
**Добавление пользователя в группу sudo**

```bash
usermod -aG sudo username
groups username
su username
```
---

**Скачивание дополнительных модулей для работы**
```bash
sudo apt install nginx git supervisor
sudo apt install postgresql
```
---
**Создание базы данных**
```bash
sudo -u postgres psql
CREATE DATABASE banket;
CREATE USER b_user WITH PASSWORD 'She3348Jdfurfghs';
ALTER ROLE userdb SET client_encoding TO 'utf8';
ALTER ROLE userdb SET default_transaction_isolation TO 'read committed';
ALTER ROLE userdb SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE movie TO userdb;
\q
```
----------------------------------------

Создание виртуального окржения
--------------------
python3 -m venv venv
sudo apt install python3.x-venv
source venv/bin/activate

pip install psycopg2-binary
pip install gunicorn
--------------------

Компиляции python 3.6
----------------------
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev
sudo apt-get install -y libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm
sudo apt-get install -y libncurses5-dev  libncursesw5-dev xz-utils tk-dev

wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
tar xvf Python-3.6.4.tgz
cd Python-3.6.4
./configure --enable-optimizations
make -j8
sudo make altinstall
python3.6

--------------------------------------------
Установка Gunicorn
------------------
gunicorn project.wsgi:application --bind 111.222.333.44:8000
----------------------------------------
Настрока nginx
--------------
sudo nano /etc/nginx/sites-available/default
server {
    listen 80;
    server_name 111.222.333.44; # здесь прописать или IP-адрес или доменное имя сервера
    access_log  /var/log/nginx/example.log;
 
    location /static/ {
        root /home/user/myprojectenv/myproject/myproject/;
        expires 30d;
    }

    location /media/ {
        root /home/poppins/myprojectenv/;
        expires 30d;
    }
 
    location / {
        proxy_pass http://127.0.0.1:8000; 
        proxy_set_header Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

sudo service nginx restart

------------------------------------------
For SSL
-------
sudo apt install snapd
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx

map $sent_http_content_type $expires {
    "text/html"                 epoch;
    "text/html; charset=utf-8"  epoch;
    default                     off;
}
server {
    listen 80;
    server_name www.django.com;
    return 301 https://django.com$request_uri;
}
server{
    listen 443 ssl;
    ssl on;                                      
    ssl_certificate /etc/ssl/django.crt;     
    ssl_certificate_key /etc/ssl/django.key; 
    server_name django.com;
    client_max_body_size 100M;

    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_http_version 1.1;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript application/javascript;

    location /static/ {
        root /home/user/pj;
        expires 1d;
    }

    location /media/ {
        root /home/user/pj;
        expires 1d;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

---------------------------------------
Настройка supervisor
cd /etc/supervisor/conf.d/
sudo ln /home/linkspace/Linkiq/LinkScrop/config/link.conf
sudo update-rc.d supervisor enable
sudo service supervisor start
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl status project
sudo supervisorctl restart project
--------------------
python manage.py collectstatic


https://icxxic.sharepoint.com/sites/plk_edu


edu_lk






map $sent_http_content_type $expires {
    "text/html"                 epoch;
    "text/html; charset=utf-8"  epoch;
    default                     off;
}

server {
    listen 80;
    server_name iqnix.space;
    return 301 https://iqnix.space$request_uri;
}


server {
    listen 443 ssl; # managed by Certbot
    ssl on; 
    ssl_certificate /etc/letsencrypt/live/iqnix.space/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/iqnix.space/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

    server_name iqnix.space; # здесь прописать или IP-адрес или доменное имя сервера
    client_max_body_size 100M;

    gzip on;
    gzip_vary on;
    gzip_proxied any;
    gzip_http_version 1.1;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript application/javascript;
    location /static/ {
        root /home/linkspace/Linkiq/;
        expires 30d;
    }
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

sudo chown -R spirik:spirik /home/spirik/DvGruz/venv

-------
sudo chmod o+rx /home/poppins/IqnixLink
sudo chown -R poppins:poppins /home/poppins/S444Link/

-------


----------
Бэкап
----------

Создайте резервную копию базы данных: Воспользуйтесь утилитой pg_dump, чтобы создать резервную копию базы данных на текущем сервере Ubuntu. Выполните следующую команду в терминале:
pg_dump -U iqlink -d iqlink_db > backup.sql


Создайте новую базу данных: Перейдите на новый сервер Ubuntu и создайте новую базу данных PostgreSQL с теми же параметрами, что и в вашем файле конфигурации Django. Выполните следующую команду в терминале:
sudo -u postgres psql -c "CREATE DATABASE iqlink_db;"


Восстановите данные из резервной копии: Восстановите данные из резервной копии в новую базу данных. Перейдите в каталог, где находится файл backup.sql, и выполните следующую команду:
sudo -u postgres psql -d iqlink_db -f backup.sql