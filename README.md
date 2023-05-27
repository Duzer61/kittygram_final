# Kittygram
URL: kittyflu.hopto.org
IP: 130.193.55.60
# Kittygram - социальная сеть на самых минималках для размещение фотографий котиков. Учебный проект Яндекс.Практикум.

## Описание проекта
Проект написан в рамках учебного курса по Python от Яндекс.Практикум.
Пользователи могут регистрироваться, загружать фотографии своих котов с кратким описанием, и смотреть котиков других пользователей. Основная задача  - обучение автоматизации деплоя проекта на сервер с помощью Docker.

## Технологии

 - Python 3.9
 - Django==3.2.3
 - djangorestframework==3.12.4
 - Docker
 - Nginx
 - gunicorn
 
## Установка проекта на локальный компьютер из репозитория 
 - Клонировать репозиторий `git clone <адрес вашего репозитория>`
 - перейти в директорию с клонированным репозиторием
 - установить виртуальное окружение `python3 -m venv venv` и активировать его `source venv/scripts/activate`
 - установить зависимости `pip install -r requirements.txt`
 - в директории /backend/kittygram_backend/ создать файл .env . Примерное содержание:

	    POSTGRES_USER=kittygram_user
	    POSTGRES_PASSWORD=mypass
	    POSTGRES_DB=django
	    DB_HOST=db_kittygram
	    DB_PORT=5432
	    SECRET_KEY = '<ваш_ключ>'


# Деплой проекта на удаленный сервер
В репозитории проекта в разделе GitHub Actions `Settings/Secrets/Actions` прописать Secrets - переменные окружения для доступа к сервисам:

   
    DOCKER_USERNAME                # имя пользователя в DockerHub
    DOCKER_PASSWORD                # пароль пользователя в DockerHub
    HOST                           # ip_address сервера
    USER                           # имя пользователя
    SSH_KEY                        # приватный ssh-ключ
    PASSPHRASE                     # кодовая фраза (пароль) для ssh-ключа
    
    TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
    TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)


Для деплоя необходимо внести изменения в некоторые файлы:
- kittygram_final/.github/workflows/main.yml - в tags необходимо заменить имя пользователя на ваше имя в Docker Hub `tags: <ваш логин Docker Hub>/kittygram_backend:latest` для всех tags
- в settings.py внести данные вашего сервера в ALLOWED_HOSTS
- в корне проекта внести изменения в файл `docker-compose.production.yml`: заменить имя пользователя на ваше имя в Docker Hub `image: <ваш логин Docker Hub>/kittygram_gateway` для всех image

При push в ветку main будут автоматически отработаны сценарии по тестированию кода, сборке Docker образов и загрузке их на Docker Hub, деплой проекта из Docker Hub на сервер со сборкой образов, выполнением миграций и сборкой статики. В случае успешного деплоя будет отправлено сообщение в Telegram.
 

## Автор
Данил Кочетов - [GitHub](https://github.com/Duzer61)
Рабочий проект размещен на [kittyflu.hopto.org](https://kittyflu.hopto.org/)

