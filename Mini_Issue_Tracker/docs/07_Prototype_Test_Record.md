# 07 — Prototype Test Record

**Проєкт:** Mini Issue Tracker  
**Версія:** 2.2 — фінальна документальна синхронізація (етап 8)  
**Дата:** 2026-11-11  
**Статус:** `TEST PLAN UPDATED / REGRESSION NOT COMPLETED`  
**Figma:** https://www.figma.com/design/B5nr6SR4YnQztz8cmqTPaa/Untitled?node-id=0-1

## 1. Правила доказів і межі перевірки

- `NOT TESTED`: у цій фінальній ітерації немає виконаного тесту з actor, click steps, actual result і доказом. Всі PT нижче мають цей статус для нового регресійного прогону.
- `VISUAL EVIDENCE`: наявний/повідомлений screenshot готового стану; **не** доводить натискання або роботу ролей.
- `USER-REPORTED HISTORICAL`: раніше студент у розмові повідомив про успішний Comment Filled → Comment Added у Present і показав Comments (3). Це не новий незалежний PASS.
- `IT / NOT RUN`: перевірка потребує справжнього застосунку й не може бути виконана як backend test у Figma.
- `D-06`: Select → Apply залишається **PROPOSED / NOT APPROVED**. PT-10/12/15 формулюють очікування за умови прийняття цієї моделі, а не вважають її впровадженою.

**Джерело тест-кейсів:** локально доступний `03_Screen_Contracts_Traceability.md` (33 AC, PT-01–PT-21, IT-01–IT-07), `SD_Spec.docx`, попередній `07` і додані зображення. Нова версія контрактів 2.1, яку описує журнал іншої сесії, тут не була надана як окремий файл; її ID `T-201–T-228` потребують остаточної cross-check після завантаження. Не створюємо непідтверджених відповідностей між TR-ID і T-ID.

## 2. Prototype tests — PT-01–PT-21

У колонці `Actual` відзначено **доступний попередній контекст**, а не результати нового регресійного прогону. Для завершення кожного тесту треба зафіксувати tester, дату, версію Figma, початковий frame, click path, фінальний frame і новий evidence.

| Test ID | Actor / preconditions | Steps | Expected result | Actual / prior evidence | Status |
|---|---|---|---|---|---|
| PT-01 | Authenticated user, M-01 open | Inspect form | Editable Title + Description only; Create/Cancel | New click outcome not recorded; `create_default.png` (visual, reported) | NOT TESTED |
| PT-02 | Any auth user, Title blank | Click Create | `Title is required`; issue not created in simulated route | New click outcome not recorded; `create_validation.png` (visual, reported) | NOT TESTED |
| PT-03 | Any auth user, Description blank | Click Create | Required-field error, no simulated success | New click outcome not recorded; `create_validation.png` (visual, reported) | NOT TESTED |
| PT-04 | Any auth user; both fields filled | Click Create; inspect new result | Entered text, new ID, Open, Not Set, author and timestamp; proper create route | New click outcome not recorded; `create_success.png` (ISS-009; visual, file supplied) | NOT TESTED |
| PT-05 | Auth user, issues fixture | Open All; inspect rows | All rows, required fields, per-issue current status | New click outcome not recorded; `all_issues.png` (visual, reported) | NOT TESTED |
| PT-06 | Auth user, choose ISS-003 or another fixture | Click row, inspect S-03 | Matching ID + Title, Description, Status, Priority, Assignee, Author, Created at | New click outcome not recorded; `issue_details.png` (visual, reported) | NOT TESTED |
| PT-07 | Auth user, zero-issue fixture | Open S-02-E | Empty message, no rows | New click outcome not recorded; `empty_state.png` (visual, reported) | NOT TESTED |
| PT-08 | Auth user, empty comment | Click Add Comment | Validation; comment count unchanged | New click outcome not recorded; `comment_errors.png` (visual, reported) | NOT TESTED |
| PT-09 | Auth user, nonempty comment in S-03-CF | Add Comment → success | Added text, current author, timestamp, count coherent | Historic user-reported success;  `comment_filled.png`; `comment_added.png` (visual); user reported click success in prior session | NOT TESTED |
| PT-10 | Lead; team-member choices; issue in details | Select an eligible single assignee; commit using agreed model | One current assignee shown; no non-team entries | New click outcome not recorded; `role_lifecycle_updated.png` (list of choices, visual only) | NOT TESTED |
| PT-11 | Member non-assignee / member assignee / Lead contexts | Attempt assignment | Members denied; Lead allowed regardless of assignee relationship | New click outcome not recorded; `role_lifecycle_updated.png` (role examples, visual only) | NOT TESTED |
| PT-12 | Lead, issue with Not Set or known priority | Open priority options, set a value | Only Low/Normal/High/Critical selectable; Not Set denotes absence | New click outcome not recorded; `role_lifecycle_updated.png` (choice list, visual only) | NOT TESTED |
| PT-13 | Lead vs Member, issue in details | Attempt priority update | Lead allowed; Member denied; updated value shown for Lead | New click outcome not recorded; `role_lifecycle_updated.png` (visual only) | NOT TESTED |
| PT-14 | Current assignee, Open/In Progress/Resolved/Closed fixtures | Open status options | Only BR-08.1 outgoing choices; Closed none | New click outcome not recorded; `role_lifecycle_updated.png` (status examples, visual only) | NOT TESTED |
| PT-15 | Current assignee, allowed edge | Commit change, navigate away/back in prepared prototype if possible | Updated status reflected; in fixture, visually consistent | New click outcome not recorded; `role_lifecycle_updated.png` (visual only) | NOT TESTED |
| PT-16 | Non-assignee (including Lead), or unassigned issue | Attempt status change | Disabled/denied or blocked; no changed status | New click outcome not recorded; `role_lifecycle_updated.png` (role example, visual only) | NOT TESTED |
| PT-17 | Assignee with status Closed, or invalid target candidate | Attempt prohibited transition | No status change; undefined value not selectable | New click outcome not recorded; `role_lifecycle_updated.png` (Closed example, visual only) | NOT TESTED |
| PT-18 | Auth user, nonempty comment, simulated failed save | Trigger error route | Error visible; new comment not shown; count unchanged | New click outcome not recorded; `comment_errors.png` (visual only) | NOT TESTED |
| PT-19 | Auth user; fixtures High, Critical, Low, Normal, Not Set; Open/Resolved/Closed | Switch All ↔ Important, compare rows | High+Resolved included, Critical+Closed excluded, Low/Normal/Not Set excluded; existing fixture 001/002/003/007 | New click outcome not recorded; `important_issues.png` (visual, reported) | NOT TESTED |
| PT-20 | Auth user, create open from list | Cancel | Return to list, no new issue | New click outcome not recorded; `create_default.png` (visual only) | NOT TESTED |
| PT-21 | Auth user, from Important selected row | Open details then Back | Return to previous list tab **only if D-07 approved** | New click outcome not recorded; not supplied; D-07 remains proposed | NOT TESTED |

## 3. Implementation-only tests — IT-01–IT-07

| ID | Source | Verification required | Status |
|---|---|---|---|
| IT-01 | BR-01, NFR-02 | Unauthenticated user denied access; predefined team users authorized | NOT RUN — out of Figma scope |
| IT-02 | AC-01.2/3/4/5 | Reject missing fields; generate unique ID, Open, author/date, absent initial priority; persist and reload | NOT RUN — out of Figma scope |
| IT-03 | US-03 AC bullets 2–4, AC-04.2, AC-07.4 | Tamper with requests; deny unauthorized assignment, priority, status updates | NOT RUN — out of Figma scope |
| IT-04 | BR-08.1, AC-07.3/5 | Reject all invalid transitions and unknown status; persist valid transition | NOT RUN — out of Figma scope |
| IT-05 | AC-06.2–5 | Store comment author/time; failed save creates none and returns error | NOT RUN — out of Figma scope |
| IT-06 | AC-08.1–4 | Query Important from real data: exactly High/Critical AND status != Closed | NOT RUN — out of Figma scope |
| IT-07 | NFR-01/03/04 | Measure response time under defined conditions; HTTPS-only deployment; backup of all data | NOT RUN — out of Figma scope |

## 4. Historical record — separated from new test results

| Record | Historical observation | Evidence level |
|---|---|---|
| H-01 / old T-06 | Студент повідомив, що після заповнення коментаря Add Comment відкривав Comment Added з `Comments (3)` | USER-REPORTED HISTORICAL + screenshot |
| H-02 / old T-07 | Помилкова навігація з Filled спершу вела до error state; студент змінив Destination і повторно показав результат | USER-REPORTED HISTORICAL + screenshot |
| H-03 / old T-15 | Підготовлено `Create Issue — Filled` → `ISS-009` з Open, Not Set, Author та часом; окремого журналу кліків немає | VISUAL EVIDENCE / NOT TESTED |

## 5. Evidence register and availability

У вихідному ZIP, наданому раніше в розмові, **фактично присутні** `create_success.png`, `comment_filled.png`, `role_lifecycle_updated.png`. Також користувач надавав скриншот Comment Added в розмові, але його остаточна версія у репозиторії в цій ітерації не підтверджена.

| Evidence | Shows | Limitation |
|---|---|---|
| `evidence/create_success.png` | ISS-009, дані нової заявки | Вміст підтверджено у наданому ZIP; screenshot ≠ підтверджений click |
| `evidence/comment_filled.png` | Непорожній введений коментар | Вміст підтверджено у наданому ZIP; screenshot ≠ підтверджений click |
| `evidence/comment_added.png` | Comments (3), автор, дата і новий запис | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/comment_errors.png` | Приклади помилок/валідації | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/role_lifecycle_updated.png` | In Progress, Closed, рольові й option приклади | Вміст підтверджено у наданому ZIP; screenshot ≠ підтверджений click |
| `evidence/important_issues.png` | Приклад результату High/Critical і not Closed | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/create_validation.png` | Валідація порожніх обов’язкових полів | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/all_issues.png` | Загальний список | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/empty_state.png` | Порожній список | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |
| `evidence/issue_details.png` | Поля деталей існуючої заявки | Згадано у попередніх документах; перевірити актуальність; screenshot ≠ підтверджений click |

## 6. Manual Figma Present test run — form for actual executions

Для кожного PT заповнити після натискання, не завчасно:

```text
Test ID: PT-__
Date and time / tester:
Figma version or frame URL:
Actor / role / fixture:
Start frame:
Action and click sequence:
Expected:
Actual observed:
End frame:
Evidence filename / recording URL:
Result: PASS / FAIL / BLOCKED
Defect ID if FAIL:
```

### Мінімальний регресійний маршрут

1. PT-01–04: Create form, обидві required errors, Filled → ISS-009; окремо перевірити унікальний ID лише як симуляцію.
2. PT-05–07, 19–21: All, Important, details, empty, Cancel, Back; збереження вкладки — лише за рішенням D-07.
3. PT-08–09, 18: пустий коментар → error, Filled → Added, save failure → не створено запис.
4. PT-10–13: single assignee, чотири priority, Team Lead дозволено; Member заблокований; Apply — лише якщо D-06 ухвалено.
5. PT-14–17: Open → In Progress, In Progress → Resolved, Resolved → Closed / In Progress; Closed terminal; заборони non-assignee.

## 7. AC coverage and conclusion

| US | Count of original AC | Linked PT |
|---|---:|---|
| US-01 | 5 | PT-01–04 |
| US-02 | 5 | PT-05–07 |
| US-03 | 4 ненумеровані | PT-10–11 |
| US-04 | 2 | PT-12–13 |
| US-05 | 3 | PT-05–06 |
| US-06 | 5 | PT-08–09, PT-18 |
| US-07 | 5 | PT-04, PT-14–17 |
| US-08 | 4 | PT-19 |
| **Разом** | **33** | **PT-01–21 (test design)** |

**Висновок:** тест-кейси документально охоплюють 33 AC та 21 PT; IT-01–07 окремо. **Жоден новий PASS не встановлено**. Для фінального приймання потрібні ручні фактичні результати й людські рішення; `Select → Apply` не схвалено.
