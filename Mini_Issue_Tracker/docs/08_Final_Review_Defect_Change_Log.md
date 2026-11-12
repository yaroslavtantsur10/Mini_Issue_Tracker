# 08 — Final Review, Defect & Change Log

**Проєкт:** Mini Issue Tracker  
**Версія:** 2.3 (етап 10 — відтворювані тести та фінальна звірка)  
**Дата огляду:** 2026-11-12 (ручні тести 2026-11-11)  
**Підсумковий статус:** `NOT READY — FULL VERIFICATION AND APPROVAL PENDING`

## 1. Межа огляду та рівень довіри

Джерела: `SD_Spec.docx` (§3, §5, §8), наявні в цій сесії файли `02`, `03`, `04`, `05`, `07`, попередній публічний `08`, скриншоти з evidence ZIP та опис етапів 1–7. У новому чаті заявлено створення `03` v2.1, `02/04` v2.0 та інших файлів, але **їх фактичні байти не додані до цієї розмови**. Тому незалежна перевірка саме цих версій і `T-201–T-228` наразі неможлива. Локально доступний `03` має власні `TR-*`, і відповідність між схемами не вигадувалася.

**Рівні:** `DOCUMENTED` — наявний текст/план; `VISUAL` — evidence state; `USER-REPORTED` — свідчення студента; `NOT TESTED` — клік не задокументовано; `APPROVED` — лише фактичне людське підтвердження.

## 2. Підсумок трьох критеріїв викладача

| Критерій | Оцінка | Пояснення |
|---|---|---|
| Відповідність методичним вимогам | PARTIAL | Є artifacts і traceability, але human gates та регресійна evidence неповні |
| Повнота | DOCUMENTED 33/33 AC; prototype incomplete | PT-01–21 розроблені; PT-04/09 = PASS, PT-08 = FAIL, 18 PT ще не перевірено |
| Якість виконання | IMPROVED / RESIDUAL DEFECTS | Create, Comment, Lifecycle представлені; Відтворено FAIL порожнього коментаря; Priority/Assignee інтерактивність і D-06 відкриті |

## 3. Defect Register — 19 пунктів

| ID | Початковий дефект | Зміна / evidence | Поточний статус | Наступна дія |
|---|---|---|---|---|
| DEF-01 | 33 AC були зведені до 8 US-level зв’язків | 03 — AC-level matrix на 33 критерії | DOCUMENTED / RECHECK REQUIRED | Звірити опубліковану редакцію 03 із джерелом |
| DEF-02 | Немає повних C-ID/contracts/actions | 03 — деталізація C-ID та контрактів; локальна редакція v1.1, останній огляд GitHub повідомляє про v2.0 | DOCUMENTED / VERSION CROSS-CHECK PENDING | Звірити C-ID опублікованої редакції |
| DEF-03 | Непогоджені Q-01–06 і D-01–08 | 02/04 — обґрунтування рішень і план контролю | OPEN — HUMAN SIGN-OFF | Погодити або відхилити рішення, date/owner |
| DEF-04 | Модель зміни Assignee/Priority/Status не визначена | D-06 — Select → Apply запропоновано | OPEN — PROPOSED | Узгодити модель з фактичним прототипом |
| DEF-05 | Create Success не було показано | 11.11.2026: студент підтвердив Create Filled → ISS-009; два скриншоти Present | **PROTOTYPE ROUTE PASS (user-reported)** | Збереження до реальної БД та новий рядок All Issues не перевірені |
| DEF-06 | Після створення немає підтвердженої присутності ISS-009 у списку | Окремий стан ISS-009 | OPEN | Додати state списку або явно обмежити симуляцію |
| DEF-07 | Порожній коментар переходить до успіху | 11.11.2026: на `ISS-003 — Member A` при пустому полі після Add Comment відображено `Comment Added / Comments (3)`; повторювалося після налаштувань Prototype | **OPEN — REPRODUCED FAIL (AC-06.1 / PT-08)** | Потрібне реальне виправлення клікабельного маршруту та повторний тест; не вважати виправленим |
| DEF-08 | Comment Added показував непослідовне форматування і підпис | Третій коментар відредаговано | VISUAL REVIEW PENDING | Звірити останній comment_added.png |
| DEF-09 | Помилка збереження коментаря не перевірена кліком | Є comment_errors state | OPEN — VISUAL ONLY | PT-18 |
| DEF-10 | In Progress/Closed control examples відсутні | role_lifecycle_updated.png | VISUAL FIX / BEHAVIOR NOT TESTED | PT-14/17 |
| DEF-11 | Недостатні Priority option examples | Додано Low/Normal/High/Critical як текст | PARTIAL — NO INTERACTIVE DROPDOWN | PT-12/13 |
| DEF-12 | Недостатні Assignee menu/result examples | Додано приклади членів команди | PARTIAL — NO INTERACTIVE CHANGE | PT-10/11 |
| DEF-13 | Роль non-assignee не перевірена в інтерактиві | Матриця прав у документах/супровідному frame | OPEN — VISUAL ONLY | PT-11/13/16 |
| DEF-14 | Не перевірено всі 4 status transitions | Додано статичні lifecycle states | OPEN — VISUAL ONLY | PT-14–17 |
| DEF-15 | Important Issues не перевірено як динамічний фільтр | Існуючий fixture ISS-001/002/003/007 | VISUAL ONLY | PT-19; IT-06 для реального застосунку |
| DEF-16 | Повернення у попередню вкладку не узгоджено | D-07 PROPOSED | OPEN — HUMAN DECISION | PT-21 після узгодження |
| DEF-17 | Протокол тестування не містив повного прогону | 07 v2.3: 2 PASS, 1 FAIL, 18 NOT TESTED за підтвердженням студента і screenshot | **PARTIAL RETEST** | Решта 18 PT і жоден IT не пройдені |
| DEF-18 | AI журнал не мав Share URL | У 09 внесено https://chatgpt.com/share/6af4e0e5-4be8-83eb-94e3-e4e46b2888c2 | **DOCUMENTED LINK — PUBLIC CONTENT NEEDS USER CHECK** | Відкрити URL без авторизації та переконатися, що доступний потрібний діалог |
| DEF-19 | Різні версії документів у локальному наборі й GitHub | Підготовлено синхронізований пакет 07–09 + README | OPEN — UPLOAD/ID CROSS-CHECK | Синхронізувати фактичні 02–05 v2 і 07–09, перевірити коміт |

## 3.1. Фактична повторна перевірка 11.11.2026

| Test | Result | Фактичний доказ | Межа висновку |
|---|---|---|---|
| PT-04 / US-01 | **PASS — USER-REPORTED + SCREENSHOTS** | `Create Issue — Filled` → Create → ISS-009 (Open, Not Set, Unassigned, Member A) | Готовий Figma-демомаршрут, не database persistence та не додавання ISS-009 до All Issues |
| PT-09 / US-06 | **PASS — USER-REPORTED + SCREENSHOTS** | `Comment Filled` → Add Comment → `Comment Added`; Comments (3) із текстом та автором | Демонстраційний стан, не реальне збереження |
| PT-08 / AC-06.1 | **FAIL — USER-REPORTED + SCREENSHOTS** | Порожнє поле у `ISS-003 — Member A` → Add Comment → помилково `Comment Added / Comments (3)` | Реальний дефект інтерактивного маршруту; налаштування видно, але причина не підтверджена |

**Висновок:** задокументовано один відтворений функціональний дефект Figma-прототипу. Наявність однієї помилки не скасовує візуальне покриття 33 AC, але заважає назвати прототип повністю перевіреним. Інші 18 PT — NOT TESTED, 7 IT — NOT RUN. Не прирівнювати тести в Figma до тестів серверної реалізації.

Докази повторного проходження, додані до комплекту: [PT-04: форма](../evidence/retest_pt04_filled.png), [PT-04: результат](../evidence/retest_pt04_result.png), [PT-09: стан успіху](../evidence/retest_pt09_result.png), [PT-08: помилковий стан](../evidence/retest_pt08_fail.png). Скриншоти підтверджують видимі стани; факт натискання — за повідомленням студента. Посилання доступні після завантаження PNG.

## 4. Change Log — document preparation ≠ repository commit

| Change | Stage | What changed | Evidence boundary |
|---|---|---|---|
| CH-01 | 1 | Заявлено 33-row traceability в `03` v2.0 | Контроль кількості заявлено у звіті іншої сесії |
| CH-02 | 2 | Заявлено Screen Contracts v2.1, C-ID, T-201–228 | Потрібен сам файл для фінальної звірки |
| CH-03 | 3 | Заявлено нові `02`/`04` із D-01–08, Q-01–06 | D залишаються NOT APPROVED |
| CH-04 | 4 | Підготовлено Figma Brief / Correction Plan | Планування, не редагування макета AI |
| CH-05 | 5 | PT-01–21 / IT-01–07 у тестовому протоколі | Звіт, не виконані тести |
| CH-06 | 6 | Повторний Final Review, перелік дефектів/ризиків | Висновок NOT READY |
| CH-07 | 7 | AI Log для нової документованої сесії | Share URL надано 11.11.2026 і вставлено в 09 |
| CH-08 | 8 | Синхронізовано `07`, `08`, `09`, README в окремому пакеті | Ці файли створено локально; GitHub автоматично не редагувався |
| CH-09 | 9 | Користувач усунув суфікси у назвах 03/07/08/09 за скриншотами GitHub | Потрібно перевірити фактичний вміст і посилання після комітів |
| CH-10 | 10 | Зафіксовано 2 PASS і 1 FAIL із ручної Figma-перевірки, оновлено 07/08/09 | Підтвердження користувача та скриншоти Present; без вигаданого backend або approval |

| CH-11 | 12.11.2026 | Повторно підготовлено комплект 07/08 v2.3 та README із Share URL; додано PNG доказів | Локальний комплект; завантаження та коміт виконує студент |

## 5. Residual Risks — 9

| ID | Risk | Owner / mitigation |
|---|---|---|
| R-01 | Реальні переходи Figma не перевірені системно | Студент: ручний PT run, доказ + дата |
| R-02 | Select → Apply суперечить/може не збігатися з поточним макетом | Власник рішення: людина, D-06 |
| R-03 | Priority options — лише референсна ілюстрація | PT-12/13, інтерактивний state або документоване обмеження |
| R-04 | Assignee options — лише референсна ілюстрація | PT-10/11 |
| R-05 | D-01–D-08 не схвалені | Human review з реальною датою, без фіктивного APPROVED |
| R-06 | Новий ISS-009 не підтверджений у списку після Create | PT-04 + список fixture |
| R-07 | Документи різних версій та схеми TR/T не синхронізовані | Звірити точні файли 02/03/04/05 перед публікацією |
| R-08 | URL зафіксовано, але його доступність/вміст для зовнішнього рецензента не підтверджені | Відкрити з приватного вікна та звірити 09 |
| R-09 | Відсутні дані про реальну реалізацію та NFR | Не видавати Figma за backend; IT-01–07 NOT RUN |

## 6. Scope and coverage control

| Story | AC count | Design evidence / test family |
|---|---:|---|
| US-01 | 5 | PT-01–04, Create Filled, ISS-009 |
| US-02 | 5 | PT-05–07, list/detail/empty |
| US-03 | 4 (source bullets) | PT-10/11, role examples |
| US-04 | 2 | PT-12/13, priority options |
| US-05 | 3 | PT-05/06, status in list/details |
| US-06 | 5 | PT-08/09/18, comments |
| US-07 | 5 | PT-04/14–17, lifecycle |
| US-08 | 4 | PT-19, Important predicate |
| **Total** | **33** | **Coverage as a plan; not 33 PASS** |

**Business rules:** status may be changed by the **current assignee only** (even a non-assignee Team Lead cannot); Priority and Assignee are Team Lead actions; allowable edges: Open→In Progress, In Progress→Resolved, Resolved→Closed/In Progress; Closed terminal. Important: `(High or Critical) and status != Closed`; Resolved High/Critical remains included. US-09 attachments deferred; AI future.

## 7. Approval and readiness gates

- [ ] Відкрити фінальні 02–05 та виконати ID cross-check: C-ID, `TR-*` ↔ `T-201–228` (якщо файл v2.1 використовується), PT-ID, IT-ID, D-ID.
- [ ] Отримати дійсні рішення щодо D-01–D-08 або чесно залишити неузгодженими.
- [ ] Завершити PT-01–21 у Figma Present: **2 PASS, 1 FAIL, 18 NOT TESTED**, виконати регресію FAIL після фактичної корекції; фіксувати actor, version, click path та evidence.
- [ ] Відобразити тільки справді виправлені дефекти як VERIFIED/CLOSED.
- [x] Додати наданий користувачем публічний ChatGPT Share URL до 09. Зовнішню доступність та повноту вмісту ще слід перевірити.
- [ ] Завантажити узгоджені файли в GitHub за коректними шляхами, перевірити links/commit.
- [ ] Якщо потрібний захист відео — додати справжнє посилання на відео.

**Final verdict:** `NOT READY` для заяви про *повністю перевірений і погоджений* прототип через відтворений FAIL PT-08, 18 неперевірених PT і неприйняті D-рішення. Документальна частина покращена, два позитивні Figma-маршрути підтверджено користувачем. Можна передавати на повторний огляд **як роботу із задокументованими обмеженнями**, не стверджуючи, що все пройшло PASS.
