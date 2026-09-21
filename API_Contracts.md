## Подтверждение готовности Hello World (Backend & Frontend)

В рамках 2-й лабораторной работы был успешно развернут и запущен базовый каркас приложения (Hello World project).

* **Базовый URL сервера:** `https://maks.my`
* **Интерактивная спецификация (Swagger UI):** `https://maks.my/hog/docs`
* **Точка проверки работоспособности (Health Check):** `GET /health`

### Проверка статуса системы (Smoke-тест)
Для проверки того, что бэкенд-сервис запущен, корректно обрабатывает маршрутизацию и готов к интеграции с фронтендом, используется эндпоинт `/health`.

**Запрос:**
`GET https://maks.my/health`

**Ожидаемый ответ сервера:**
* **Код ответа:** `200 OK`
* **Тело ответа:**

{
  "status": "ok"
}

# 1. HTML Страницы (Frontend-рендер)
Эти методы возвращают text/html для отображения в браузере:

GET / — Лендинг

GET /test — Страница Теста

GET /register — Страница Регистрации

GET /login — Страница Входа

GET /app — Кабинет

GET /lesson/{lesson_id} — Урок (возвращает страницу конкретного урока)

GET /shop — Магазин

GET /admin — Панель администратора

# 2. Авторизация и настройки (Auth & Settings)

## POST /register

Название: Регистрация

Формат тела: **application/x-www-form-urlencoded**

Параметры:

* **email (string, обязательный)**

* **username (string, обязательный)**

* **password (string, обязательный)**

* **level (string, необязательный)**

Ответы:

`200 OK (application/json) — Успешная регистрация.`

`422 Validation Error — Ошибка валидации данных.`

## POST /login

Название: Вход

Формат тела: **application/x-www-form-urlencoded**

Параметры:

* **email (string, обязательный)**

* **password (string, обязательный)**

Ответы:

`200 OK (application/json) - Успешный вход.`

`422 Validation Error - Ошибка валидации.`

## GET /logout

Название: Выход

`Ответы: 200 OK (application/json).`

## GET /lang/{code}

Название: Сменить Язык

Описание: Переключение языка. Русский по умолчанию, чеченский — для своих.

Параметры пути: code (string, обязательный).

`Ответы: 200 OK, 422 Validation Error.`

# 3. Учебный модуль (Hogwards / Tasks)

## POST /hog/test/submit

Название: Проверить Тест

Описание: Принимает ответы этапа, отдаёт следующий этап или итог.

Формат тела: **application/json (объект с ответами)**

`Ответы: 200 OK, 422 Validation Error.`

## POST /hog/task/{task_id}/check

Название: Проверить Задание

Формат тела: **application/json**

Параметры пути: task_id (integer, обязательный).

`Ответы: 200 OK, 422 Validation Error.`

## POST /hog/task/{task_id}/hint

Название: Подсказка

Описание: Живая подсказка от модели по коду ученика. Без ключа — статичная из задания.

Формат тела: **application/json**

Параметры пути: task_id (integer, обязательный).

`Ответы: 200 OK, 422 Validation Error.`

# 4. Геймификация и Магазин (Shop & Wheel)

## GET /hog/wheel/state

Название: Состояние Колеса

`Ответы: 200 OK (application/json).`

## POST /hog/wheel/spin

Название: Крутить Колесо

`Ответы: 200 OK (application/json).`

## POST /hog/shop/buy/{sku}

Название: Купить

Параметры пути: sku (string, обязательный) — идентификатор товара.

`Ответы: 200 OK, 422 Validation Error.`

## POST /hog/shop/equip/{sku}

Название: Надеть

Параметры пути: sku (string, обязательный).

`Ответы: 200 OK, 422 Validation Error.`

# 5. Панель Администратора (Admin)

## POST /admin/bonus

Название: Раздать Бонус

Формат тела: **application/x-www-form-urlencoded**

Параметры:

* **amount (integer, обязательный)**

* **comment (string, необязательный)**

`Ответы: 200 OK, 422 Validation Error.`

## POST /admin/reset

Название: Сбросить Себя

Описание: Обнуляет прогресс самого админа — для повторной проверки воронки.

`Ответы: 200 OK.`

## POST /admin/reset/{user_id}

Название: Сбросить Пользователя

Параметры пути: user_id (integer, обязательный).

`Ответы: 200 OK, 422 Validation Error.`

## POST /admin/unlock

Название: Открыть Всё

Описание: Выдаёт админу весь каталог — чтобы проверить скины, не покупая по одному.

`Ответы: 200 OK.`

## POST /admin/complete

Название: Пройти Курс

Описание: Отмечает все уроки пройденными — быстрый способ увидеть конец воронки.

`Ответы: 200 OK.`

# 6. Системные запросы

## GET /health

Название: Здоровье

Описание: Проверка статуса сервера.

`Ответы: 200 OK (application/json).`
