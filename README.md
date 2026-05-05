[![Kittygram Workflow](https://github.com/YuraZvonarev/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/YuraZvonarev/kittygram_final/actions/workflows/main.yml)

#  Как работать с репозиторием финального задания


## Что нужно сделать

Настроить запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions

## Как проверить работу с помощью автотестов

В корне репозитория создайте файл tests.yml со следующим содержимым:
```yaml
repo_owner: ваш_логин_на_гитхабе
kittygram_domain: полная ссылка (https://доменное_имя) на ваш проект Kittygram
taski_domain: полная ссылка (https://доменное_имя) на ваш проект Taski
dockerhub_username: ваш_логин_на_докерхабе
```

Скопируйте содержимое файла `.github/workflows/main.yml` в файл `kittygram_workflow.yml` в корневой директории проекта.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

## Чек-лист для проверки перед отправкой задания

- Проект Taski доступен по доменному имени, указанному в `tests.yml`.
- Проект Kittygram доступен по доменному имени, указанному в `tests.yml`.
- Пуш в ветку main запускает тестирование и деплой Kittygram, а после успешного деплоя вам приходит сообщение в телеграм.
- В корне проекта есть файл `kittygram_workflow.yml`.


## Описание

kittygram - это-вебприложение, где пользователи могут делиться фотографиями и интересными фактами о своих котах. Проект помогает обьединить любителей кошек, позволяет создавать карточки питомцев и просматривать чужик котиков.


## Как развернуть проект локально
1. Клонировать репозиторий
git clone https://github.com/YuraZvonarev/kittygram_final.git
2. Создать файл .env 
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=secure_password
POSTGRES_DB=kittygram
DB_HOST=db
DB_PORT=5432
SECRET_KEY=ваш_секретный_ключ
3. Запустить контейнеры
docker compose up -d --build

## Примеры запросов к API
Регистрация пользователя
curl -X POST http://localhost:9000/api/users/ \
-H "Content-Type: application/json" \
-d '{"username": "kotik", "password": "123456"}'
Создание карточки котика
curl -X POST http://localhost:9000/api/cats/ \
-H "Authorization: Token <ваш_токен>" \
-H "Content-Type: application/json" \
-d '{"name": "Барсик", "color": "рыжий", "birth_year": 2020, "image": "https://example.com/cat.jpg"}'
Получение списка котиков
curl http://localhost:9000/api/cats/
