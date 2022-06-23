# Учебный проект: yamdb_final
Приложение  `api_yamdb`  упаковано в контейнеры. Настроены _Continuous Integration_  и  _Continuous Deployment. Реализованы:
-   автоматический запуск тестов,
-   обновление образов на Docker Hub,
-   автоматический деплой на боевой сервер при пуше в главную ветку  **_main_.**

## Бейдж о статусе работы workflow
![workflow](https://github.com/hi-ais/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Установка

1. Склонируйте репозиторий на Ваш компьютер
 `git@github.com:hi-ais/yamdb_final.git`
2. Создайте и активируйте виртуальное окружение:  
 `python -m venv venv` 
 `source venv/Scripts/activate` 
 `python -m pip install`
3. Установите зависимости из папки  `api_yamdb`: 
 `pip install -r requirements.txt`
4. Установите линтер flake8 
 `pip install flake8 pep8-naming flake8-broken-line flake8-return flake8-isort`
5. Проверить код на соответствие стандартам  PEP8 и запуск pytest: 
  `python -m flake8`
  `pytest`
## Подготовка сервера 
1. Войдите на свой удаленный сервер в облаке.
2. Остановите службу nginx: 
  `sudo systemctl stop nginx`
3. Установите Docker: 
   `sudo apt install docker.io`
4. Установите docker-compose:
   `sudo apt-get update`
   `sudo apt-get install docker-compose-plugin`
5. Скопируйте файлы docker-compose.yaml и nginx/default.conf из вашего проекта на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно:
    `scp docker-compose.yaml <USER>@<HOST>`
    `scp default.conf <USER>@<HOST>:/nginx/`
## Развертывание приложения
1. При пуше в ветку main приложение пройдет тесты, обновит образ на DockerHub и сделает деплой на сервер. Дальше необходимо подключиться к серверу.
 `ssh <USER>@<HOST>`
2. Перейдите в запущенный контейнер приложения `api_yamdb` командой:
`sudo docker container exec -it <CONTAINER ID> bash`
3. Внутри контейнера необходимо выполнить миграции, подключить статику и создать суперпользователя:
 `python manage.py makemigrations reviews`
 `python manage.py migrate`
 `python manage.py collectstatic --no-input`
 `python manage.py createsuperuser`

