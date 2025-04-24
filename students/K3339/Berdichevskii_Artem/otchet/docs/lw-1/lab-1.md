# Лабораторная работа №1: Веб-приложение с Docker и Alembic

## 📘 Описание проекта
Проект представляет собой контейнеризированное Python-приложение, построенное с использованием **Docker**, **FastAPI** и **Alembic** для управления миграциями базы данных. Вся логика находится в директории `app/`, контейнеризация обеспечивается через `Dockerfile` и `docker-compose`.

---

## 📁 Структура проекта

```
lr1/
├── .env                  # Переменные окружения
├── Dockerfile            # Сборка контейнера
├── docker-compose.yaml  # Компоновка сервисов
├── requirements.txt      # Python-зависимости
├── alembic.ini           # Настройка Alembic
├── app/
│   ├── main.py           # Основной модуль FastAPI
│   ├── database.py       # Подключение к БД
│   ├── start.sh          # Скрипт запуска
│   └── ...
```

---

## 🚀 Установка и запуск

### 🔧 Предварительные требования
- Docker
- Docker Compose

### ▶️ Запуск

```bash
# Клонирование проекта
$ git clone <repo-url>
$ cd lr1

# Копирование переменных окружения
$ cp .env.example .env

# Запуск приложения в контейнере
$ docker-compose up --build
```

После запуска приложение будет доступно по адресу: [http://localhost:8000](http://localhost:8000)

---

## 🧩 Основные модули

### 📄 `main.py`
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, World!"}
```

### 🗃 `database.py`
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(bind=engine)
```

---

## 🛠 Работа с Alembic

### Инициализация Alembic
```bash
$ alembic init alembic
```

### Создание миграции
```bash
$ alembic revision --autogenerate -m "Initial migration"
```

### Применение миграций
```bash
$ alembic upgrade head
```

---

## 📎 Пример запроса

- **URL**: `GET /`
- **Ответ**: `{ "message": "Hello, World!" }`

Можно протестировать через браузер или cURL:
```bash
$ curl http://localhost:8000/
```

---

## ✅ Заключение
Проект демонстрирует базовую архитектуру веб-сервиса с API-интерфейсом, миграциями и возможностью запуска в контейнерах. Это хорошая основа для масштабируемого и удобного в развертывании веб-приложения.

---

<sub>Отчет сгенерирован автоматически с использованием MkDocs-совместимой разметки</sub>


