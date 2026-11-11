# 04 — Plan Review (G4 / Control B)

**Проєкт:** Mini Issue Tracker — UX/UI Release MVP  
**Дата огляду:** 2026-11-11  
**Версія:** 1.1 — revised review draft  
**Статус:** **NOT READY FOR APPROVAL / HUMAN REVIEW REQUIRED**  
**Тип перевірки:** AI-assisted документальний огляд; **не** незалежне погодження викладачем або розробником.

## 1. Предмет, джерела та межі огляду

- **Вихідна специфікація:** наданий текст SD_Spec, передусім §3 (BR-01–12), §5 (US-01–09/AC), §8 (остаточний Release MVP). Оригінальний файл DOCX із підтвердженими реквізитами версії у репозиторії не зафіксовано — **source version open**.
- **План:** `01_Input_Pack.md`, переглянутий `02_Screen_Map_Decision_Log.md` (v1.1) і `03_Screen_Contracts_Traceability.md` (revised draft), наявні `evidence/` та попередня перевірка викладача.
- **Scope:** **US-01–US-08**, разом **33 змістові AC**. Чотири ненумеровані пункти US-03 позначені як `US-03, AC, пункт 1–4`. US-09 Attachments — Deferred; SR-10/11 — Future.
- **Рівні висновків:** `COVERED` = вимогу простежено в **документах**, не доведено роботу Figma; `AMBIGUOUS` = опис є, але рішення / результат / стан неповний; `MISSING` = немає достатнього контракту. **`PASS` не застосовується до неперевірених кліків.**
- **Перевірка Figma:** цей огляд не підтверджує фактичну редагованість шарів, компонентність, виконання переходів або persistence; потрібен окремий Present-mode тест і реальні докази.

## 2. Підсумок перевірки правил

| Питання | Результат на рівні документів | Джерело / зауваження |
|---|---|---|
| В остаточному Release є US-01–US-08 | COVERED | §8; US-09 deferred, SR-10/11 future |
| Всі 33 AC мають окремі ID трасування | COVERED in doc 03 | UIR-01…UIR-33; **не** означає 33 тести PASS |
| При створенні заповнюють тільки Title/Description | COVERED | US-01, BR-02–04; новий ID/Open/Not Set/author/time у результаті **ще не доведені** |
| Team Lead non-assignee не може змінити Status | COVERED | BR-08, AC-07.4; негативний приклад є, фактичні права не перевіряються макетом |
| Статусні переходи: рівно чотири | COVERED; PARTIAL VISUAL EVIDENCE | BR-08.1; відсутні додаткові In Progress / Closed option examples |
| `Resolved` не дорівнює `Closed` | COVERED | BR-09.1, AC-08.1/2 |
| Important = High/Critical та не Closed | COVERED in fixtures | AC-08.1–4; Not Set/Low/Normal/Closed виключені |
| Not Set = відсутність priority, не п'ятий selectable level | COVERED as rule; MENU UNVERIFIED | BR-04/05; показати options |
| Порожні, validation, failed-save стани | PARTIAL | Create required показано; comment save fail та valid comment path треба доробити |
| Контракти C-ID і переходи TR-ID | COVERED as plan | Doc 03; вибір commit-моделі D-06 не закритий |
| D-01–D-08 погоджені людиною | **NOT VERIFIED** | Відсутні ім’я/роль, дата та документований результат approval |
| Prototype Present-mode тестування | **NOT VERIFIED** | Потрібен `07_Prototype_Test_Record.md` із фактичними результатами |

## 3. AC coverage matrix — всі 33 критерії

Нижче наведено **стан плану**, не факт успішного виконання в Figma. `COVERED` означає, що doc 03 описує вимогу та тест; `AMBIGUOUS` означає, що ще бракує однозначного UX-рішення або прикладу результату для демонстрації.

| Джерельний критерій | UIR | Screen/state, control | Test | Огляд плану | Що треба підтвердити |
|---|---|---|---|---|---|
| AC-01.1 Title, Description | UIR-01 | M-01; C-C01/C-C02 | PT-01 | COVERED | Поля на формі |
| AC-01.2 Title required | UIR-02 | M-01-V; C-C01/C-C03 | PT-02 | COVERED | Validation без створення |
| AC-01.3 Description required | UIR-03 | M-01-V; C-C02/C-C03 | PT-03 | COVERED | Validation без створення |
| AC-01.4 New ID, Open, created_at, author | UIR-04 | S-03-N planned | PT-04 | AMBIGUOUS | Valid Create → нова issue, а не ISS-003 |
| AC-01.5 New priority absent | UIR-05 | S-03-N planned | PT-04 | AMBIGUOUS | Нову issue показано з Not Set |
| AC-02.1 View issue list | UIR-06 | S-02; C-L01 | PT-05 | COVERED | Відкриття списку |
| AC-02.2 List ID/Title/Status/Priority/Assignee | UIR-07 | S-02, S-02-I | PT-05 | COVERED | Поля видно, assignee коли є |
| AC-02.3 Open selected issue | UIR-08 | S-02 → S-03; C-L03 | PT-06 | COVERED | Реальний click у Present |
| AC-02.4 Details: ID/Title/Description/Status/Priority/Assignee/Author/Created at | UIR-09 | S-03 | PT-06 | COVERED | Усі поля для обраної issue |
| AC-02.5 Empty issue list | UIR-10 | S-02-E | PT-07 | COVERED | Порожній стан |
| US-03 AC пункт 1: single assignee | UIR-11 | S-03, SUP-A planned; C-D02 | PT-10 | AMBIGUOUS | Select із одним team member |
| US-03 AC пункт 2: team member only | UIR-12 | S-03, SUP-A planned; C-D02 | PT-10 | AMBIGUOUS | Допустимий набір options |
| US-03 AC пункт 3: Team Lead only | UIR-13 | S-03, SUP; C-D02/D03 | PT-11 | AMBIGUOUS | Заборонено non-Lead; спосіб commit D-06 |
| US-03 AC пункт 4: current assignee visible | UIR-14 | S-03, SUP-A planned | PT-10 | AMBIGUOUS | Результат assignment/reassignment |
| AC-04.1 Priority levels 4 | UIR-15 | S-03, SUP-A planned; C-D04 | PT-12 | AMBIGUOUS | Розкрите меню із 4 values |
| AC-04.2 Only Lead updates priority | UIR-16 | S-03, SUP; C-D04/D05 | PT-13 | AMBIGUOUS | Заборонено non-Lead; D-06 |
| AC-05.1 Current status for each issue | UIR-17 | S-02 | PT-05 | COVERED | Статус на кожному рядку |
| AC-05.2 Status in details | UIR-18 | S-03 | PT-06 | COVERED | Поточний статус видимий |
| AC-05.3 Status in list | UIR-19 | S-02, S-02-I | PT-05 | COVERED | Статус у списку |
| AC-06.1 Non-empty comment | UIR-20 | S-03; C-D08/D09 | PT-08 | AMBIGUOUS | Empty → помилка, не success |
| AC-06.2 Saved comment shown | UIR-21 | S-03-CF planned → S-03-C | PT-09 | AMBIGUOUS | Введений текст перед success |
| AC-06.3 Comment author | UIR-22 | S-03-C | PT-09 | COVERED | Відповідний автор у записі |
| AC-06.4 Comment date/time | UIR-23 | S-03-C | PT-09 | COVERED | Час у записі |
| AC-06.5 Failed save creates nothing + error | UIR-24 | S-03-CE planned | PT-18 | AMBIGUOUS | Error без нового comment |
| AC-07.1 New issue has Open | UIR-25 | S-03-N planned | PT-04 | AMBIGUOUS | New Issue Details після Create |
| AC-07.2 Four allowed statuses | UIR-26 | S-03, SUP-S planned | PT-14 | AMBIGUOUS | Розкладка options для кожного стану |
| AC-07.3 New status persists on revisit | UIR-27 | S-03, SUP-S planned; C-D06/D07 | PT-15 | AMBIGUOUS | Predefined outcome + revisit; реальне persistence не доведено |
| AC-07.4 Non-assignee cannot update | UIR-28 | S-03, SUP; C-D06/D07 | PT-16 | COVERED | Role-state example, не серверні права |
| AC-07.5 Undefined status rejected | UIR-29 | S-03, SUP-S planned | PT-17 | AMBIGUOUS | Не показувати недопустимі options |
| AC-08.1 High non-Closed in Important | UIR-30 | S-02-I; C-L02 | PT-19 | COVERED | Зіставити дані All/Important |
| AC-08.2 Critical non-Closed in Important | UIR-31 | S-02-I; C-L02 | PT-19 | COVERED | Resolved включено |
| AC-08.3 Low/Normal absent | UIR-32 | S-02-I; C-L02 | PT-19 | COVERED | Виключення в fixture |
| AC-08.4 Closed excluded at any priority | UIR-33 | S-02-I; C-L02 | PT-19 | COVERED | Closed немає навіть High/Critical |

**Підсумок матриці:** **18 COVERED, 15 AMBIGUOUS, 0 MISSING** у **плані** (33/33 рядки). Навіть `COVERED` не підтверджує `PASS` у прототипі. Після доопрацювання станів та незалежного review потрібно переглянути статуси, не переписуючи історію перевірки заднім числом.

## 4. Defect / action list

| DEF-ID | Severity | Source | Plan / mockup | Дефект або ризик | Мінімальна дія | Стан |
|---|---|---|---|---|---|---|
| DEF-01 | BLOCKER | G4, D-06 | doc 02/03, S-03 | Немає визначеного моменту застосування Assignee/Priority/Status | Вибрати Select+Apply **або** immediate; узгодити control/result у 02/03/Figma | OPEN |
| DEF-02 | HIGH | AC-01.4/5, AC-07.1 | M-01-F → S-03-N | Не продемонстровано валідний Create і результат нової issue | Зробити prefilled form, new details, переходи | OPEN |
| DEF-03 | HIGH | AC-06.1–5 | S-03/S-03-CF/C/CE | Порожній comment може вести до saved state; бракує failed save | Додати filled/empty/failure branches | OPEN |
| DEF-04 | HIGH | BR-08.1, AC-07.2/5 | SUP-S | Немає наочних In Progress і Closed option examples | Додати компактні state examples | OPEN |
| DEF-05 | HIGH | US-03, AC-04.1/2 | SUP-A | Неповний evidence set Assignee/Priority options і результатів | Додати menus та before/after | OPEN |
| DEF-06 | BLOCKER | G4 Control B | doc 02 D-01–D-08 | Рішення не засвідчені людиною | Записати автора/дату/обраний варіант; зовнішнє погодження окремо | OPEN |
| DEF-07 | HIGH | G6 / methodology | 07 Prototype Test Record | Не зафіксовані повні фактичні кліки, outcomes, evidence | Present-mode test з version та скриншотами | OPEN |
| DEF-08 | MEDIUM | AC-06.2–4 | Comment Added/Error | Непослідовні стиль коментарів і видимий count | Уніфікувати та узгодити видимі дані | OPEN |
| DEF-09 | MEDIUM | Source Check | repo | Версія вихідної SD_Spec не ідентифікована | Додати джерело/версію або явно описати її відсутність | OPEN |
| DEF-10 | MEDIUM | G2, D-07 | S-03 → list | Повернення до All/Important не затверджено/не перевірено | Погодити, зв'язати й перевірити обидва маршрути | OPEN |
| DEF-11 | MEDIUM | reporting | 09 AI Interaction Log | Відсутня відтворювана історія AI-запитів | Додати реальні посилання/запити; нову роботу логувати зараз | OPEN |

**Не вважати дефектом вимог:** відсутність конкретно кнопки `Apply` (поки сам спосіб збереження узгоджений і однозначний), або відсутність справжньої БД у навчальному клікабельному прототипі. Потрібно чесно описати межі симуляції.

## 5. Decision Log review та питання

| D-ID | Стан | Потрібна дія |
|---|---|---|
| D-01 | USED / PENDING APPROVAL | Підтвердити desktop low-fi, tabs і modal як UX рішення |
| D-02 | USED / PENDING APPROVAL | Підтвердити authentication boundary без вигаданого login |
| D-03 | USED / PENDING APPROVAL | Підтвердити Not Set як absent, 4 selectable priority |
| D-04 | PENDING | Прямо вирішити initial Unassigned і reassignment |
| D-05 | PENDING | Прямо обрати disabled або hidden для недоступних дій |
| D-06 | **BLOCKING** | Прямо обрати **Select+Apply** або **immediate commit**; синхронізувати документи та S-03 |
| D-07 | PENDING | Уточнити Back до попереднього list tab |
| D-08 | USED / PENDING APPROVAL | Підтвердити статичні simulated outcomes, без реального backend |

### Питання до людини перед відміткою Control B як пройденого

1. **Q-04 / D-06 (blocking):** Зміни assignee/priority/status застосовуються одразу чи після окремої кнопки `Apply`? **Рекомендований варіант для мінімального макета:** immediate commit після вибору, **лише якщо фактичний S-03 це показує або буде виправлений**. Це рекомендація, не автоматичне погодження.
2. **Q-02 / D-04 (blocking для assignment result):** Чи створюється нова issue з `Unassigned`? Чи дозволене подальше reassignment Team Lead?
3. **Q-03 / D-05:** Недоступні контроли disabled чи hidden? В обох варіантах права мають бути однакові.
4. **Q-05 / D-07:** Back з Details повертає на початкову вкладку чи завжди на All?
5. **Q-01 / D-02 та Q-06 / D-08:** Чи прийнятні boundary та simulated outcomes як формат здавання?

**Не блокують розробку продуктової логіки:** точний механізм login (якщо boundary схвалена), реальна БД/API, HTTPS/backup як окремі UI-екрани (їх і не має бути). Не потрібно додавати зовнішні функції задля закриття цих питань.

## 6. Review sign-off — заповнюється лише після фактичної перевірки

| Поле | Значення |
|---|---|
| Reviewer | **Not recorded** — потрібен реальний рецензент (викладач/розробник/інший учасник) |
| Review date | **Not recorded** |
| Reviewed artifact versions | `02` v1.1, `03` revised draft; точні commit SHA додати при погодженні |
| Accepted D-ID | **None documented yet** |
| Remaining blocking issues | DEF-01, DEF-06; також доопрацювати DEF-02/03 до фінального proof |
| Decision | **NOT APPROVED** |
| Evidence of sign-off | **Not available** |

**Авторські рішення:** студент може окремо зафіксувати власні UX-рішення датою й підставою як `AUTHOR-DECIDED`. Це **не** підміняє окреме погодження викладача, якщо воно вимагається методикою.

## 7. Мінімальний план повторної перевірки

1. **Затвердити UX-модель:** внести конкретні відповіді D-04–D-08 у doc 02; D-06 відобразити також у C-D03/C-D05/C-D07 та TR у doc 03.
2. **Допрацювати Figma:** `M-01-F → S-03-N`; `S-03-CF → S-03-C` + empty/failure; `SUP-S` (In Progress, Closed); `SUP-A` (Assignee/Priority options та outcomes).
3. **Перевірити Present mode:** тестувати valid/invalid Create, All/Important, opening/Back, role examples, permitted/denied transitions, comment success/empty/error. Зазначати `PASS` тільки для реально пройдених кроків, `STATIC ONLY` для скриншотних доказів, `NOT TESTED` для решти.
4. **Оновити журнали:** `07_Prototype_Test_Record.md`, `08_Final_Review_Defect_Change_Log.md`, `09_AI_Interaction_Log.md`; для кожної перевірки — автор, дата, версія, крок, фактичний результат, evidence link.
5. **Після людського sign-off:** зафіксувати reviewer/date/version/accepted decisions, тільки тоді змінити `Control B` на `PASSED` і відповідні артефакти на `APPROVED`.

## 8. Final review verdict

**PLAN NOT READY FOR FORMAL APPROVAL.** Контракти документально охоплюють усі **33/33 AC**, але необхідно закрити D-06 і рішення людини, показати обов’язкові позитивні/негативні стани та підтвердити прототип фактичним тестом. Цей висновок свідомо відокремлює **повноту опису** від **доведеної працездатності**.
