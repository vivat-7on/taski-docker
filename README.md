# API для Управления Подписками Пользователей

Этот проект реализует API для управления подписками пользователей. Включает модели для обработки подписок и методы для управления ими. Проект развернут на удаленном сервере Yandex Cloud с использованием Docker.

## Стек технологий

![Django](https://img.shields.io/badge/Django-092E20?logo=django&logoColor=white)
![Django REST Framework](https://img.shields.io/badge/Django_REST_Framework-FF3C2A?logo=django&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?logo=json-web-tokens&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white)
![Gunicorn](https://img.shields.io/badge/Gunicorn-499848?logo=gunicorn&logoColor=white)

## Описание проекта

Проект включает разработку API для управления подписками пользователей в приложении:
- **Модель Follow**: Поддержка полей `user` (подписчик) и `following` (на кого подписан).
- **Эндпоинт `/follow/`**:
  - **GET**: Получение всех подписок пользователя с возможностью поиска по параметру `search`.
  - **POST**: Подписка пользователя на другого пользователя с проверкой попытки подписки на самого себя и возвратом информативного сообщения об ошибке.
- **Аутентификация**: Использование JWT-токенов для защиты эндпоинтов и управления доступом.
- **Обработка ошибок**: Ответ с кодом 401 Unauthorized для анонимных пользователей, пытающихся получить доступ к защищенным ресурсам.
- **Развертывание**: Развертывание приложения на удаленном сервере Yandex Cloud с использованием Docker.

## Установка и настройка

1. **Клонируйте репозиторий:**
   ```bash
   git clone <URL-репозитория>
   cd <папка-репозитория>
   ```

2. **Настройте переменные окружения:**
   Создайте файл `.env` в корневой директории проекта и добавьте настройки для базы данных и JWT:
   ```env
   DB_NAME=your_db_name
   DB_USER=your_db_user
   DB_PASSWORD=your_db_password
   DB_HOST=db
   DB_PORT=5432
   SECRET_KEY=your_secret_key
   JWT_SECRET_KEY=your_jwt_secret_key
   ```

3. **Запустите Docker Compose:**
   ```bash
   docker-compose up --build
   ```

   Это запустит все контейнеры (backend, db, nginx, gunicorn) и поднимет приложение.

## Автоматизация и развертывание

Проект настроен для автоматизации тестирования и развертывания:
- **Аутентификация**: Проверка кода и запуск тестов.
- **Сборка Docker образов** и их отправка на Docker Hub.
- **Обновление** образов на сервере и перезапуск приложения.
- **Сборка статики** и выполнение миграций.
- **Уведомления** о завершении деплоя в Telegram.

## Работа с проектом

1. **Запуск тестов:**
   ```bash
   docker-compose exec backend pytest
   ```

2. **Переход к интерфейсу приложения:**
   После запуска контейнеров, приложение доступно по [http://localhost](http://localhost).

3. **Обновление статики:**
   ```bash
   docker-compose exec backend python manage.py collectstatic
   ```

4. **Миграции:**
   ```bash
   docker-compose exec backend python manage.py migrate
   ```
