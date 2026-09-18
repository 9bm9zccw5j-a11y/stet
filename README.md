# Водяной — магазин сантехники

React 19 + Vite 7 + Tailwind 4 + Supabase + framer-motion.

## Запуск (обязательно через сервер, не двойным щелчком)

```bash
npm install     # один раз
npm run dev     # http://localhost:5173
```

**Открывать нужно адрес из терминала** (`http://localhost:5173`), а не файл `index.html`.
Если открыть `index.html` двойным щелчком — страница будет пустой: браузер не умеет
исполнять `/src/main.tsx` без сборщика.

## Сборка одного файла

```bash
npm run build     # dist/index.html — один файл со всеми стилями и скриптами
```
Благодаря `vite-plugin-singlefile` и `base: "./"` собранный `dist/index.html`
открывается даже с диска, без сервера.

## Частые причины «сайт не открывается»

| Симптом | Причина | Решение |
|---|---|---|
| Пустая страница, открыли файл | запуск `file://index.html` | `npm run dev` и открыть адрес из терминала |
| `npm: command not found` | не установлен Node.js | поставить Node LTS 22+ |
| `vite: command not found` | не выполнен `npm install` | `npm install` |
| Ошибка про версию Node | Vite 7 требует Node ≥ 20.19 | обновить Node |
| Порт занят | 5173 уже используется | `npm run dev -- --port 3000` |
| Данные пустые | нет таблицы в Supabase | см. ниже |
| Красная надпись «Ошибка Supabase» | нет таблицы `vodyanoy_store` | админка → синхронизация → SQL |

## Настройка Supabase

1. Меню → **Админ-панель** (логин `admin`, пароль `123456789`).
2. Нажмите круглую стрелку синхронизации — появится модалка с SQL.
3. Supabase → SQL Editor → New query → вставьте SQL → **Run**.
4. Вернитесь в админку и нажмите «Проверить запись в Supabase».

Таблица `vodyanoy_store` хранит: `products`, `categories`, `loyalty_users`,
`plumbers`, `media_library`. Изображения — в публичном бакете `vodyanoy-media`.

## Структура

```
src/
├─ main.tsx, App.tsx, index.css
├─ data/catalog.ts          типы + категории по умолчанию
├─ hooks/                   useProducts, useCategories, useLoyalty, usePlumbers, useMediaLibrary
├─ utils/                   supabase, cloudSync, imageUpload, saveCache, cn
└─ components/              ShopView, LoyaltyCard, PlumbersList, PumpCalculator, AdminPanel
```

## Картинки

Категории и баннеры ждут файлы в `public/images/`:
`cat-ppr.png`, `cat-brass.png`, `cat-valves.png`,
`banner-reputation.png`, `banner-warranty.png`, `banner-returns.png`.

## Проверка типов

```bash
npm run check    # tsc --noEmit
```
