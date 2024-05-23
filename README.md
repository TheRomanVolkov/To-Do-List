# RESTful Веб-Сервис

Это RESTful веб-сервис, который предоставляет API для управления задачами и категориями.

## Стек технологий

Этот проект использует следующие технологии:

- **Flask**: Веб-фреймворк на Python.
- **MySQL**: Реляционная база данных, используемая для хранения данных приложения.
- **SQLAlchemy**: ORM для работы с базой данных.
- **Docker**: Платформа для разработки, доставки и запуска приложений в контейнерах.
- **Docker Compose**: Инструмент для определения и запуска многоконтейнерных Docker-приложений.
- **unittest**: Библиотека для написания и выполнения модульных тестов на Python.

## Оглавление

- [Установка и настройка](#установка-и-настройка)
  - [Установка](#установка)
  - [Настройка](#настройка)
- [Сборка и запуск ](#сборка-и-запуск)
  - [Запуск](#запуск)
- [API Endpoints](#api-endpoints)
  - [Задачи (Tasks)](#задачи-tasks)
  - [Категории (Categories)](#категории-categories)
- [Примеры запросов](#примеры-запросов)
  - [Создание новой задачи](#создание-новой-задачи)
  - [Получение списка задач](#получение-списка-задач)
- [API Ресурсы](#api-ресурсы)
  - [Задачи (Tasks)](#задачи-tasks-1)
  - [Категории (Categories)](#категории-categories-1)
- [Тестирование](#тестирование)
- [Автор](#автор)

## Установка и настройка

### Установка

1. Клонируйте репозиторий:

    ```bash
    git clone https://github.com/TheRomanVolkov/To-Do-List.git
    cd To-Do-List
    ```

### Настройка
2. Настройте файл .env на основе .env.example (определите настройки базы данных и другие параметры)

### Сборка и запуск

3. Запустите докер-контейнеры:

    ```bash
    docker-compose up --build
    ```
Если тесты не пройдут, сборка завершится с ошибкой и образ не будет создан.

Сервис будет доступен по адресу http://localhost:5000

## API Endpoints

### Задачи (Tasks)

- **GET /tasks**: Получить список всех задач с возможностью фильтрации и сортировки.
- **POST /tasks**: Создать новую задачу.
- **GET /tasks/<id>**: Получить информацию о задаче по её идентификатору.
- **PUT /tasks/<id>**: Обновить информацию о задаче по её идентификатору.
- **DELETE /tasks/<id>**: Удалить задачу по её идентификатору.

### Категории (Categories)

- **GET /categories**: Получить список всех категорий.
- **GET /categories/<id>**: Получить информацию о категории по её идентификатору.
- **POST /categories**: Создать новую категорию.
- **DELETE /categories/<id>**: Удалить категорию по её идентификатору.

## Примеры запросов

### Создание новой задачи

```bash
curl -X POST http://localhost:5000/tasks -H "Content-Type: application/json" -d "{\"title\": \"New Task\", \"description\": \"Test Description\", \"categories\": [\"Category1\"]}"
```

### Получение списка задач
```bash
curl -X GET http://localhost:5000/tasks
```

### API Ресурсы

#### Задачи (Tasks)

- **Создать новую задачу**
  - Метод: POST
  - Путь: /tasks
  - Тело запроса:
    ```json
    {
      "title": "Название задачи",
      "description": "Описание задачи",
      "categories": ["категория1", "категория2"]
    }
    ```
  - Ответ:
    ```json
    {
      "id": 1,
      "title": "Название задачи",
      "description": "Описание задачи",
      "created_at": "2023-12-04T12:00:00Z",
      "updated_at": "2023-12-04T12:00:00Z",
      "file_path": "/uploads/file.txt",
      "categories": ["категория1", "категория2"]
    }
    ```

- **Получить задачу по ID**
  - Метод: GET
  - Путь: /tasks/{id}
  - Ответ:
    ```json
    {
      "id": 1,
      "title": "Название задачи",
      "description": "Описание задачи",
      "created_at": "2023-12-04T12:00:00Z",
      "updated_at": "2023-12-04T12:00:00Z",
      "file_path": "/uploads/file.txt",
      "categories": ["категория1", "категория2"]
    }
    ```

- **Обновить задачу по ID**
  - Метод: PUT
  - Путь: /tasks/{id}
  - Тело запроса (возможные поля для обновления):
    ```json
    {
      "title": "Новое название задачи",
      "description": "Новое описание задачи",
      "categories": ["новая_категория"]
    }
    ```
  - Ответ:
    ```json
    {
      "id": 1,
      "title": "Название задачи",
      "description": "Описание задачи",
      "created_at": "2023-12-04T12:00:00Z",
      "updated_at": "2023-12-04T12:00:00Z",
      "file_path": "/uploads/file.txt",
      "categories": ["категория1", "категория2"]
    }
    ```

- **Удалить задачу по ID**
  - Метод: DELETE
  - Путь: /tasks/{id}
  - Ответ:
    ```json
    {
      "message": "Task and associated file deleted successfully"
    }
    ```

#### Категории (Categories)

- **Получить список всех категорий**
  - Метод: GET
  - Путь: /categories
  - Ответ:
    ```json
    {
      "categories": [
        {"id": 1, "name": "категория1"},
        {"id": 2, "name": "категория2"}
      ]
    }
    ```

- **Получить категорию по ID**
  - Метод: GET
  - Путь: /categories/{id}
  - Ответ:
    ```json
    {
      "category": {"id": 1, "name": "категория1"}
    }
    ```

- **Создать новую категорию**
  - Метод: POST
  - Путь: /categories
  - Тело запроса:
    ```json
    {
      "name": "Новая категория"
    }
    ```
  - Ответ:
    ```json
    {
      "message": "Category created successfully",
      "category": {"id": 3, "name": "Новая категория"}
    }
    ```

- **Удалить категорию по ID**
  - Метод: DELETE
  - Путь: /categories/{id}
  - Ответ:
    ```json
    {
      "message": "Category deleted successfully"
    }
    ```

## Тестирование

Для выполнения тестов используйте команду:

```bash
docker-compose run flask_todo_app python -m unittest discover
```

Это запустит все тесты, определенные в вашем приложении.

## Автор

Volkov Roman
