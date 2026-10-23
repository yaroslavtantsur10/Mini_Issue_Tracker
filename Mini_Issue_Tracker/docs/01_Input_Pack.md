# 01 — Input Pack і Source Check
**Проєкт:** Mini Issue Tracker · **Тип:** практична робота · **Форма виконання:** індивідуальна · **Дата оформлення:** 23.10.2026

## Контекст і межі
Внутрішня вебсистема для невеликої команди: два Team Member та один Team Lead. MVP охоплює US-01–US-08. US-09 (attachments) — deferred, SR-10 і SR-11 (AI recommendations) — future. Не передбачено видалення issues, журналу змін, інтеграцій і повноцінного керування проєктами.

## Вимоги та семантичні AC
| US | Критерії з вихідної специфікації | Кількість |
|---|---|---:|
| US-01 Create | Ввід Title/Description; Title required; Description required; створення ID, Open, created_at, author; priority відсутній | 5 |
| US-02 View | Авторизований перегляд списку; колонки ID/Title/Status/Priority/Assignee; відкриття деталей; деталі з Description/Author/Created at; empty state | 5 |
| US-03 Assign | Один assignee; лише член команди; призначає тільки Lead; assignee видно в issue (чотири ненумеровані пункти оригіналу) | 4 |
| US-04 Priority | Low/Normal/High/Critical; редагує лише Lead | 2 |
| US-05 Progress | Поточний статус issue; статус у деталях; статус у списку | 3 |
| US-06 Comment | Непорожній текст; збереження/відображення; автор; timestamp; помилка збереження без додавання | 5 |
| US-07 Status | Початковий Open; чотири статуси; збереження зміни; тільки поточний assignee; недопустимі статуси заборонені | 5 |
| US-08 Important | High non-Closed; Critical non-Closed; виключити Low/Normal; виключити Closed | 4 |
| **Разом** | **8 US / 33 семантичні AC** | **33** |

## Бізнес-правила
- Створення: Title і Description обов'язкові; початковий status = Open; priority = Not Set (позначення відсутнього значення).
- Assignee встановлює лише Team Lead; один assignee з команди.
- Priority встановлює/змінює лише Team Lead.
- Status змінює **тільки поточний assignee**, навіть якщо Team Lead не є assignee.
- Дозволені переходи: `Open → In Progress`, `In Progress → Resolved`, `Resolved → In Progress`, `Resolved → Closed`; із Closed переходів немає.
- Important = `(High OR Critical) AND status != Closed`; Resolved включається.
- Непризначена заявка не має користувача, який може змінити її статус, поки не призначено assignee.

## Тестові дані
| ID | Status | Priority | Assignee | Important? |
|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | Так |
| ISS-002 | In Progress | High | Member B | Так |
| ISS-003 | Resolved | High | Member A | Так |
| ISS-004 | Closed | Critical | Member B | Ні |
| ISS-005 | Open | Normal | Unassigned | Ні |
| ISS-006 | Open | Not Set | Unassigned | Ні |
| ISS-007 | Resolved | Critical | Lead | Так |
| ISS-008 | In Progress | Low | Member A | Ні |

## NFR
Authentication, HTTPS, response <1 s, backup — **NOT VERIFIABLE IN STATIC FIGMA**.

## Source Check
**Джерела:** надана специфікація Mini Issue Tracker і методичні вказівки. Перевірка повноти: 8/8 US, 33/33 семантичних AC внесено в таблицю. **Це перевірка документа, а не доказ реалізації усіх AC.**

## Питання (Q-ID)
Q-01: спосіб автентифікації не деталізовано. Q-02: чи погоджено початкове Unassigned? Q-03: чи дозволено перепризначення? Q-04: як показувати недоступні дії? Q-05: чи підтверджено Apply? Q-06: чи зберігати попередню вкладку при поверненні? Статус усіх: **OPEN / потребує рішення людини**.
