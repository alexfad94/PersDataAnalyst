# Data Assistant

AI-чат на FastAPI + Jinja2 + HTMX. Модель OpenAI отвечает как финансовый аналитик по таблицам и изображениям; графики, отчёты и файлы собираются локально.

## Что умеет

- принимать текстовые сообщения и файлы в одном чате;
- загружать CSV, Excel, JSON и изображения;
- анализировать данные через OpenAI (роль: финансовый аналитик);
- строить графики `line`, `bar`, `histogram` и `pie` в PNG;
- выбирать тип графика в боковой панели чата;
- собирать DOCX-отчёты и markdown-summary;
- показывать и скачивать артефакты прямо из диалога.

## Настройка окружения

Скопируйте пример и заполните ключ:

```bash
copy .env.example .env
```

Основные переменные:

```env
APP_HOST=0.0.0.0
APP_PORT=8000
MAX_FILE_SIZE=10MB
OPENAI_API_KEY=your_api_key
OPENAI_MODEL=gpt-5-mini
OPENAI_MAX_HISTORY_MESSAGES=8
```

Без `OPENAI_API_KEY` чат работает в локальном fallback-режиме (без роли финансового аналитика).

## Локальный запуск

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Откройте `http://localhost:8000`.

## Docker

```bash
docker-compose up --build -d
```

После изменений в коде или шаблонах пересоберите образ (`--build`): volumes монтируют только `storage/uploads` и `storage/outputs`.

## Как проверить

1. Загрузите `examples/sample_sales.csv` или `examples/sample_chart_data.csv`.
2. В сайдбаре выберите тип графика (`pie` / `bar` / `line` / `histogram`) и нажмите «Построить график».
3. Для роли аналитика спросите, например: «Кратко оцени продажи и риски по выручке».
