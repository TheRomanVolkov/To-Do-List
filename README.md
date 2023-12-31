# RESTful Веб-Сервис

Это RESTful веб-сервис, который предоставляет API для управления задачами и категориями.

## Оглавление

- [Установка и настройка](#установка-и-настройка)
  - [Установка](#установка)
  - [Настройка](#настройка)
- [Использование](#использование)
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
- [Автор](#автор)



## Установка и настройка

### Установка

1. Клонируйте репозиторий:

    ```bash
    git clone https://github.com/RomanV2/To-Do-List.git
    cd To-Do-List

### Настройка
2. Установите зависимости:

    ```bash
    pip install -r requirements.txt
    
    
3. Создайте файл конфигурации config.py и определите настройки базы данных и другие параметры по вашему усмотрению.
    ```bash
    # config.py

    class Config:
        SQLALCHEMY_DATABASE_URI = 'your-database-uri'
        # Другие настройки
    
 4. Создайте файл конфигурации config.py и определите настройки базы данных и другие параметры по вашему усмотрению.
    ```bash
    flask db init
    flask db migrate
    flask db upgrade    

# Использование

## Запуск
  ```bash
     app.run

  ```

Сервис будет доступен по адресу http://localhost:5000

# API Endpoints

## Задачи (Tasks)

- **GET /tasks**: Получить список всех задач.
- **POST /tasks**: Создать новую задачу.
- **GET /tasks/<id>**: Получить информацию о задаче по её идентификатору.
- **PUT /tasks/<id>**: Обновить информацию о задаче по её идентификатору.
- **DELETE /tasks/<id>**: Удалить задачу по её идентификатору.

## Категории (Categories)

- **GET /categories**: Получить список всех категорий.
- **GET /categories/<id>**: Получить информацию о категории по её идентификатору.
- **POST /categories**: Создать новую категорию.
- **DELETE /categories/<id>**: Удалить категорию по её идентификатору.

# Примеры запросов

## Создание новой задачи

```bash
curl -X POST http://localhost:5000/tasks -H "Content-Type: application/json" -d "{\"title\": \"New Task\", \"description\": \"Test Description\", \"categories\": [\"Category1\"]}"
```

## Получение списка задач
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
      "message": "Задача успешно создана",
      "id": 1
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
      "date_created": "2023-12-04T12:00:00Z",
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
      "message": "Задача успешно обновлена"
    }
    ```

- **Удалить задачу по ID**
  - Метод: DELETE
  - Путь: /tasks/{id}
  - Ответ:
    ```json
    {
      "message": "Задача удалена успешно"
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
      "message": "Категория успешно создана",
      "category": {"id": 3, "name": "Новая категория"}
    }
    ```

## Автор

Volkov Roman

