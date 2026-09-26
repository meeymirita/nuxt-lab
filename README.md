# Nuxt Lab — Help Center

![Nuxt](Nuxt.png)

> **26.09.2026 — методичка вычитана и исправлена.** Что найдено и что поправлено — в [fixes/nuxt.md](https://github.com/meeymirita/lab-fixes/blob/main/nuxt.md) репозитория `lab-fixes`.

**Статус: ⚪ методичка готова, прохождение впереди.**
**Сложность: высокая.** Проект полностью самостоятельный (свой репозиторий `nuxt-lab`), кода из других лаб не берёт. Vue предполагается знакомым на уровне Vue-лабы (`ref`, `computed`, props/emits, Pinia, Router — здесь не объясняются заново), TypeScript — на уровне сессий 1–3 TS-лабы.

## О чём

Публичный центр поддержки, где у каждой зоны свой режим рендеринга: база знаний — prerender (SSG), статус сервисов — SWR-кеш, обращения клиента — SSR с сессией, кабинет агента — SPA (`ssr: false`). Главное — что Nuxt добавляет поверх Vue: SSR и гидрация, payload, Nitro как сервер внутри проекта, состояние на сервере, `routeRules`, SEO. Почти в каждой сессии есть шаг «сначала сломать, потом починить»: двойной запрос, hydration mismatch, потерянная cookie, утечка состояния между пользователями, общий кеш на все запросы.

## Стек

Nuxt 4.5+ (с пометками про v5), TypeScript strict + `nuxi typecheck`, Nitro server routes, SQLite + Drizzle, Zod-схемы в `shared/`, nuxt-auth-utils, `@pinia/nuxt`, Nuxt Content v3, `@nuxtjs/sitemap` + `@nuxtjs/robots`, Vitest + `@nuxt/test-utils`. Всё в Docker.

## Формат

Методичка [`Nuxt_Lab_HelpCenter.html`](Nuxt_Lab_HelpCenter.html) — открывается в браузере, прогресс по чекбоксам сохраняется локально. У каждого шага: код → «зачем» → команда → ожидаемый результат → «проверь себя»; ответы — в `docs/nuxt-notes.md`.

## Что внутри (6 сессий, ~20,5 ч)

- **Сессия 1** — стенд и основы: docker-compose, скаффолд Nuxt 4, typecheck; файловый роутинг (динамические параметры, catch-all 404); layouts, компоненты и что генерирует `.nuxt/`; SSR vs SPA руками (`view-source`, `ssr: false`, `window` на сервере, `ClientOnly`)
- **Сессия 2** — данные и гидрация: первый server route и тип ответа из хендлера, payload (ломаем двойным запросом через `$fetch`), реактивный query/`lazy`/`pick`/`refresh`, ошибки (404 из хендлера, fatal, `clearError`), hydration mismatch на времени и часовом поясе
- **Сессия 3** — Nitro и БД: Drizzle + SQLite (схема, миграции, Nitro-плагин), `readValidatedBody` + Zod, server middleware request-id, общая схема в `shared/` для клиента и сервера, форма обращения с ошибками сервера по полям
- **Сессия 4** — авторизация и состояние: nuxt-auth-utils и роли, route middleware, потерянная cookie при SSR-`$fetch`, утечка состояния через модульный `ref` → `useState`/`useCookie`, Pinia + `callOnce`, кабинет агента на `ssr: false`
- **Сессия 5** — контент, кеш, рендеринг: Nuxt Content v3, поиск через `defineCachedEventHandler` (и сломанный ключ кеша), `routeRules` на prod-сборке — пререндер базы знаний и SWR для статуса, устаревание и инвалидация
- **Сессия 6** — SEO и продакшн: `useSeoMeta`, canonical, sitemap и robots, `runtimeConfig`, тесты (unit, компонент в Nuxt-окружении, e2e по API), `nuxt build` и multi-stage Dockerfile, финальная таблица «Vue Lab vs Nuxt Lab»

Разделы 1–10 методички — теория (зачем Nuxt поверх Vue, азбука на примере Help Center, рендеринг и гидрация под капотом, режимы рендеринга, данные, Nitro, состояние на SSR, авторизация, контент и SEO, структура проекта), раздел 11 — шесть сессий заданий, разделы 12–15 — чек-лист, глоссарий, вопросы для собеседования, что дальше.

---

Часть сборного репозитория лабораторных работ — [anitech-performance](https://github.com/meeymirita/anitech-performance).
