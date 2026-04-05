# Личный менеджер (MVP)

Fullstack: **React (Vite)** + **Express** + **MongoDB** + **JWT**. Данные задач, привычек, заметок и финансов хранятся только на сервере и изолированы по `userId`.

## Структура проекта

```
personal-manager/
├── backend/
│   ├── package.json
│   ├── .env.example
│   └── src/
│       ├── index.js
│       ├── config/database.js
│       ├── middleware/auth.js
│       ├── models/          # User, Task, Habit, Note, FinanceEntry
│       ├── routes/          # auth, tasks, habits, notes, finance
│       └── utils/habitStats.js
├── frontend/
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── index.html
│   ├── public/favicon.svg
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       ├── index.css
│       ├── api/client.js
│       ├── contexts/        # Auth, Theme
│       ├── pages/         # Login, Register, Dashboard
│       └── components/    # Header, tabs (Tasks, Habits, Notes, Finance)
└── README.md
```

## API (backend)

| Метод | Путь | Описание |
|--------|------|-----------|
| POST | `/auth/register` | Регистрация `{ email, password }` |
| POST | `/auth/login` | Вход |
| * | `/tasks`, `/habits`, `/notes`, `/finance` | CRUD, заголовок `Authorization: Bearer <JWT>` |
| GET | `/finance/stats` | Сводка день / неделя / месяц + всего |
| POST | `/habits/:id/done-today` | Отметить привычку на сегодня |

## Установка и запуск

### Требования

- Node.js 18+
- MongoDB (локально или URI облака)

### 1. MongoDB

Запустите локальный MongoDB или задайте `MONGODB_URI` в `.env`.

### 2. Backend

```bash
cd backend
copy .env.example .env
# Отредактируйте .env: MONGODB_URI, JWT_SECRET
npm install
npm run dev
```

API по умолчанию: `http://localhost:4000`.

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

Приложение: `http://localhost:5173`. Запросы к `/auth`, `/tasks`, … проксируются на порт 4000 (см. `vite.config.js`).

**Продакшен-сборка фронта:** задайте в `.env` переменную `VITE_API_URL` с URL вашего API (без завершающего слэша), затем:

```bash
npm run build
npm run preview
```

### PWA

После `npm run build` сервис-воркер регистрируется автоматически. Для иконки установки можно заменить `public/favicon.svg` и обновить `manifest` в `vite.config.js`.

## Безопасность (продакшен)

- Сильный случайный `JWT_SECRET`
- HTTPS
- Ограничить `cors` конкретными origin вместо `origin: true`

## Автор

В интерфейсе указано: **Made by Temirlan**.
