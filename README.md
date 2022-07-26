# Docker для
## Инструкция
Скачать с GIT
git clone git@github.com:caveinfix/infra_sp2.git
Скачать образ с Dockerhub в программу Docker
docker pull caveinfix/api_yamdb:v2

Пример файла .env. Должен находится в папке ./infra_sp2/infra/:
SECRET_KEY=... (ключ к Джанго проекту)
DB_ENGINE=django.db.backends.postgresql (указываем, что работаем с postgresql)
DB_NAME=postgres (имя базы данных)
POSTGRES_USER=... (логин для подключения к базе данных)
POSTGRES_PASSWORD=... (пароль для подключения к БД (установите свой)
DB_HOST=db (название сервиса (контейнера)
DB_PORT=5432 (порт для подключения к БД)

Запустите docker-compose
docker-compose up
Или пересобрать
docker-compose up -d --build

http://localhost/redoc/


### Для себя
После сборки и запуска выполните по очереди команды:
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input 

# При первом запуске выполнить миграции
docker-compose exec web python manage.py migrate

Для загрузки информации в БД воспользуйтесь fixtures.json
docker-compose exec web python manage.py loaddata fixtures.json

Автор
