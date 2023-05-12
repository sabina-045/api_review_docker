# yamdb_final

![maste](https://github.com/sabina-045/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master)


# Описание

Проект представляет собой API для проекта Reviews.

# api_yamdb
>API Reviews - это API без лишних деталей. Благодаря этому его легко освоить и доработать. Через приложение уже можно читать информацию о разных произведениях,оставлять отзывы и комментарии к отзывам. Эту основу легко расширить, добавляя новые возможности.

#### Как запустить проект, упакованный в контейнер Docker:

+ клонируем репозиторий:
`git clone git@github.com:sabina-045/infra_sp2.git`
+ создаем файл `.env` в директории `infra_sp2/infra/`
    + заполняем его по образцу:
    DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
    DB_NAME=postgres # имя базы данных
    POSTGRES_USER=postgres # логин для подключения к базе данных
    POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
    DB_HOST=db # название сервиса (контейнера)
    DB_PORT=5432 # порт для подключения к БД
+ переходим `cd infra_sp2/infra/`
    + запускаем docker-compose
    `sudo docker-compose up -d`
+ выполняем миграции
`sudo docker-compose exec web python manage.py migrate`
+ заполняем базу данных:
    + создаем суперюзера:
    `sudo docker-compose exec web python manage.py createsuperuser`
    + собираем статику:
    `sudo docker-compose exec web python manage.py collectstatic --no-input`
+ смотрим проект по адресу http://localhost/

#### Инструкции и примеры

>Основные эндпойнты `/api/v1/`:

/titles/ - список произведений, создается админом.

/titles/{title_id}/ - информация об отдельном произведении.

/titles/{title_id}/reviews/ - список отзывов к отдельному произведению, создание отзыва.

/titles/{title_id}/reviews/comments/{comment_id}/ - информация об отдельном комментарии, изменение комментария автором или модератором.

</br>

>Для доступа к API необходимо получить токен:

Нужно выполнить POST-запрос http://127.0.0.1:8000/api/v1/auth/signup/ передав поля username и email.
На указанный адрес придет письмо с confirmation_code.
Нужно отправить POST-запрос http://127.0.0.1:8000/api/v1/auth/token/ передав поля username и confirmation_code.

Полученный токен передаем в заголовке Authorization: Bearer <токен>

</br>


> Команда создателей:
Яндекс Практикум, Сабина Гаджиева

> Вопросы и пожелания по адресу:
sabina_045@mail.ru
