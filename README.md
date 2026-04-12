# Telegram Bot для создания задач Bitrix24

Автоматизация создания задач в Bitrix24 через Telegram-бота и n8n.

## Быстрый старт

### 1. Подготовка

```bash
# Скопировать .env.example в .env
cp .env.example .env

# Заполнить .env (см. ниже)
```

### 2. Получить Telegram Bot Token

1. Откройте [@BotFather](https://t.me/BotFather) в Telegram
2. Отправьте `/newbot`
3. Следуйте инструкциям
4. Скопируйте токен в `.env` → `TELEGRAM_BOT_TOKEN`

### 3. Получить Bitrix24 Webhook URL

1. Откройте ваш Bitrix24 портал
2. Перейдите в **Разработчикам** → **Вебхуки**
3. Создайте вебхук с правами на **Задачи**
4. Скопируйте URL в `.env` → `BITRIX24_WEBHOOK_URL`

### 4. Запустить n8n

```bash
docker compose up -d
```

Откройте http://localhost:5678

### 5. Импортировать workflow

1. Откройте n8n UI
2. Создайте новый workflow
3. Импортируйте `workflows/bitrix-telegram-bot.json`
4. Настройте credentials (Telegram, Bitrix24)
5. Активируйте workflow

## Команды бота

| Команда | Описание | Пример |
|---------|----------|--------|
| `/epic` | Создать эпик | `/epic Модуль отчётов` |
| `/sprint` | Создать задачу спринта | `/sprint API логина до 20.01 высокий` |
| `/backlog` | Создать задачу бэклога | `/backlog Кэширование запросов` |
| `/task` | Создать подзадачу | `/task Тесты parent:#123` |
| `/tasks` | Мои активные задачи | `/tasks` |
| `/help` | Справка | `/help` |

## Структура проекта

```
n8n_bitrix/
├── docker-compose.yml      # Docker конфигурация
├── .env.example            # Шаблон переменных
├── .env                    # Переменные (не коммитить)
├── workflows/              # n8n workflows
│   └── bitrix-telegram-bot.json
└── docs/
    └── PRD-telegram-bot-bitrix24.md
```

## Разработка

```bash
# Перезапуск
docker compose restart

# Логи
docker compose logs -f n8n

# Остановить
docker compose down

# С данными
docker compose down -v
```
