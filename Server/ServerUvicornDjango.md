# 1. Подготовка сервера

## 1.1 Установка необходимых пакетов

_Убедись, что на сервере установлены Python и pip. Можно установить их с помощью следующих команд:_

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

## 1.2. Обновление системы
_Рекомендуется обновить систему перед началом установки:_

```bash
sudo apt update
sudo apt upgrade
```

# 2. Установка и настройка проекта

## 2.1. Создание виртуального окружения
_Перейди в директорию, где ты будешь развертывать проект, и создай виртуальное окружение:_

```bash
python3 -m venv venv
source venv/bin/activate
```

## 2.2. Установка зависимостей
_Установи необходимые пакеты, включая uvicorn и Django:_

```bash
pip install django uvicorn
```

## 2.3. Клонирование проекта
_Если проект хранится в репозитории, клонируй его на сервер:_

```bash
git clone <URL-репозитория>
cd <директория-проекта>
```

## 2.4. Установка зависимостей проекта
_Установи зависимости, указанные в requirements.txt (если такой файл имеется):_

```bash
pip install -r requirements.txt
```

## 2.5. Настройка базы данных
_Выполни миграции базы данных:_

```bash
python manage.py migrate
```

## 2.6. Сбор статических файлов
_Собери статические файлы (если используешь их):_

```bash
python manage.py collectstatic
```

# 3. Настройка uvicorn для запуска

## 3.1. Запуск uvicorn
_Ты можешь запустить uvicorn для тестирования, используя команду:_

_Здесь your_project_name - это имя твоего проекта (корневой папки с settings.py)._

```bash
uvicorn your_project_name.asgi:application --host 0.0.0.0 --port 8000
```

# 4. Настройка Nginx и Gunicorn (или альтернатив)
_Для продакшн-среды обычно используют Nginx в связке с uvicorn и gunicorn. Рассмотрим настройку с Nginx:_

## 4.1. Установка Nginx
_Установи Nginx, если он еще не установлен:_

```bash
sudo apt install nginx
```

## 4.2. Настройка Nginx
_Создай файл конфигурации для твоего сайта:_

```bash
sudo nano /etc/nginx/sites-available/your_project_name
```

_Пример конфигурации:_

```nginx
server {
    listen 80;
    server_name your_domain_or_ip;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static/ {
        alias /path/to/your/staticfiles/;
    }

    location /media/ {
        alias /path/to/your/mediafiles/;
    }
}
```

_Создай символическую ссылку на этот файл в папке sites-enabled:_

```bash
sudo ln -s /etc/nginx/sites-available/your_project_name /etc/nginx/sites-enabled/
```

## 4.3. Перезапуск Nginx
_Перезапусти Nginx, чтобы применить изменения:_

```bash
sudo systemctl restart nginx
```


# 5. Настройка supervisor или systemd
_Для управления процессом uvicorn удобнее использовать supervisor или systemd. Вот пример конфигурации для systemd:_
## 5.1. Создание файла сервиса
_Создай файл сервиса для uvicorn:_

```bash
sudo nano /etc/systemd/system/uvicorn.service
```

_Пример конфигурации:_

```bash
[Unit]
Description=uvicorn daemon for your Django project
After=network.target

[Service]
User=govcarpets
Group=govcarpets_group
WorkingDirectory=/home/govcarpets/GosCarpets
ExecStart=/home/govcarpets/GosCarpets/venv/bin/uvicorn GosCarpets.asgi:application --host 127.0.0.1 --port 8001
Restart=always
Environment="PATH=/home/govcarpets/GosCarpets/venv/bin"

[Install]
WantedBy=multi-user.target

```

## 5.2. Перезапуск и включение сервиса

_Перезапусти systemd и включи сервис:_

```bash
sudo systemctl daemon-reload
sudo systemctl start uvicorn
sudo systemctl enable uvicorn
```

## 6. Проверка статуса uvicorn через systemd

_Если ты использовал systemd для управления процессом uvicorn, можно проверить его статус с помощью команды:_

```bash
sudo systemctl status uvicorn
```


# Если возникли ошибки
## 1. Проверка пользователя и группы

_Убедись, что пользователь govcarpets и группа govcarpets_group существуют на сервере:_

_Проверка пользователя:_

```bash
id govcarpets
```

_Проверка группы:_

```bash
getent group govcarpets_group
```

_Если пользователь или группа не существуют, создай их:_

```bash
sudo useradd govcarpets
sudo groupadd govcarpets_group
sudo usermod -a -G govcarpets_group govcarpets
```

## 2. Проверка прав доступа

_Убедись, что пользователь govcarpets имеет права на доступ к директории проекта и исполняемому файлу uvicorn._

_Проверь права доступа к директории проекта и файлам:_

```bash
ls -ld /home/govcarpets/GosCarpets
ls -l /home/govcarpets/GosCarpets/venv/bin/uvicorn
```

_Убедись, что директория и файл доступны для пользователя govcarpets. Если необходимо, измени права:_

```bash
sudo chown -R govcarpets:govcarpets_group /home/govcarpets/GosCarpets
```
