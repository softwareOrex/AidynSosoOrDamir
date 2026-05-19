# Проект по разработке 
# Лабораторная работа 

Деплой Django-проекта на Windows

Цель работы
Научиться подготавливать Django-проект к публикации и выполнять деплой веб-приложения на сервер.

# Выполненные настройки в проекте

- В college_site/settings.py установлено DEBUG = False.
- В college_site/settings.py задан ALLOWED_HOSTS через переменную окружения DJANGO_ALLOWED_HOSTS.
# Настроены статические файлы:
- STATIC_URL = '/static/'
- STATIC_ROOT = BASE_DIR / 'staticfiles'
# Добавлен файл зависимостей requirements.txt.

# Порядок деплоя (Windows)
1) Проверка локального запуска

2) python manage.py runserver

3) Сбор статических файлов
python manage.py collectstatic

4) Установка зависимостей
pip install -r requirements.txt

5) Миграции и администратор
python manage.py migrate
python manage.py createsuperuser

# 5) Запуск в production через Waitress
Перед запуском укажи IP/домен сервера в DJANGO_ALLOWED_HOSTS:

$env:DJANGO_ALLOWED_HOSTS="127.0.0.1,localhost,192.168.1.98,your-domain.com"
# Узнать IP сервера можно так:

ipconfig
# После этого запускай сервер:

waitress-serve --host=0.0.0.0 --port=8000 college_site.wsgi:application
# Открыть в браузере:

http://IP_СЕРВЕРА:8000
или
http://your-domain.com
# Если сайт не открывается из сети, открой порт 8000 в Windows Firewall.

netsh advfirewall firewall add rule name="Django 8000" dir=in action=allow protocol=TCP localport=8000

# Практический результат 
После выполнения указанных шагов проект готов к деплою на Windows-сервере и доступен по IP-адресу/домену.
