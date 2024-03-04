# api_reviews_docker

![maste](https://github.com/sabina-045/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master)

# Описание

Проект представляет собой API для проекта Reviews - сервис отзывов на произведения (фильмы, музыка, книги).

# api_reviews
>API Reviews - это API без лишних деталей. Благодаря этому его легко освоить и доработать. Через приложение уже можно читать информацию о разных произведениях, оставлять отзывы и комментарии к отзывам. Эту основу легко расширить, добавляя новые возможности.

### Технологии:
+ Django==3.2.10
+ djangorestframework==3.12.4
+ PyJWT==2.1.0
+ djangorestframework-simplejwt==5.2.2
+ psycopg2-binary==2.9.6
+ gunicorn==20.1.0
+ Docker==20.10.24

#### Как запустить проект, упакованный в контейнер Docker:

+ устанавливаем Docker
'https://www.docker.com/'
+ клонируем репозиторий:
`git clone git@github.com:sabina-045/api_reviews_docker.git`
+ создаем файл `.env` в директории `yamdb_final/infra/`
    + заполняем его по образцу:
   * DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
   * DB_NAME=postgres # имя базы данных
   * POSTGRES_USER=postgres # логин для подключения к базе данных
   * POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
   * DB_HOST=db # название сервиса (контейнера)
   * DB_PORT=5432 # порт для подключения к БД
   * SECRET_KEY='n&l%385148polhtyn^##a1)icz@4zqj=rq&agdol^##zgl9(vs' # секретный ключ Django
+ переходим `cd yamdb_final/infra/`
    + запускаем docker-compose
    `sudo docker-compose up -d`
+ выполняем миграции
`sudo docker-compose exec web python manage.py migrate`
+ создаем суперюзера:
`sudo docker-compose exec web python manage.py createsuperuser`
+ собираем статику:
`sudo docker-compose exec web python manage.py collectstatic --no-input`
+ смотрим проект по адресу http://localhost/
+ для тестирования проекта при желании заливаем данные в базу данных из фикстур:
'sudo docker-compose exec yamdb python manage.py loaddata /yamdb_final/infra/fixtures.json'

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
