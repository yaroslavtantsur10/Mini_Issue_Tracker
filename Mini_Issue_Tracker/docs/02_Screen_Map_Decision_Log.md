# 02 — Screen Map, User Flows та Decision Log

**Проєкт:** Mini Issue Tracker — Release MVP (US-01–US-08)  
**Версія документа:** 1.1 — revised draft, 2026-11-10  
**Статус:** **PENDING HUMAN REVIEW / NOT APPROVED**  
**Джерела:** надана специфікація SD_Spec (§3 Business Rules, §5 US/AC, §8 Release Scope); методика G2/G4; наявний GitHub-документ `02_Screen_Map_Decision_Log.md`; оновлений `03_Screen_Contracts_Traceability.md`. Версію/дату оригінальної SD_Spec потрібно підтвердити окремо.  
**Призначення:** описати мінімальні поверхні інтерфейсу, їхні стани, переходи, права, невирішені рішення та умови ручного погодження.

> **Важливо.** `SOURCE` — вимога специфікації; `DERIVED` — логічний наслідок вимоги; `PROPOSED` — UX-рішення, яке потребує погодження; `UNRESOLVED` — відкрите питання. Статус `USED IN MOCKUP` не дорівнює `APPROVED`. Цей документ описує цільовий сценарій і доступні приклади, але не стверджує, що кліки Figma пройшли тест.

## 1. Scope і межі моделі

- **Release MVP:** US-01–US-08, 33 змістові AC. Чотири критерії US-03 у джерелі **ненумеровані** — посилання мають вигляд `US-03 AC пункт 1…4`, а не вигадані `AC-03.1…4`.
- **Deferred:** US-09 Attachments. **Future:** SR-10 категоризація AI, SR-11 рекомендації priority. Не включати ці функції до поточного макета.
- **Ролі:** Team Member та Team Lead; обидві — автентифіковані члени команди. Поточний **assignee** — окрема умова права на зміну статусу, а не третя роль.
- **Бізнес-правила:** початкові `status = Open`, `priority = Not Set` (відсутній); Team Lead призначає assignee та змінює priority; лише поточний assignee змінює status (BR-08, AC-07.4); дозволені рівно чотири статусні переходи (BR-08.1); Important = `(High OR Critical) AND status != Closed` (BR-09/09.1, AC-08.1–4).
- **Не перевіряється клікабельним макетом:** реальна автентифікація, БД/збереження між сесіями, серверна авторизація, продуктивність, безпека та резервні копії. Результати прототипу — наперед підготовлені стани (D-08, якщо погоджено).

## 2. Узгодженість ID між документами

В репозиторії уже використовуються такі назви. **Не перейменовувати наявні Figma frames без потреби**; нижче подано відповідники методики.

| ID в роботі | Тип | Назва / відповідник методики | Стан в наданих доказах |
|---|---|---|---|
| `S-01` | boundary/placeholder | Authentication boundary | Заявлено в наявному screen map |
| `S-02` | product screen / state | Issues List — All (`S-02-A`) | Наявний стан із 8 fixtures |
| `S-02-I` | state S-02 | Important Issues (`S-02-B`) | Наявний стан із 4 fixtures |
| `S-02-E` | state S-02 | Empty Issues (`S-02-C`) | Наявний приклад |
| `M-01` | modal | Create Issue — default | Наявний приклад |
| `M-01-V` | modal state | Create — validation | Наявний приклад |
| `S-03` | product screen | Issue Details, existing ISS-003 | Наявний приклад |
| `S-03-C` | state S-03 | Comment Added | Наявний приклад; маршрут потребує виправлення |
| `SUP` | review annotations | Матриці ролей, переходи та помилки | Не окрема продуктова сторінка |
| `M-01-F` | **planned** modal state | Create із непорожніми полями | Потрібно додати / перевірити |
| `S-03-N` | **planned** S-03 state | Details щойно створеної issue | Потрібно додати / перевірити |
| `S-03-CF` | **planned** S-03 state | Comment із заповненим input | Потрібно додати / перевірити |
| `S-03-CE` | **planned** S-03 state | Comment save failed | Потрібно додати / перевірити |
| `SUP-S` | **planned** review notes | In Progress / Closed states | Потрібно додати / перевірити |
| `SUP-A` | **planned** review notes | Assignee / Priority menu та результат | Потрібно додати / перевірити |

**Підсумок:** продуктові поверхні — `S-01` boundary, `S-02` list, `M-01` modal, `S-03` details (**4**). Різні frames — лише докази станів цих поверхонь, а не окремі функціональні сторінки. `SUP*` — пояснювальні annotations поза продуктовими frames.

## 3. Screen / State Inventory (G2)

| Screen / state | Purpose / actors | Entry | Visible data | Inputs / actions | Rights / states | Errors / empty | Exit | Source / D-ID |
|---|---|---|---|---|---|---|---|---|
| `S-01` Auth boundary | Позначити автентифікацію; усі ролі | Початок демонстрації, якщо потрібно | Назва, `Authentication entry — mechanism TBD` | Лише явно позначений demo shortcut, якщо використовується | **Не** симулювати справжнє підтвердження credentials | Механізм login — TBD | `S-02` у demo | BR-01, NFR authentication; D-02 PROPOSED |
| `S-02` All | Перегляд усіх issues; автентифіковані члени команди | Demo / Back / create success (останній маршрут залежить від D) | ID, Title, Status, Priority, Assignee; fixture 8 issues | All/Important tabs; open row; Create | All доступний обом ролям | Якщо немає issues — `S-02-E` | `S-02-I`, `M-01`, `S-03` | US-02, US-08, BR-02; D-01 |
| `S-02-I` Important | Перегляд важливих не-Closed; обидві ролі | Important tab | Ті самі поля, **той самий набір даних**, фільтр High/Critical AND non-Closed | All tab; open row; Create (за обраним UX) | Resolved з High/Critical входить; Closed не входить | Порожній Important можна показати як state, не новий screen | `S-02`, `S-03`, `M-01` | AC-08.1–4, BR-09.1; D-01 |
| `S-02-E` Empty | Повідомити про відсутність issues; обидві ролі | All Issues за 0 записів | Clear empty message | Create, tabs (якщо передбачено) | Не показувати фіктивний issue row | Empty state — це не серверна помилка | `M-01`, `S-02` | AC-02.5 |
| `M-01` Create default | Ввести issue; обидві ролі | Create Issue із List | Title, Description, Create, Cancel | Заповнення; Create; Cancel | Лише Title/Description вводяться; ID/author/time/status/priority система визначає після create | Відсутній Title/Description → `M-01-V` | Cancel → попередній list; валідний Create → запланований success | AC-01.1–5, BR-02/03/04; D-01 |
| `M-01-V` Create errors | Показати validation; обидві ролі | Submit з порожніми обов’язковими полями | Підписи помилок (`Title is required` з BDD прикладу) | Правка полів; Cancel; повторна спроба | Недійсні дані **не створюють** issue | Field errors | `M-01`, `M-01-F` (після заповнення) | AC-01.2/3, BDD |
| `M-01-F` **planned** | Демонструвати valid input | Заповнений `M-01` | Непорожні Title/Description | Create | Валідні поля | — | `S-03-N` за запропонованим маршрутом | AC-01.1–5; D-08 |
| `S-03` Details | Перегляд та редагування дозволених полів; обидві ролі | Click issue row | ID, Title, Description, Status, Priority, Assignee, Author, Created at, Comments | Back, assignee/priority/status controls, comment | Assignee/priority змінює тільки Lead; status — тільки поточний assignee, відповідно до allowed transitions | Disabled/hidden — UX choice D-05; save errors comments | Back → list; action success → refreshed details state | AC-02.4, US-03–07; D-04/05/06/07 |
| `S-03-N` **planned** | Новостворена issue після Create | Valid Create | **Новий** ID, введені Title/Description, Open, Not Set, Author, Created at | Back | Не підміняти ISS-003 Resolved як доказ create success | — | `S-02` | AC-01.4/5; D-08 |
| `S-03-CF` **planned** | Коментар, готовий до відправки | `S-03` із непорожнім comment input | Введений текст | Add Comment | Доступно автентифікованому члену команди | Empty input не веде до success | `S-03-C` | AC-06.1–4 |
| `S-03-C` Comment Added | Показати позитивний результат | `S-03-CF` після Add Comment | Новий коментар із author/time | Back / next actions | Mockup симулює outcome | Не починати з порожнього input | `S-03` | AC-06.2–4; D-08 |
| `S-03-CE` **planned** | Показати failed save | Failure outcome after non-empty comment | Error; новий comment **відсутній** | Retry / stay | Помилка збереження не створює comment | Save failed | `S-03` | AC-06.5 |
| `SUP`, `SUP-S`, `SUP-A` | Review annotations, **не продуктові сторінки** | Поруч із frames поза їх межами | Role matrix, allowed transitions, error/state/menu examples | Без продуктових кліків | Матриці мають відповідати BR/AC | Приклади відхилення дій | — | BR-06/08.1, AC-07.4, US-03/04 |

## 4. Таблиця навігації та дій

Тут `T-*` — **локальні ID G2**, а `TR-*` у файлі 03 — ID детальніших контрактів. Перед фінальним здаванням звірити обидва файли; назви дій і destination мають збігатися. `PLANNED / NOT TESTED` ≠ `PASS`.

| T-ID | From | Actor | Trigger | Preconditions | To / result | Source / D-ID | Evidence status |
|---|---|---|---|---|---|---|---|
| T-01 | `S-01` | Demo operator | Continue to demo | Явно підписано demo, не login | `S-02` | BR-01; D-02 | NOT TESTED |
| T-02 | `S-02` | Auth member | Important tab | — | `S-02-I`, only qualifying issues | AC-08.1–4 | NOT TESTED |
| T-03 | `S-02-I` | Auth member | All tab | — | `S-02` | AC-02.1 | NOT TESTED |
| T-04 | `S-02`/`S-02-I` | Auth member | Click issue | Issue exists | `S-03` with selected issue details | AC-02.3/4 | NOT TESTED |
| T-05 | `S-02`/`S-02-I` | Auth member | Create Issue | Auth context | `M-01` | BR-02, D-01 | NOT TESTED |
| T-06 | `M-01` | Auth member | Cancel | Any form values | Back to previous list; **no issue created** | US-01; D-01/D-07 | NOT TESTED |
| T-07 | `M-01` | Auth member | Create | Empty Title and/or Description | `M-01-V`; validation, **no create** | AC-01.2/3 | NOT TESTED |
| T-08 | `M-01-F` | Auth member | Create | Both fields filled | `S-03-N` with new ID/Open/Not Set/author/time (**proposed route**) | AC-01.1/4/5; D-08 | PLANNED |
| T-09 | `S-03` | Auth member | Back | From All/Important | Return to prior list tab if D-07 approved | AC-02.3; D-07 | NOT TESTED |
| T-10 | `S-03` | Team Lead | Choose assignee and commit | Eligible team member; interaction model D-06 decided | Updated assignee in S-03 | US-03 AC п.1–4; D-04/06 | PLANNED / menu evidence missing |
| T-11 | `S-03` | Team Lead | Choose priority and commit | Low/Normal/High/Critical; D-06 decided | Updated priority; membership in Important recalculated | AC-04.1/2, AC-08.*; D-06 | PLANNED / menu evidence missing |
| T-12 | `S-03` | Current assignee | Commit status | Open | In Progress | BR-08.1, AC-07.4 | PLANNED |
| T-13 | `S-03` | Current assignee | Commit status | In Progress | Resolved | BR-08.1, AC-07.4 | PLANNED / state evidence missing |
| T-14 | `S-03` | Current assignee | Commit status | Resolved | Closed | BR-08.1, AC-07.4 | PLANNED |
| T-15 | `S-03` | Current assignee | Commit status | Resolved | In Progress | BR-08.1, AC-07.4 | PLANNED |
| T-16 | `S-03` | Not current assignee, **including Lead if not assignee** | Attempt status edit | No permission | **No transition**, no change | AC-07.4, BR-08 | Static example; click NOT TESTED |
| T-17 | `S-03` | Current assignee | Attempt status edit | Closed | **No transition** (no outgoing edges) | BR-08.1 | PLANNED / state missing |
| T-18 | `S-03` | Auth member | Add Comment | Comment input empty | Validation; **no comment** | AC-06.1 | NOT TESTED |
| T-19 | `S-03-CF` | Auth member | Add Comment | Non-empty comment | `S-03-C` with saved-looking new entry, author/time (simulated) | AC-06.2–4; D-08 | PLANNED / input state missing |
| T-20 | `S-03-CF` | Auth member | Save fails | Non-empty comment | `S-03-CE`, visible error, **no new entry** | AC-06.5 | PLANNED |
| T-21 | `S-02` | Auth member | Open All | Dataset empty | `S-02-E` | AC-02.5 | Static example; click NOT TESTED |

**Немає переходу** для забороненої зміни priority не-Lead, assignment не-Lead, зміни status не-assignee, невалідного status або спроби вийти з Closed. Зміна вибраного значення в dropdown сама по собі **не** означає збереження, доки не визначено D-06.

## 5. Мінімальні user flows

1. **View and details:** `S-02` → вибір рядка → `S-03` → Back → `S-02` або `S-02-I` (згідно з D-07). Поля list/details відповідають AC-02.1–4; empty демонструє `S-02-E` (AC-02.5).
2. **Create — cancel/validation:** `S-02` → `M-01` → Cancel → `S-02`, **нової issue немає**. Або Create з порожніми полями → `M-01-V`, issue **не створюється**.
3. **Create — success (потребує нового доказу):** `S-02` → `M-01-F` (Title/Description заповнено) → Create → `S-03-N` (новий ID, Open, Not Set, Author, Created at) → `S-02` із новою issue. Це **predefined prototype outcome**, не справжній запис до БД.
4. **Assignment:** `S-03` як Lead → обрати **одного** team member → commit за D-06 → `S-03` із новим assignee. Non-Lead не може змінити призначення. Reassign залишається предметом D-04.
5. **Priority:** `S-03` як Lead → вибрати Low/Normal/High/Critical → commit → нове значення в details; за High/Critical та non-Closed issue входить до `S-02-I`. Для non-Lead дія заборонена. `Not Set` — display absent value, а не додатковий enum option.
6. **Status:** `S-03` як current assignee: Open → In Progress; In Progress → Resolved; Resolved → Closed **або** Resolved → In Progress. Closed не має status exit. Не-assignee (навіть Lead) не змінює status.
7. **Comment:** `S-03` із empty input → validation без нового comment; `S-03-CF` з непорожнім input → `S-03-C` із author/time; альтернативний failed save → `S-03-CE` і comment відсутній. Обидва результати — заплановані статичні прототипні приклади, не гарантія серверного збереження.
8. **Important:** `S-02` ↔ `S-02-I` із єдиною моделлю даних. High/Critical + Resolved **включити**, будь-який Closed **виключити**, Low/Normal/Not Set **виключити**.
9. **Unauthorized:** `S-03` як non-assignee → status action disabled або відхилена (після D-05) → залишається `S-03` без зміни; Lead non-assignee не є винятком.

## 6. Role / state matrix (SOURCE rules; presentation PROPOSED)

| Actor / context | View issue | Create | Comment | Assign | Set priority | Change status |
|---|---|---|---|---|---|---|
| Team Member, not assignee | Yes | Yes | Yes | **No** | **No** | **No** |
| Team Member, current assignee | Yes | Yes | Yes | **No** | **No** | **Yes**, only BR-08.1 edges |
| Team Lead, not assignee | Yes | Yes | Yes | **Yes** | **Yes** | **No** |
| Team Lead, current assignee | Yes | Yes | Yes | **Yes** | **Yes** | **Yes**, only BR-08.1 edges |

Показати заборонену дію disabled або прихованою — **D-05 PROPOSED**. Таблиця визначає **право**, не механізм серверного enforcement. Для issue без assignee немає користувача, який є current assignee: status edit недоступний, доки не визначено assignee.

| Current status | Allowed next status | No other transitions |
|---|---|---|
| Open | In Progress | Open→Resolved/Closed — ні |
| In Progress | Resolved | In Progress→Open/Closed — ні |
| Resolved | Closed **або** In Progress | Resolved→Open — ні |
| Closed | **None** | Жодних вихідних status transitions |

## 7. Decision Log — потребує реальної людської дії

**Стани:** `USED IN MOCKUP / PENDING APPROVAL` = видно або заявлено в старому макеті, **але це не схвалення**; `BLOCKING` = без вибору неможливо описати однозначний сценарій; `PENDING` = потрібна відповідь. **Немає записів `APPROVED`, оскільки підтвердження автора/дати погодження не надано.**

| ID | Запропоноване рішення (не SOURCE) | Підстава / наслідок | Статус на 2026-11-10 | Що зафіксувати для approval |
|---|---|---|---|---|
| D-01 | Desktop 1440×900, grayscale low-fi; один S-02 з All/Important tabs; Create as M-01 modal | Формат демонстрації; не додає функціональності | USED IN MOCKUP / PENDING APPROVAL | Хто затвердив, дата, версія макета |
| D-02 | S-01 тільки authentication boundary; демонстрація починається з автентифікованого S-02 | Не вигадує password/SSO | USED IN MOCKUP / PENDING APPROVAL | Підтвердження, що demo не імітує справжню auth |
| D-03 | Відсутній priority в UI = `Not Set`; selectable лише Low/Normal/High/Critical; reset не додавати | BR-04/05 визначають absent vs встановлене значення; спосіб presentation — UX | USED IN MOCKUP / PENDING APPROVAL | Підтвердження меню та UI показу |
| D-04 | Нове issue спочатку `Unassigned`; Lead може перепризначати | Source не уточнює default assignee/reassign повністю | **PENDING — explicit decision needed** | Чи обидві частини прийняті; автор/дата |
| D-05 | Недоступні role controls показувати disabled, не приховувати | UI representation; право з BR/AC не змінюється | PENDING / partly shown | Обрати disabled vs hidden; автор/дата |
| D-06 | Зміни assignee/priority/status зберігаються **або** після окремого Apply, **або** відразу після вибору; один варіант для макета | Наявний Details не показує однозначний commit | **BLOCKING** | Обрати **одну** модель, оновити S-03 і doc 03; автор/дата |
| D-07 | Back із Details повертає на ту вкладку, з якої відкрили issue | Збереження контексту навігації | PENDING / NOT TESTED | Погодити або описати інший конкретний return; автор/дата |
| D-08 | Fixture data і predefined outcomes без login/DB; усі mock successes позначаються simulated | Межа навчального прототипу | USED IN MOCKUP / PENDING APPROVAL | Погодити й зафіксувати обмеження в тест-звіті |

### Template для справжнього рішення людини (заповнювати лише після підтвердження)

| Decision ID | Final chosen text | Decision maker (name/role) | Date (YYYY-MM-DD) | Status | Evidence/link/version |
|---|---|---|---|---|---|
| D-__ | *To be filled after review* | — | — | PENDING | — |

Якщо студент як автор має повноваження обирати UX-варіант, він може **зараз** зафіксувати власне рішення як `AUTHOR-DECIDED` із реальною датою та підставою. **Не** називати це `TEACHER-APPROVED` або `DEVELOPER-APPROVED`, якщо такого погодження не було. Якщо за умовами методики потрібне окреме погодження викладача/розробника, залишити `PENDING EXTERNAL REVIEW`.

## 8. Відкриті питання / зв’язок із G1

| Q-ID | Відкрите питання | Який D-ID / наслідок | Стан |
|---|---|---|---|
| Q-01 | Чи достатня S-01 boundary без реалізації auth mechanism? | D-02; справжній механізм залишається TBD | OPEN — UX scope confirmation |
| Q-02 | Яке початкове значення assignee; чи допускається reassign? | D-04 | OPEN — explicit human decision |
| Q-03 | Disabled чи hidden для недоступних дій? | D-05 | OPEN |
| Q-04 | Момент збереження Select/Apply чи immediate? | D-06 | **BLOCKING** |
| Q-05 | Повернення до попередньої вкладки? | D-07 | OPEN |
| Q-06 | Чи прийнято prototype-only simulation та критерії її доказів? | D-08 | OPEN — scope confirmation |

> `Q-01…Q-06` тут — **локальні посилання на питання цього документа**. Перед злиттям із `01_Input_Pack.md` треба перевірити його чинні Q-ID: якщо формулювання або нумерація відрізняються, замінити посилання на фактичні ID, а не видавати їх за дослівний вміст Pack.

## 9. Що НЕ додавати до MVP

1. Окремі продуктові сторінки Assignment, Priority, Status, Comments чи dashboard: ці дії вже в `S-03`/`S-02`.
2. Attachment upload, антивірусні стани або downloads — US-09 **deferred** за фінальним Release Scope (§8), попри ранній Candidate MVP.
3. AI category / AI priority suggestions, Jira/GitHub integration, delete issue, history, нову роль Reviewer або «Approve Resolution» — не входять до Release MVP. `Resolved → Closed` може виконати поточний assignee, без вигаданої ролі.

## 10. Контроль B (G4) — чекліст перед подальшою генерацією / здаванням

- [x] Обрані мінімальні product surfaces і відокремлені від review annotations.
- [x] Описані 8 user flows і правила Important, ролей та статусів.
- [x] Planned states явно відрізнені від тих, що вже показані у fixtures.
- [ ] **D-04–D-08** та інші рішення оформлено із реальною датою, автором, доказом погодження/самостійного рішення; конфлікти закрито.
- [ ] **D-06** однозначно вибрано та синхронізовано з `03_Screen_Contracts_Traceability.md` і реальним S-03 у Figma.
- [ ] Підготовлено `M-01-F` → `S-03-N` для valid Create.
- [ ] Підготовлено `S-03-CF` → `S-03-C` і `S-03-CE` для коментарів.
- [ ] Показано In Progress/Closed, повний priority/assignee option set та результати зміни.
- [ ] Виконано Present-mode click test, записано фактичні результати в `07_Prototype_Test_Record.md`, не називаючи неперевірене PASS.
- [ ] Вказано посилання на Figma Design, Prototype і версію артефактів у README.

**Контроль B: NOT PASSED / AWAITING HUMAN REVIEW.** Цей документ — готовий план для перевірки, а не підроблене погодження. Після фактичного review змінити статус лише тих D-ID, для яких є запис автора, дати і рішення. Після цього вирівняти doc 03, Figma brief, сам макет та тест-протокол.
