FROM python:3.12.1-slim-bullseye

# Отключаем создание .pyc файлов и включаем непрерывный вывод в консоль
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Устанавливаем рабочую директорию
WORKDIR /app

# Обновляем пакеты и устанавливаем необходимые зависимости для сборки Python пакетов
RUN apt update -y && \
    apt install -y python3-dev gcc musl-dev libffi-dev && \
    apt clean && rm -rf /var/lib/apt/lists/*

# Добавляем файл pyproject.toml и poetry.lock для установки зависимостей
COPY pyproject.toml poetry.lock* /app/

# Обновляем pip и устанавливаем Poetry
RUN pip install --upgrade pip && pip install poetry

# Отключаем создание виртуальных окружений для Poetry и устанавливаем зависимости
RUN poetry config virtualenvs.create false
RUN poetry install --no-root --no-interaction --no-ansi

# Копируем оставшиеся файлы проекта
COPY /app/* /app/
