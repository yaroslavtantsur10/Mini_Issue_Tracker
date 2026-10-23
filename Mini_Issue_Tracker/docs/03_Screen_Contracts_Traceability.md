# 03 — Screen Contracts, Traceability, Permissions

## Screen Contracts
| Екран | Обов'язковий вміст | Дії / очікування | US |
|---|---|---|---|
| S-01 | Auth boundary | Лише умовний entry; не доказ login | NFR-02 |
| S-02 All | 8 issues, ID/Title/Status/Priority/Assignee | Відкрити деталі, Important, Create | US-02,05 |
| S-02-I Important | 001,002,003,007 | Перемкнути на All, відкрити issue | US-08 |
| S-02-E Empty | Повідомлення про відсутність issues | Зрозумілий empty state | US-02 |
| M-01 | Title*, Description*, Create/Cancel | Валідація порожніх полів, початкові значення | US-01 |
| S-03 Details | ID, Title, Description, Status, Priority, Assignee, Author, Created at, Comments | Перегляд, дії згідно ролі | US-02–07 |
| S-03-C | Новий коментар, author, timestamp, count 3 | Демонстрація success state без persistence | US-06 |
| SUP | Матриці та error states | Довідкові сценарії | US-03,04,06,07 |

## Permission Matrix
| Дія | Team Member не assignee | Поточний assignee | Team Lead не assignee |
|---|---|---|---|
| Створити issue | Так | Так | Так |
| Переглянути | Так | Так | Так |
| Коментувати | Так | Так | Так |
| Призначити assignee | Ні | Ні* | Так |
| Змінити priority | Ні | Ні* | Так |
| Змінити status | Ні | Так | Ні |

`*` Якщо поточний assignee також Team Lead, Lead має право призначення/priority **через роль Lead**. Для статусу важливий assignee, а не роль Lead.

## Transition Matrix
| З | До | Результат |
|---|---|---|
| Open | In Progress | Allow, assignee only |
| In Progress | Resolved | Allow, assignee only |
| Resolved | In Progress | Allow, assignee only |
| Resolved | Closed | Allow, assignee only |
| Closed | Будь-який | Deny |
| Інші переходи | — | Deny |

## Traceability
US-01 → M-01/M-01-V; US-02 → S-02/S-02-E/S-03; US-03 → S-03/SUP; US-04 → S-03/SUP; US-05 → S-02/S-03; US-06 → S-03/S-03-C/SUP; US-07 → S-03/SUP; US-08 → S-02-I.

**Статус:** наявність екрана ≠ доведений PASS AC. Реальна зміна даних і права backend — NOT VERIFIABLE у Figma.
