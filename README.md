# News Aggregator

Простое `FastAPI`-приложение для сбора новостей из открытых источников и обновления курсов ЦБ РФ.

## Что делает

- собирает новости из `РБК`, `Коммерсантъ`, `ТАСС`, `Ведомости`
- старается извлекать полный текст статьи, а не анонс
- отбрасывает короткие материалы меньше `300` слов
- добавляет `loaded_at` и по возможности `published_at`
- разбивает текст на чанки и сохраняет в `CSV`
- обновляет курсы `USD`, `EUR`, `BYN`, `KZT`, `GBP` из API ЦБ РФ

## Запуск

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

## Ручки

- `GET /health` - проверка сервиса
- `POST /collect` - один проход сбора
- `GET /collect/stream` - потоковый сбор в формате `SSE`
- `GET /dataset` - превью сохраненных строк из `CSV`

## Формат CSV

Файл создается автоматически: `data/news_dataset.csv`

Колонки:

- `source`
- `title`
- `text`
- `url`
- `chunks`
- `loaded_at`
- `published_at`
