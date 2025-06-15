FastAPI + MySQL (Docker Compose)

Этот проект демонстрирует взаимодействие между веб-приложением на FastAPI и базой данных MySQL, запущенными в разных Docker-контейнерах.

 Цель
- Запуск FastAPI и MySQL в отдельных контейнерах
- Организация взаимодействия между ними
- Тестирование CRUD API через Swagger и curl
- Сохранение данных после удаления контейнеров (volume)
- Демонстрация проекта через asciinema

- FastAPI
- MySQL 8
- SQLAlchemy
- Docker + Docker Compose
- JWT (аутентификация)
- Volume для сохранения данных


Установка и запуск
1. Клонируй проект
git clone https://github.com/khramykhalena/fast_api2.git
cd fast_api2

2. Создай .env файл
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=tasks
MYSQL_USER=admin
MYSQL_PASSWORD=admin

3. Запусти контейнеры
docker compose up --build

Swagger UI
Перейди в браузере:
http://localhost:8000/docs — здесь ты можешь протестировать API визуально.

Тестирование через curl
1. Создать пользователя
curl -X POST http://localhost:8000/users/ -H "Content-Type: application/json" -d '{"username": "tester", "password": "tester"}'

2. Получить токен
curl -X POST http://localhost:8000/token -H "Content-Type: application/x-www-form-urlencoded" -d "username=tester&password=tester"
Отсюда надо взять токен, его нужно подставлять в следующие запросы.

3. Создать задачу
curl -X POST http://localhost:8000/tasks/ -H "Authorization: Bearer <ACCESS_TOKEN>" -H "Content-Type: application/json" -d '{"title": "Сделать домашку","description": "по Docker","status": "в ожидании","priority": 2}'

4. Получить список задач
curl -X GET http://localhost:8000/tasks/ -H "Authorization: Bearer <ACCESS_TOKEN>"

5. Обновить задачу
curl -X PUT http://localhost:8000/tasks/1 -H "Authorization: Bearer <ACCESS_TOKEN>" -H "Content-Type: application/json" -d '{"title": "Сделать домашку","description": "по Docker","status": "в процессе","priority": 5}'

6. Удалить задачу
curl -X DELETE http://localhost:8000/tasks/1 -H "Authorization: Bearer <ACCESS_TOKEN>"

Проверка Volume (сохранение данных)
1. Создай задачу
2. Останови контейнеры: docker compose down
3. Подними снова: docker compose up
4. Повтори GET /tasks/ — данные должны сохраниться 

Запись в asciinema

asciinema rec
cat Dockerfile
cat docker-compose.yml
cat .env
cat requirements.txt
cat README.md
docker compose up --build
curl ... (CRUD-запросы)
docker compose down
docker compose up
curl ... (GET — проверить сохранение)
exit
