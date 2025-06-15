Это веб-приложение для управления списком задач, построенное на FastAPI.
- CRUD операции для задач
- Сортировка задач по заголовку, статусу, дате создания или приоритету
- Поиск задач по тексту в заголовке или описании
- Топ-N самых приоритетных задач
- Аутентификация пользователей с JWT
- Кэширование GET-запросов
Как запустить:
git clone https://github.com/khramykhalena/Fast_Api.git
cd Fast_Api
pip install -r requirements.txt
uvicorn main:app --reload
доступно по -  http://127.0.0.1:8000/docs и http://127.0.0.1:8000/redoc

Доступные методы:
Метод	Путь	Описание
POST	/users/	Создать пользователя
POST	/token	Получить JWT-токен
POST	/tasks/	Создать задачу
GET	/tasks/	Получить все задачи
GET	/tasks/top/{n}	Топ-N задач по приоритету
GET	/tasks/{task_id}	Получить задачу по ID
PUT	/tasks/{task_id}	Обновить задачу
DELETE	/tasks/{task_id}	Удалить задачу
