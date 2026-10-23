# 02 — Screen Map та Decision Log

## Карта екранів
| ID | Екран/стан | Основний зміст |
|---|---|---|
| S-01 | Auth placeholder | Межа автентифікації, без реальної авторизації |
| S-02 | All Issues | 8 тестових issues, колонки, навігація |
| S-02-I | Important Issues | 4 issues за предикатом |
| S-02-E | Empty List | Порожній стан |
| M-01 | Create — Default | Title, Description, Create, Cancel |
| M-01-V | Create — Validation | Помилки обов'язкових полів |
| S-03 | Issue Details ISS-003 | Метадані, статус, assignee, priority, comments |
| S-03-C | Comment Added | Симуляція успішного коментаря, Comments (3) |
| SUP | Supplementary | Матриці прав/переходів, помилки коментарів |

## Навігація
All ↔ Important; All row ISS-003 → Details; Create → modal; порожні поля → Validation; Cancel → list; Details Add Comment → Comment Added. Інші зв'язки потребують окремої перевірки.

## Decision Log
| ID | Рішення | Походження | Статус |
|---|---|---|---|
| D-01 | Grayscale desktop 1440×900, tabs All/Important, Create modal | UX-рішення | Використано; без формального approval |
| D-02 | S-01 placeholder, початок демонстрації з S-02 | UX-рішення | Використано |
| D-03 | `Not Set` для відсутнього priority | Інтерпретація BR | Використано |
| D-04 | Unassigned за замовчуванням; Lead reassign | Припущення | Потребує підтвердження |
| D-05 | Disabled недоступних контролів | UX-рішення | Перевірити |
| D-06 | Select + Apply для редагування | UX-рішення | Перевірити |
| D-07 | Повернення на попередню вкладку | UX-рішення | Перевірити |
| D-08 | Статичні фікстури і наперед задані outcomes | Обмеження прототипу | Використано |

**Спосіб перевірки:** зіставлення структури екранів із вимогами специфікації. UX-рішення відокремлено від обов’язкових вимог; формального погодження окремих рішень немає.
