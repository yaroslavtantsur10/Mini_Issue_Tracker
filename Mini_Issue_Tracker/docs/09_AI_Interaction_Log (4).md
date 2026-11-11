# 09 — AI Interaction Log | Mini Issue Tracker

**Дата укладання:** 2026-11-11  
**Версія:** 1.2 (оновлено Share URL і зафіксовано перевірку назв файлів; не історична реконструкція)  
**Тип:** журнал **нової сесії доопрацювання після зауважень викладача**, а не первинної розробки  
**Публічний ChatGPT Share URL:** https://chatgpt.com/share/6af4e0e5-4be8-83eb-94e3-e4e46b2888c2  
**GitHub:** https://github.com/yaroslavtantsur10/Mini_Issue_Tracker  
**Figma:** https://www.figma.com/design/B5nr6SR4YnQztz8cmqTPaa/Untitled?node-id=0-1

> Це документальна послідовність взаємодій, про результати яких користувач повідомив у поточній розмові. Де точні логи/оригінальні файли іншої ChatGPT-сесії недоступні, результати атрибутовано повідомленню користувача, а не незалежній перевірці. Точні часові мітки окремих повідомлень не встановлено. Жодної вигаданої історії первинної розробки чи погодження не записано.

## 1. Правила і джерела

- `SD_Spec.docx`: першоджерело BR, US-01–08 і 33 AC; US-03 містить 4 ненумеровані bullets.
- Методичні рекомендації та звіт рецензента: підстава для повторної перевірки.
- Повідомлення користувача з фактичними результатами етапів 1–7; завантажені в цей чат Markdown і screenshots.
- Публічний GitHub: поточний README має Figma link; деякі документи старіші за підготовлені чернетки.
- `PREPARED/REPORTED`: AI іншої сесії повідомив про файл; `VERIFIED FILE`: сам файл прочитано в цій сесії; `NOT TESTED`: нема фактичного проходження Present; `PROPOSED`: без людського approval.

## 2. Реєстр взаємодій (етапи 1–7)

| Етап | Мета | Фактичний витяг із запиту | AI response / prepared artifact | Human verification and limits |
|---|---|---|---|---|
| 1 — Requirements Traceability | Опрацювати відповідне зауваження | «Побудуй повну AC-level Traceability Matrix для всіх 33 критеріїв.» | AI повідомив про створення AC-level матриці з 33 AC після отримання SD_Spec.docx. **Artifact:** `03_Screen_Contracts_Traceability.md v2.0` | Повторна AC-by-AC звірка фінальної публічної версії, Figma тести |
| 2 — Screen Contracts | Опрацювати відповідне зауваження | «Для кожного екрана й стану деталізувати призначення, actors, visible data, inputs, actions, preconditions, postconditions, errors та navigation.» | За відповіддю AI: контракти, C-ID та 28 T-ID; D-06 залишено PROPOSED. **Artifact:** `03_Screen_Contracts_Traceability.md v2.1` | Фінальна версія 2.1 не вкладена в цей чат; T-ID не перевірено тут |
| 3 — Decision Log / Plan Review | Опрацювати відповідне зауваження | «Не вигадувати імен, дат погоджень або статусів APPROVED.» | За відповіддю AI: розгляд Q-01–Q-06, D-01–D-08 та Control B. **Artifact:** `02_Screen_Map_Decision_Log.md v2.0; 04_Plan_Review.md v2.0` | Human approval не надано |
| 4 — Figma Correction Plan | Опрацювати відповідне зауваження | «Врахуй, що Create Success, Comment Filled, Comment Added, приклади In Progress і Closed уже представлені в опублікованих evidence. Не пропонуй створювати їх повторно.» | За відповіддю AI: план 7 груп змін, reuse наявних screenshot states. **Artifact:** `05_Figma_Brief_v1.1.md; Figma_Correction_Plan.md` | Figma AI не редагував; click paths треба перевірити |
| 5 — Prototype Testing | Опрацювати відповідне зауваження | «Не встановлюй PASS без фактичного доказу. Якщо сценарій не перевірено, використовуй NOT TESTED.» | За відповіддю AI: PT-01–21, IT-01–07, historical comment success окремо. **Artifact:** `07_Prototype_Test_Record.md v2.0` | Нових незалежних PASS немає |
| 6 — Final Review | Опрацювати відповідне зауваження | «Не позначати дефект CLOSED, якщо є лише план виправлення без підтвердження.» | За відповіддю AI: 19 defect entries, 9 risks, фінальний статус NOT READY. **Artifact:** `08_Final_Review_Defect_Change_Log.md v2.0` | Репозиторій і нові артефакти потребують перевірки відповідності |
| 7 — AI Interaction Log | Опрацювати відповідне зауваження | «Поки я не надам Share URL, залиш поле PENDING — PUBLIC SHARE LINK.» | За відповіддю AI: журнал нової сесії з 7 етапів. **Artifact:** `09_AI_Interaction_Log.md v1.0` | Share URL надано користувачем 11.11.2026; публічна сторінка відкривається, але вміст не вдалося незалежно прочитати повністю |

### Артефакти й межі підтвердження

| Filename | Status in this review |
|---|---|
| `02_Screen_Map_Decision_Log.md` | Локальна редакція доступна; окрема описана v2.0 іншої сесії тут не вкладена |
| `03_Screen_Contracts_Traceability.md` | Локальна редакція містить 33 AC/PT-01–21/IT-01–07; окрема v2.1 не вкладена |
| `04_Plan_Review.md` | Локальна редакція доступна; версію 2.0 іншої сесії не верифіковано байтово |
| `05_Figma_Brief_v1.1.md` | Локальна редакція доступна |
| `Figma_Correction_Plan.md` | Створення reported на етапі 4; сам файл у цьому наборі не отримано |
| `07_Prototype_Test_Record.md` | Доступна попередня версія; етап 8 підготував нову редакцію |
| `08_Final_Review_Defect_Change_Log.md` | Публічна попередня редакція доступна; етап 8 підготував нову редакцію |
| `09_AI_Interaction_Log.md` | Публічна редакція v1.0 прочитана; етап 8 підготував поточне доповнення |

## 3. Етап 8 — синхронізація документів (поточний чат)

**Дата:** 2026-11-11 (точний час не фіксувався).  
**Фактичний запит користувача:** «теперь давай же сделаем 8 пункт в докс 7 и тд ну обновить»; уточнення: «я от тебя прошу».

**Мета:** не надсилати промпти до іншого чату, а безпосередньо створити оновлені файли `07`, `08`, `09` і README для GitHub.

**Дії AI:** перевірено доступні локальні `02–05/07`, вихідну специфікацію та публічні README/08/09; створено власні редакції `07` v2.2, `08` v2.2, `09` v1.1 і кореневий README. Збережено `NOT TESTED` для нових PT, D-01–08 не позначено APPROVED, на момент створення першої редакції Share URL ще не був наданий. Створення локальних файлів не означає автоматичної публікації у GitHub.

**Людська перевірка:** користувач повідомив, що завантажив файли до GitHub, і надав публічний Share URL. Точні шляхи/версії GitHub та нові Figma-тести ще потребують перевірки.

## 4. AI vs human responsibility

| Area | AI provided | Still requires user / reviewer |
|---|---|---|
| Requirements | AC mappings and plans | Final acceptance of current source version and IDs |
| Prototype | UX states and test instructions | Clicking in Figma Present; actual screenshots + tester/date |
| Decisions | D-01–08 proposals | Human approval/rejection and change record |
| Real app | IT-01–IT-07 cases | Implemented service; persistence/security/NFR tests if applicable |
| GitHub | Markdown package for upload | Actual upload/commit, link validation |
| ChatGPT public link | URL надано користувачем | Перевірити, що він відкриває повний потрібний діалог і не містить приватної інформації |

## 5. Public conversation link

**Share URL:** https://chatgpt.com/share/6af4e0e5-4be8-83eb-94e3-e4e46b2888c2

Перед публікацією користувач має переконатися, що в публічному чаті немає приватних даних та що URL відкриває саме розмову етапів 1–7. Посилання на іншу розмову не слід подавати як доказ неіснуючої історії.

## 6. Етап 9 — перевірка назв файлів у GitHub

**Дата:** 2026-11-11.  
**Повідомлення користувача:** посилання на актуальний GitHub-репозиторій та скриншот вмісту `Mini_Issue_Tracker/docs/`; запит: «так обнови его сам нужный давай».

**Фактичний результат зі скриншота:** після завантаження файлів у папці `docs/` співіснували `03_Screen_Contracts_Traceability (1).md` та `03_Screen_Contracts_Traceability.md`, `07_Prototype_Test_Record (1).md` та `07_Prototype_Test_Record.md`; документи `08_Final_Review_Defect_Change_Log (1).md` і `09_AI_Interaction_Log (3).md` мали суфікси у назвах. Скриншот також містив повідомлення коміту про видалення попередньої версії `09_AI_Interaction_Log.md`. Ці дані описують стан, видимий на скриншоті, а не гарантують поточний стан репозиторію після подальших комітів.

**Корекція AI:** підготовлено цей документ під точним цільовим ім'ям `09_AI_Interaction_Log.md`, без суфікса `(3)`, із наданим користувачем публічним Share URL. Це локальне створення документа; **GitHub не було змінено автоматично**.

**Цільовий шлях у репозиторії:** `Mini_Issue_Tracker/docs/09_AI_Interaction_Log.md`.

## 7. Remaining actions

1. Перевірити публічний Share URL і його доступність для викладача; справжнє посилання вже додано до цього файлу.
2. Упевнитися, що назви і версії фінальних `02`, `03`, `04`, `05` відповідають посиланням та ID.
3. Додати ручний PT run із фактичними результатами до `07`, відобразити наслідки у `08`.
4. Підписати тільки реально погоджені рішення D-01–D-08.
5. Завантажити цей файл під **точним** ім’ям `09_AI_Interaction_Log.md` без `(3)` та перевірити GitHub URL; аналогічно усунути дублікати `(1)` у `03`, `07`, `08` після порівняння їхнього вмісту.
