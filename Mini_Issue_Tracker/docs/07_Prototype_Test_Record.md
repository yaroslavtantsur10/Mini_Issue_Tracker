# 07 — Prototype Manual Test Record

**Метод:** огляд скриншотів і ручна перевірка окремих переходів у Figma Present. **Виконавець:** автор практичної роботи.  
**Правило:** PASS лише за наявності повідомлення про фактичний успішний перехід; решта — NOT VERIFIED.

| ID | Сценарій | Очікування | Статус |
|---|---|---|---|
| T-01 | All ↔ Important | Перемикання між вкладками | SCREEN EVIDENCED; INTERACTION NOT FULLY VERIFIED |
| T-02 | ISS-003 row → Details | Відкриваються деталі ISS-003 | SCREEN EVIDENCED; INTERACTION NOT FULLY VERIFIED |
| T-03 | Create → Modal | Модальне вікно | SCREEN EVIDENCED; INTERACTION NOT FULLY VERIFIED |
| T-04 | Empty required fields | Validation errors | SCREEN EVIDENCED; INTERACTION NOT FULLY VERIFIED |
| T-05 | Cancel | Повернення до списку | SCREEN EVIDENCED; INTERACTION NOT FULLY VERIFIED |
| T-06 | Add Comment → Comment Added | Comments (3), новий текст, автор, час | PASS (за повідомленням студента після виправлення) |
| T-07 | Add Comment не веде до error supplement | Немає хибного On drag/Hover | PASS (за повідомленням студента) |
| T-08 | Important predicate | Точно ISS-001/002/003/007 | PASS (visual fixture, screenshot); interaction NOT VERIFIED |
| T-09 | 4 дозволені статусні переходи | Всі працюють лише для assignee | NOT VERIFIED |
| T-10 | Заборонені переходи та Closed | Недоступні | NOT VERIFIED |
| T-11 | Lead-only assign/priority | Недоступно іншим | NOT VERIFIED |
| T-12 | Comment failure | Помилка без доданого коментаря | NOT VERIFIED |
| T-13 | Справжнє збереження даних | Збереження після refresh | NOT VERIFIABLE IN FIGMA |
| T-14 | Auth/HTTPS/backup/<1s | NFR | NOT VERIFIABLE IN FIGMA |

## Додані візуальні докази
У `evidence/` містяться 10 скриншотів: списки, empty state, модальні вікна, деталі, comment added, ролі, lifecycle і помилки коментарів. Наявність візуального стану підтверджена; поведінку кнопок перевіряють окремо.

## Як додати докази
Для T-01–T-12, де потрібна перевірка натискання, пройти сценарії у Present mode і зафіксувати фактичний результат. Не міняти NOT VERIFIED на PASS лише на підставі статичного скриншота.

## Огляд наданих зображень
| Зображення | Що підтверджує |
|---|---|
| `evidence/all_issues.png` | Список з 8 issues |
| `evidence/important_issues.png` | 4 important issues: ISS-001, 002, 003, 007 |
| `evidence/empty_state.png` | Порожній стан |
| `evidence/create_default.png` | Початковий стан Create Issue |
| `evidence/create_validation.png` | Помилки обов’язкових полів |
| `evidence/issue_details.png` | Деталі ISS-003 і два коментарі |
| `evidence/comment_added.png` | Підготовлений стан з трьома коментарями |
| `evidence/role_lifecycle.png` | Матриця ролей і чотири дозволені переходи |
| `evidence/comment_errors.png` | Приклади validation/save failure |
| `evidence/reusable_components.png` | Приклади повторно використовуваних контролів |
