# Первый этап: сборка зависимостей попробоавпть обычный питон 
FROM python:3.10 AS builder
ENV PYTHONUNBUFFERED=1


WORKDIR /app
COPY requirements.txt /app

# Устанавливаем зависимости в директорию 
RUN pip install --no-cache-dir --upgrade -r requirements.txt

COPY . /app

# Финальный этап: минимальный образ
FROM python:3.10-alpine
ENV PYTHONUNBUFFERED=1

# Без этого не работает
COPY --from=builder /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages

# Копируем из builder
COPY --from=builder /app /app

WORKDIR /app

EXPOSE 8000

CMD [ "python3", "manage.py", "runserver", "0.0.0.0:8000" ]
