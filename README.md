# Go REST Template

## Назначение каталогов

### cmd/
Точки входа приложения.

- `api/` — запускает HTTP REST API. Обычно `main.go` содержит только вызов `app.Run()`.

---

### configs/
Файлы конфигурации приложения.

Например:

- config.yaml
- config.dev.yaml
- config.prod.yaml

---

### internal/
Внутренний код приложения.

#### app/
Composition Root.

Здесь собирается приложение:

- загружается конфигурация;
- создаётся логгер;
- создаются подключения к БД;
- создаются repository;
- создаются use case;
- создаются HTTP handler;
- создаётся и запускается HTTP Server.

#### config/
Загрузка и валидация конфигурации.

#### logger/
Инициализация логирования.

#### middleware/
Общие HTTP middleware (Logger, Recovery, CORS, Auth, RequestID и т.д.).

#### domain/
Доменная модель.

Содержит:

- Entity;
- Value Object;
- интерфейсы Repository;
- доменные ошибки;
- бизнес-правила.

Не зависит от HTTP и PostgreSQL.

#### usecase/
Бизнес-логика приложения.

Каждый use case реализует один сценарий работы.

#### repository/
Реализации интерфейсов доступа к данным.

Например:

- UserRepository
- OrderRepository

#### transport/
Входные адаптеры.

##### http/

HTTP слой приложения.

- `handler/` — HTTP обработчики.
- `request/` — DTO входящих запросов.
- `response/` — DTO ответов клиенту.
- `router.go` — регистрация всех маршрутов и подключение middleware.

#### platform/
Инфраструктурные компоненты.

- `postgres/` — подключение к PostgreSQL.
- `redis/` — подключение к Redis.
- `http/` — HTTP клиенты для обращения к внешним сервисам.

---

### migrations/
SQL миграции.

---

### pkg/
Публичные библиотеки.

Используется только если код действительно должен импортироваться другими Go-модулями.

---

### scripts/
Вспомогательные скрипты.

---

### test/
Интеграционные тесты, фикстуры и тестовые данные.

---

## Корневые файлы

- `go.mod` — Go-модуль.
- `Makefile` — сборка, тестирование, генерация.
- `Taskfile.yml` — альтернатива Makefile.
- `Dockerfile` — сборка Docker-образа.
- `docker-compose.yml` — локальная инфраструктура разработки.
- `.env.example` — пример переменных окружения.
- `.gitignore` — правила Git.
- `README.md` — описание проекта.
