# Docker для api_yamdb
### Технологии
- Django 2.2.16
- Python 3.10.4
- Django REST Framework 3.12.4
- Simple-JWT 4.8.0
- PostgreSQL 13.0-alpine
- Nginx 1.21.3-alpine
- Gunicorn 20.0.4
- Docker 20.10.17
- Docker-compose 3.8
### Подготовка к запуску
Скачиваем к себе локально репозиторий:
```git
git clone git@github.com:caveinfix/infra_sp2.git
```
Далее переходим в директорию:
```git
cd infra/
```
и создаем скрытый файл .env:
```git
nano .env
```
с переменными окружения по данному шаблону:
```git
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password 
DB_HOST=db
DB_PORT=5432
# Данные для отправки почты, email(yandex) +  пароль
EMAIL_HOST_USER = simple@yandex.ru
EMAIL_HOST_PASSWORD = pass
```
Сохраняем ctrl + o и выходим ctrl + x из редактора Nano.

### Разворачиваем контейнер
Начинаем сборку:
```
docker-compose up --build -d
```
Далее выполняем миграции:
```
docker-compose exec web python manage.py migrate
```
Собираем статику:
```
docker-compose exec web python manage.py collectstatic --no-input
```
Наполняем проект тестовыми данными:
```
docker-compose exec web python manage.py loaddata fixtures.json 
```
Для удобства уже создан тестовый аккаунт с правами администратора:
```
login:admin
pass:admin
```
Или можно создать нового пользователя по команде:
```
docker-compose exec web python manage.py createsuperuser
```

### Проверка
После выполненых действий Вы можете ознакомиться с функционалом API по ссылке:
```
http://localhost/redoc/
```
Проверить, что тестовые данные успешно загружены, например, открыв список произведений:
```
http://localhost/api/v1/titles/
```
### Образ на Dockerhub
Свежую версию образа можно скачать с Dockerhub:
```
docker pull caveinfix/api_yamdb:v3
```
### Автор:
Филипп https://github.com/caveinfix/

