# 07 — Prototype Manual Test Record (updated)

**Проєкт:** Mini Issue Tracker  
**Дата актуалізації:** 11.11.2026  
**Середовище:** Figma Design / Present; low-fidelity статичний прототип.  
**Статус документа:** часткова повторна перевірка; не є свідченням реалізації backend.

## Правила оцінювання доказів

- **PASS — observed in Present:** є підтверджене фактичне проходження інтерактивного маршруту.
- **PASS — user-reported:** студент повідомив, що перехід спрацював; скриншоти лише доповнюють його повідомлення.
- **VISUAL ONLY:** стан відображений у Figma або на зображенні, але поведінку кліка не доведено.
- **NOT VERIFIED:** немає достатнього свідчення проходження сценарію.
- **NOT VERIFIABLE IN FIGMA:** потрібна функціональність поза межами статичного прототипу.

Перелік `evidence/` нижче — назви артефактів, які студент надав для завантаження. Їх фактичну наявність і шляхи слід звірити після коміту.

## Протокол сценаріїв

| ID | Сценарій / actor | Передумови та дія | Очікуваний результат | Фактичний доказ / результат | Статус |
|---|---|---|---|---|---|
| T-01 | All ↔ Important / authenticated member | Відкрити All, натиснути Important і повернутись | Правильне перемикання списків | Наявні стани `all_issues.png`, `important_issues.png`; клік не підтверджено | VISUAL ONLY |
| T-02 | Issue list → details / member | Натиснути ISS-003 | Деталі ISS-003 | Є `issue_details.png`, навігацію не зафіксовано | VISUAL ONLY |
| T-03 | All → Create / member | Натиснути Create Issue | Відкрита форма | Є `create_default.png`; перехід не зафіксовано | VISUAL ONLY |
| T-04 | Required-field validation / member | Create з порожнім Title/Description | Помилки, заявку не створено | Є `create_validation.png`; клік не зафіксовано | VISUAL ONLY |
| T-05 | Cancel / member | Натиснути Cancel у Create | Повернення без нової заявки | Клік не зафіксовано | NOT VERIFIED |
| T-06 | Comment success / Member A | На ISS-003 у стані Comment Filled введено непорожній текст і натиснуто Add Comment | Comments (2) → Comments (3), новий запис від Member A | У розмові студент пройшов Present, показав Comments (3); згодом узгодив текст із введеним | PASS — user-reported + visual |
| T-07 | Comment success не веде до error supplement | Після виправлення Destination повторити Add Comment | Відкривається Comment Added, не Comment errors | Спочатку відкривалася сторінка помилок; після корекції користувач показав Comments (3) | PASS — user-reported + visual |
| T-08 | Important predicate / member | Перевірити дані Important | High/Critical, status != Closed; включно з Resolved | `important_issues.png`; статичний приклад ISS-001/002/003/007 | VISUAL ONLY |
| T-09 | Дозволені статусні переходи / current assignee | Перевірити Open→In Progress→Resolved, Resolved→In Progress/Closed | Лише 4 дозволені напрямки | `role_lifecycle_updated.png` показує правило й приклад In Progress; всі кліки не пройдено | VISUAL ONLY |
| T-10 | Closed / current assignee | Відкрити Closed | Жодного вихідного переходу | `role_lifecycle_updated.png` показує Closed → None / Locked; реалізацію не перевірено | VISUAL ONLY |
| T-11 | Team Lead only / lead and member | Спробувати змінити Assignee/Priority для обох ролей | Доступно тільки Team Lead | `role_lifecycle_updated.png` демонструє ролі та перелік значень; взаємодії не перевірені | VISUAL ONLY |
| T-12 | Comment validation/save failure / member | Надіслати порожній текст або імітувати збій збереження | Без нового запису, показана помилка | `comment_errors.png` містить приклади; кліки не підтверджені | VISUAL ONLY |
| T-13 | Actual data persistence | Перезавантажити та перевірити запис у БД | Реальне збереження | Не входить у статичний Figma-прототип | NOT VERIFIABLE IN FIGMA |
| T-14 | Auth, security, performance | Перевірити NFR (auth, HTTPS, backup, response time) | Відповідність реальному застосунку | Figma wireframes цього не підтверджують | NOT VERIFIABLE IN FIGMA |
| T-15 | Create success / Member A | У стані Create Issue — Filled натиснути Create | ISS-009, Open, Not Set, Unassigned, Author, Created at | Студент повідомив про налаштований перехід; `create_success.png` показує підготовлений результат. Окремого підтвердженого запису фактичного переходу немає | VISUAL ONLY; INTERACTION NOT FULLY VERIFIED |
| T-16 | Back from newly created issue / member | На ISS-009 натиснути ← All Issues | Повернутись у список | Повернення не підтверджено | NOT VERIFIED |
| T-17 | List consistency after creation / member | Повернутися до All після ISS-009 | ISS-009 присутня в актуалізованому списку | Окремого state списку після Create не показано | NOT VERIFIED |

## Оновлені артефакти / evidence

| Файл | Видимий факт | Межа доказу |
|---|---|---|
| `evidence/create_success.png` | Підготовлений стан ISS-009 після Create: Open, Not Set, Unassigned | Не доводить справжнього запису в БД чи переходу |
| `evidence/comment_filled.png` | Введений непорожній коментар до натискання | Не доводить успішного збереження |
| `evidence/comment_added.png` | Підготовлений екран Comments (3); у чаті показано оновлену версію | Звірити наявний PNG із останньою редакцією Figma |
| `evidence/role_lifecycle_updated.png` | Рольові приклади, In Progress → Resolved, Closed без переходів; допустимі Priority/Assignee | Не доводить функціонування dropdown або рольових блокувань у Present |

**Інші попередні evidence:** `all_issues.png`, `important_issues.png`, `empty_state.png`, `create_default.png`, `create_validation.png`, `issue_details.png`, `role_lifecycle.png`, `comment_errors.png`, `reusable_components.png`.

## Дефекти та відкриті питання

| ID | Зауваження | Стан / наступна перевірка |
|---|---|---|
| DF-01 | Початковий Create Success не був показаний | Додані Create Filled та ISS-009; перевірити і записати клік у Present від стартового стану |
| DF-02 | Порожній коментар переходив у success | Додано Comment Filled; виправлено Destination, після чого показано Comments (3) |
| DF-03 | Вигляд третього коментаря відрізнявся | Текст/автора/дату виправлено у Figma; візуальну остаточну звірку експорту ще виконати |
| DF-04 | Відсутні In Progress і Closed приклади | Додані статичні role/lifecycle examples; поведінку лишено NOT VERIFIED |
| DF-05 | Не було повного меню Priority та Assignee | Додані референсні списки дозволених значень; взаємодія меню й застосування змін не перевірені |
| DF-06 | Невизначений D-06 (Apply чи immediate update) | Потребує рішення/узгодження людини, не позначати APPROVED без підтвердження |

## Висновок

Додано матеріали для створення issue, позитивного коментаря та прикладів рольових обмежень. Перевірка прототипу **часткова**: позитивний сценарій коментаря показано після виправлення маршруту, інші сценарії з відсутнім інтерактивним доказом залишаються VISUAL ONLY або NOT VERIFIED. Наявність screen state не доводить реального збереження, умовної логіки чи авторизації.

**Наступна дія перед здаванням:** додати актуальний `comment_added` screenshot (із третім коментарем) і за можливості перевірити T-15–T-17 у Present, записавши дату, кроки й точний результат. Не змінювати статуси на PASS без фактичної перевірки.
