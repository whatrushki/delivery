# WHAT Ecosystem Delivery 🚀

Централизованный репозиторий доставки удалённых уведомлений, опросов и журналов изменений (Changelogs) для приложений экосистемы **WHAT Technologies**.

Клиентские библиотеки читают эти файлы напрямую через GitHub Raw CDN с поддержкой HTTP `ETag` / `If-None-Match` для экономии трафика и запросов.

---

## 📁 Структура репозитория

```
delivery/
├── notifications/
│   ├── schema_v1.json         # JSON Schema валидации схемы v1
│   ├── active.json            # Актуальные уведомления и опросы
│   └── archive/               # Автоматически архивируемые просроченные уведомления
│       └── 2026.json
├── changelogs/
│   ├── schema_v1.json         # JSON Schema релизов
│   └── schedule/
│       └── releases.json      # История версий и изменений WHAT-Schedule
└── .github/workflows/
    └── archive-expired.yml    # Ежедневная CI-очистка просроченных уведомлений
```

---

## 📡 Эндпоинты для клиентов

### 1. Актуальные уведомления и опросы
* **URL:** `https://raw.githubusercontent.com/whatrushki/delivery/main/notifications/active.json`
* **Формат:** JSON (схема `notifications/schema_v1.json`)

#### Поддерживаемые типы уведомлений:
* `banner` — информационный баннер на главном экране.
* `dialog` — модальное окно (для критических событий или важных анонсов).
* `push` — локальное всплывающее пуш-уведомление через системный менеджер.
* `survey` — интерактивный опрос внутри приложения.

#### Таргетинг (`targeting`):
* `app_ids` — фильтр по ID приложения (например, `["app.what.schedule"]`).
* `min_version_code` / `max_version_code` — диапазон поддерживаемых версий.
* `institutions` — фильтр по учебному заведению (`["rksi", "sfedu"]`).
* `platforms` — фильтр ОС (`["android", "desktop", "web"]`).

---

### 2. Журнал изменений (Changelog)
* **URL для расписания:** `https://raw.githubusercontent.com/whatrushki/delivery/main/changelogs/schedule/releases.json`
* **Категории:** `new` (новое), `improved` (улучшено), `fixed` (исправлено), `breaking` (важные изменения).
