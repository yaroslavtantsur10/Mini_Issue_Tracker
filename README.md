# Mini Issue Tracker — UX/UI Design

Практична робота: low-fidelity wireframes та клікабельний UX/UI-прототип вебсистеми для реєстрації, перегляду й відстеження проблем.

**Figma Design:** https://www.figma.com/design/B5nr6SR4YnQztz8cmqTPaa/Untitled?node-id=0-1  
**GitHub:** https://github.com/yaroslavtantsur10/Mini_Issue_Tracker

## Release MVP

MVP: **US-01–US-08, 33 Acceptance Criteria**. Підтримуються створення, перегляд, призначення виконавця, priority, статуси, коментарі та Important Issues.

**Business rules:** Only Team Lead assigns issues or changes priority. Only the **current assignee** may change status. Permitted: `Open → In Progress`, `In Progress → Resolved`, `Resolved → In Progress`, `Resolved → Closed`; `Closed` is terminal. Important Issues: `(High | Critical) AND status != Closed`. `US-09` attachments deferred; AI classification/recommendations future scope.

## Prototype and evidence

Прототип показує окремі підготовлені стани, зокрема `Create Issue — Filled`, `ISS-009` (Create Success), `Comment Filled` / `Comment Added`, приклади `In Progress` та `Closed`. Це не робочий backend: у Figma не підтверджуються database persistence, server-side authorization, HTTPS, backup або response time.

- [Evidence screenshots](Mini_Issue_Tracker/evidence/)
- [Figma correction brief](Mini_Issue_Tracker/docs/05_Figma_Brief_v1.1.md)
- [Prototype test record — 07](Mini_Issue_Tracker/docs/07_Prototype_Test_Record.md)

## Documentation

| Document | Purpose |
|---|---|
| [01 — Input Pack](Mini_Issue_Tracker/docs/01_Input_Pack.md) | Вхідні вимоги, питання, scope |
| [02 — Screen Map & Decision Log](Mini_Issue_Tracker/docs/02_Screen_Map_Decision_Log.md) | Екрани та рішення D-01–D-08 |
| [03 — Screen Contracts & Traceability](Mini_Issue_Tracker/docs/03_Screen_Contracts_Traceability.md) | C-ID, AC-level traceability, tests |
| [04 — Plan Review](Mini_Issue_Tracker/docs/04_Plan_Review.md) | Review / checkpoints |
| [05 — Figma Brief](Mini_Issue_Tracker/docs/05_Figma_Brief_v1.1.md) | UI implementation brief |
| [06 — Generation Correction Report](Mini_Issue_Tracker/docs/06_Generation_Correction_Report.md) | Корекції макета |
| [07 — Prototype Test Record](Mini_Issue_Tracker/docs/07_Prototype_Test_Record.md) | 21 PT / 7 IT, observed vs not tested |
| [08 — Final Review / Defect / Change Log](Mini_Issue_Tracker/docs/08_Final_Review_Defect_Change_Log.md) | 19 defects, residual risks, readiness |
| [09 — AI Interaction Log](Mini_Issue_Tracker/docs/09_AI_Interaction_Log.md) | Реальна нова сесія доопрацювання |

## Current verification status (2026-11-12)

- Документально відображено **33/33 AC**, однак це не 33 пройдені тести.
- Ручне тестування 11.11.2026 (за повідомленнями студента та скриншотами): **2 PASS / 1 FAIL / 18 NOT TESTED** серед 21 PT.
- PT-04: Create ISS-009 — PASS (демонстраційний перехід). PT-09: непорожній Add Comment — PASS (демонстраційний перехід). PT-08: порожній коментар помилково відкриває Comment Added — FAIL; дефект залишається відкритим.
- IT-01–IT-07: NOT RUN — потребують реального застосунку, поза межами Figma.
- D-01–D-08, включно з `Select → Apply` (D-06), потребують людського погодження.
- Публічний діалог доопрацювання: [ChatGPT Share](https://chatgpt.com/share/6af4e0e5-4be8-83eb-94e3-e4e46b2888c2). Деталі: [09 — AI Interaction Log](Mini_Issue_Tracker/docs/09_AI_Interaction_Log.md).
- Висновок Final Review: **NOT READY for a claim of fully verified and approved prototype**. Це не означає, що попередні wireframes відсутні; недоліки стосуються переважно верифікації й погоджень.

## Recommended submission checks

Комплект призначено для повторного оцінювання як доопрацьований макет із задокументованими обмеженнями. Для повної верифікації потрібні повторне проходження PT-08 після виправлення, решта неперевірених PT та людське погодження UX-рішень. Не заявляємо повне приймання або усунення всіх дефектів.
