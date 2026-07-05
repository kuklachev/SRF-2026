# ТЗ клиентского мобильного приложения «Вертикаль» — индекс

Пакет технических заданий составлен на основе:
- реестра экранов `00-screens-registry.md` и постановок `01…09-*.md`;
- контракта API `openapi.yaml` (`operationId`, схемы, коды ответов);
- шаблонов `_SCREEN_TEMPLATE.md` и `_LOGIC_TEMPLATE.md`.

Скоуп — клиентское мобильное приложение, роль «Клиент». Управление
расписанием/тренировками/инструкторами выполняется существующей
административной системой (вне скоупа, доступ только на чтение).

> **Статус открытых вопросов:** [00-OPEN-QUESTIONS-LOG.md](./00-OPEN-QUESTIONS-LOG.md)
> — 6 из 7 вопросов закрыты (релиз `0.1.1`), 1 остаётся блокером прода
> (авторизация клиента, SCR-0).

---

## 01. Экраны

| ID | Экран | Приоритет | Файл |
|----|-------|-----------|------|
| SCR-1 | Список тренировок (расписание) | Critical | [screens/SCR-1_schedule-list.md](./screens/SCR-1_schedule-list.md) |
| SCR-2 | Фильтры расписания (Bottom Sheet) | High | [screens/SCR-2_schedule-filters.md](./screens/SCR-2_schedule-filters.md) |
| SCR-3 | Карточка тренировки | Critical | [screens/SCR-3_training-details.md](./screens/SCR-3_training-details.md) |
| SCR-4 | Оформление записи | Critical | [screens/SCR-4_booking-form.md](./screens/SCR-4_booking-form.md) |
| SCR-5 | Подтверждение записи | Critical | [screens/SCR-5_booking-confirmation.md](./screens/SCR-5_booking-confirmation.md) |
| SCR-6 | Мои бронирования | Critical | [screens/SCR-6_my-bookings.md](./screens/SCR-6_my-bookings.md) |
| SCR-7 | Детали бронирования / Отмена | Critical | [screens/SCR-7_booking-details-cancel.md](./screens/SCR-7_booking-details-cancel.md) |
| SCR-8 | Уведомление об отмене тренировки | Critical | [screens/SCR-8_cancellation-notification.md](./screens/SCR-8_cancellation-notification.md) |
| SCR-9 | Оценка инструктора | Medium (Should) | [screens/SCR-9_instructor-rating.md](./screens/SCR-9_instructor-rating.md) |

## 09. Логики (сквозная бизнес-логика)

| ID | Логика | Используется в | Файл |
|----|--------|-----------------|------|
| LOGIC-001 | Статусы и бейджи брони | SCR-5, SCR-6, SCR-7, SCR-8 | [logics/LOGIC-001_status-broni.md](./logics/LOGIC-001_status-broni.md) |
| LOGIC-002 | Политика отмены (правило 2 часов) | SCR-3, SCR-7 | [logics/LOGIC-002_politika-otmeny.md](./logics/LOGIC-002_politika-otmeny.md) |
| LOGIC-003 | Push-уведомление и маршрутизация при отмене тренировки | SCR-8 | [logics/LOGIC-003_push-otmena-trenirovki.md](./logics/LOGIC-003_push-otmena-trenirovki.md) |
| LOGIC-004 | Доступность записи на тренировку | SCR-1, SCR-3, SCR-4 | [logics/LOGIC-004_dostupnost-zapisi.md](./logics/LOGIC-004_dostupnost-zapisi.md) |
| LOGIC-005 | Доступность оценки инструктора | SCR-6, SCR-9 | [logics/LOGIC-005_dostupnost-ocenki.md](./logics/LOGIC-005_dostupnost-ocenki.md) |

---

## Сквозные (для всех экранов)

- Состояния «Загрузка / Пусто / Ошибка / Успех» описаны в каждом ТЗ отдельно
  для конкретных запросов (см. секции «Состояния экрана» и «Используемые
  запросы»).
- Все запросы используют `Authorization: Bearer {токен}` — `securitySchemes.bearerAuth` в `openapi.yaml`.
- NFR-11 (адаптивная вёрстка без горизонтальной прокрутки), NFR-9 (клиент
  видит только свои данные), NFR-14 (только просмотр справочных данных),
  BR-13 (оффлайн-оплата) — сквозные ограничения, учтены во всех экранах.

## Статус открытых вопросов

Начиная с релиза `0.1.1` статус открытых вопросов больше не хранится в этом
файле как отдельный список — единственный источник правды теперь
[00-OPEN-QUESTIONS-LOG.md](./00-OPEN-QUESTIONS-LOG.md), чтобы не расходиться
с фактическими правками в файлах экранов/логик.

Кратко: из 7 исходных вопросов **6 закрыты** решениями и внесены как патчи
(релиз `0.1.1`) в соответствующие ТЗ; **1 остаётся открытым и блокирует
прод** — регистрация/авторизация клиента (SCR-0), требует ответа заказчика
о наличии существующей клиентской базы/CRM. До получения ответа разработка
и QA всех 9 экранов не блокируются (работа идёт на mock-токене).

См. трекер для деталей по каждому пункту и списка затронутых файлов.
