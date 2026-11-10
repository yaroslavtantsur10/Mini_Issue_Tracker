# 03 — Developer-Verifiable Screen Contracts, Traceability & Test Cases

**Project:** Mini Issue Tracker — Release MVP (US-01–US-08)  
**Document status:** REVISED DRAFT — needs human decision review and Figma re-test; **not APPROVED**  
**Source:** provided `SD_Spec` text, §3 (BR-01–BR-12), §5 (US/AC), §8 (Release Scope), §9; existing repository docs `02_Screen_Map_Decision_Log.md`, `07_Prototype_Test_Record.md`.  
**Version/date:** 1.1 draft / 2026-11-10. Source file version/author should be recorded once confirmed.

## 1. Scope, evidence levels and naming

- **Included:** US-01–US-08, **33 semantic acceptance criteria** = 5 + 5 + 4 + 2 + 3 + 5 + 5 + 4. US-03 has four **unnumbered source bullets**; the labels `US-03 AC пункт 1–4` below are references to bullet order, **not invented AC identifiers**.
- **Deferred:** US-09 (attachments). **Future:** SR-10, SR-11 (AI classification/priority recommendation). Do not add delete issue, history, separate priority/assignment screens, new roles, AI or attachments to MVP.
- **SOURCE:** explicitly present in specification. **DERIVED:** necessary logical consequence with source citation. **PROPOSED:** UX presentation requiring a recorded human decision. `UIR-*`, `C-*`, `TR-*`, `PT-*` are **local document IDs**, not source requirement IDs.
- **V** = visible/static Figma state; **P** = interaction in Figma Present; **I** = real implementation (database, server-side rights, persistence). `V/P/I` in traceability identifies **where** evidence could be obtained, not an assertion that a test passed.
- Existing Figma states: `S-01`, `S-02` (All), `S-02-I` (Important), `S-02-E` (Empty), `M-01` (Create), `M-01-V` (validation), `S-03` (ISS-003 details), `S-03-C` (Comment Added), `SUP` (reference examples). **Planned new evidence states**, not claimed already existing: `M-01-F` (filled), `S-03-N` (new issue after Create), `S-03-CF` (comment form filled), `S-03-CE` (comment save error), `SUP-S` (missing status examples), `SUP-A` (assignee/priority option and result examples). These can be small state frames, not new product screens.
- **Review rule:** Screen evidence does not prove click navigation; simulated click navigation does not prove real storage, authorization, authentication, HTTPS, backup or speed. No `PASS` is assigned in this document without a separate observed test record.

## 2. Decision dependencies (must be reconciled with doc 02)

| ID | Decision/uncertainty | Current treatment / required action |
|---|---|---|
| D-01 | Desktop grayscale; All/Important tabs; Create as modal | Existing UX convention, **used but not formally approved**. Record approval or keep PROPOSED. |
| D-02 | S-01 authentication boundary; demo begins at S-02 | Existing presentation choice; authentication mechanism remains TBD, not invented. |
| D-03 | Missing priority is displayed as `Not Set`; selectable choices only Low/Normal/High/Critical | `Not Set` display is grounded in BR-04/05; presentation still needs decision sign-off. |
| D-04 | Newly created issue `Unassigned`; Team Lead may reassign | **UNRESOLVED / needs explicit decision**. The source defines one assignee and Lead-only assignment, but does not fully define reassignment/default assignee. Do not call it a source AC. |
| D-05 | Unauthorized actions appear disabled rather than hidden | **PROPOSED**. Enforced rights derive from source irrespective of UI presentation. |
| D-06 | Select then `Apply` versus immediate update for assignee/priority/status | **BLOCKING UX decision**. Existing details frame does not clearly show Apply. Below, `commit action` is used until one model is approved and reflected consistently in Figma. |
| D-07 | Return to previous All/Important tab after Details | **PROPOSED**, verify or change the return contract. |
| D-08 | Static fixtures and predefined prototype outcomes (no real backend) | Existing scope of demonstration, distinguish simulated outcomes from real storage. |

**Source tensions not silently resolved:** BR-08 describes assignee status rights; AC-07.4 explicitly denies other users, including a Team Lead who is not the assignee. BR-09.1 includes Resolved as active for Important; `Resolved` is **not** `Closed`. The scope in §8 prevails over earlier Candidate MVP for US-09.

## 3. Screen contracts

### 3.1 S-01 — Authentication boundary (placeholder)

- **Purpose:** show authentication entry boundary, not a fabricated login flow. **Actors:** all team users. **Entry:** starting point only if demonstrating boundary; prototype may start from S-02 (D-02).
- **Visible:** product name; `Authentication entry — mechanism TBD` as annotation. No credential inputs or simulated successful security check.
- **Controls:** `C-A01` — `Continue to demo`, navigation trigger to S-02 **only if explicitly marked as prototype shortcut** (PROPOSED D-02). Do not describe as a genuine sign-in.
- **Transitions:** TR-01; **verification:** V (boundary wording), P (shortcut), I (authentication required per NFR-02/BR-01).

### 3.2 S-02 / S-02-I / S-02-E — Issues list and states

- **Purpose:** review all issues, inspect details, switch to Important. **Actors:** any authenticated team member. **Entry:** authenticated context, from S-01 demo or S-03 back; from create success if that UX path is approved.
- **Visible list fields:** `ID` required, `Title` required, `Status` required, `Priority` (`Not Set` when absent), `Assignee` (name or `Unassigned` when absent). Existing All fixture includes 8 issues. `Important` is a filtered **view of the same issues**, not a separate dataset/business module.
- **C-L01** `All` tab; enabled for all; click → S-02, TR-02. **C-L02** `Important` tab; enabled for all; click → S-02-I, TR-03. **C-L03** issue row/link; click → S-03 with *selected issue's* ID and details, TR-04. **C-L04** `Create Issue`; click → M-01 overlay, TR-05. All four are available to authenticated users (BR-01/02, US-02, US-08); tab/modal layout uses D-01.
- **S-02-I filter (SOURCE AC-08.1–4, BR-09.1):** `(priority == High || priority == Critical) && status != Closed`. `High + Resolved` included; `Critical + Closed` excluded; `Not Set` excluded as DERIVED from predicate. Fixture: ISS-001, ISS-002, ISS-003, ISS-007. Do not infer a real filter operation from a screenshot alone.
- **S-02-E empty:** no issues → clear empty state/message; no fake issue row; `Create Issue` may remain usable. **Errors:** data-load failures are not defined in source, do not assert invented messages as requirements.
- **Navigation:** TR-02/03/04/05/06/07/08/09. **Verify:** V list fields/empty/fixture/filter examples; P navigation; I real filtering/persistence after new issues and permissions.

### 3.3 M-01 / M-01-V / M-01-F — Create Issue modal

- **Actors:** authenticated Team Member or Team Lead. **Entry:** C-L04 from S-02/S-02-I. **Source:** BR-02/03/04; AC-01.1–5. Modal UI is D-01 (PROPOSED until approved).
- **C-C01** `Title` required text field; **C-C02** `Description` required multiline field. Both user-entered. **C-C03** `Create` triggers validation; on both non-empty → simulated create success TR-10 to `S-03-N` or list, choice to be fixed in UX decision; on empty Title or Description → `M-01-V` TR-11, do **not** create issue. **C-C04** `Cancel` closes without creating, TR-06. Required-field validation uses AC-01.2/3; `Title is required` appears in the source BDD example; exact wording for Description is UI copy, not source text.
- **Auto-generated/read-only on success:** unique `ID`, `status = Open`, `created_at`, `author = current user`, `priority` absent (`Not Set`). The source **does not mandate** an assignee value at creation; proposed `Unassigned` must be decided via D-04. No editable ID/status/priority/author/created_at fields in the Create form.
- **M-01-F:** non-empty example data prior to click (new supporting state). **S-03-N:** new issue results with entered Title/Description plus auto fields, separate from existing ISS-003 `Resolved` fixture; **not present/verified yet**.
- **Verify:** V validation and success states; P click path; I unique ID, generated author/time, persistence, no creation on invalid input.

### 3.4 S-03 / S-03-N — Issue Details and issue actions

- **Purpose:** one detail surface combining issue metadata, assignment, priority, status and comments; no stand-alone pages for these actions. **Actors:** any authenticated team member for view/comment; changes depend on roles/assignee. **Entry:** TR-04 from selected list row or TR-10 after create (proposed path).
- **Visible:** ID, Title, Description, Status, Priority (`Not Set` if absent), Assignee (`Unassigned` if absent), Author and Created at (AC-02.4); comments with author/time. Current existing S-03 fixture is ISS-003 `Resolved`; do not reuse it as evidence of new Create success.
- **C-D01** Back to list; TR-07. Context preservation (All vs Important) is D-07 PROPOSED.
- **C-D02** Assignee selector/list of team members (one selected, eligible team users only). **Visible view for all; editable exclusively by Team Lead**, whether or not Lead is current assignee. `C-D03` is **commit of assignee change**; exact `Apply` button vs immediate change pending D-06; after success updated current assignee appears in S-03. Reassignment is conditional on D-04. Tests PT-10/11.
- **C-D04** Priority selector; selectable set **only** `{Low, Normal, High, Critical}`; `Not Set` is display of absence, not automatically a selectable priority. **Editable exclusively by Team Lead.** `C-D05` commits priority change per approved D-06, updated priority appears in S-03; Important membership changes according to predicate. Tests PT-12/13.
- **C-D06** Status selector; editable only if **current user == current assignee** and there is an allowed outgoing transition. Set options depend on current status. **C-D07** commits valid transition per approved D-06; updated status appears. Lead/non-assignee cannot modify. No change for Closed. Tests PT-14–18.
- **C-D08** New comment text (not empty); **C-D09** Add Comment; valid success → S-03-C via TR-14, failed save → S-03-CE via TR-16, empty text → validation via TR-15. Comments list uses C-D10. Source does not prohibit comments for Closed issues, so do not introduce such a restriction.
- **Error/disabled states:** denied role-controlled actions cannot produce state change; invalid status transition cannot be selected/applied; network/save errors for actual persistence cannot be established by a Figma static state.
- **Verify:** V field visibility, option sets, role examples and comment entries; P predetermined transitions; I durable issue update, server rights and real comment save.

### 3.5 S-03-C / S-03-CF / S-03-CE / SUP — supporting evidence states

- **S-03-CF (new):** comment field contains a non-empty sample *before* Add Comment; clicking C-D09 should reach S-03-C. Existing S-03 blank field → successful saved comment **must be corrected**; the empty field belongs to the validation route (AC-06.1).
- **S-03-C (existing):** comment added with text, author, timestamp and incremented list/count **as simulation only**; ensure consistent comment formatting and matching visible count.
- **S-03-CE (new / can reuse SUP):** failed save, message, **no new entry**, unchanged count; do not represent as a saved comment.
- **SUP:** non-product annotations for permission matrix, status transition matrix, allowed priority/assignee options, deny/empty/error examples. Keep outside interactive product frame. `SUP-S` (In Progress/Closed) and `SUP-A` (options/results) may be sections of existing SUP, not full pages.
- **Verify:** V visual states, P carefully connected predefined routes (if present), I actual failure handling/author/time storage.

## 4. Control registry

| C-ID | Surface | Control/data | Source or decision | Visibility/enabled rule / outcome |
|---|---|---|---|---|
| C-A01 | S-01 | Demo entry | PROPOSED D-02 | Prototype shortcut only, not real authentication |
| C-L01 | S-02 | All tab | US-02, D-01 | All authorized users; show all issues |
| C-L02 | S-02-I | Important tab | US-08, BR-09.1, D-01 | All authorized users; apply exact predicate |
| C-L03 | S-02 | Issue row / details link | AC-02.3 | All authorized users; open selected issue |
| C-L04 | S-02 | Create Issue | BR-02, D-01 | All authorized users; opens M-01 |
| C-C01 | M-01 | Title | AC-01.1/2 | Required editable field |
| C-C02 | M-01 | Description | AC-01.1/3 | Required editable field |
| C-C03 | M-01 | Create | AC-01.2–5 | Validate then simulate success; never save invalid fields |
| C-C04 | M-01 | Cancel | PROPOSED D-01 | Close modal; no issue created |
| C-D01 | S-03 | Back | PROPOSED D-07 | Return to list; tab-context persistence TBD |
| C-D02 | S-03 | Assignee choice | US-03, BR-01 | One team member; edit Lead only |
| C-D03 | S-03 | Assignee commit | PROPOSED D-06 | Immediate vs Apply not agreed |
| C-D04 | S-03 | Priority choice | BR-04–06, AC-04.1/2 | Lead only; four selectable values |
| C-D05 | S-03 | Priority commit | PROPOSED D-06 | Immediate vs Apply not agreed |
| C-D06 | S-03 | Status choice | BR-08.1, AC-07.4/5 | Assignee only; allowed outgoing status only |
| C-D07 | S-03 | Status commit | PROPOSED D-06 | Immediate vs Apply not agreed |
| C-D08 | S-03 | New comment | AC-06.1 | Authenticated user, required non-empty text |
| C-D09 | S-03 | Add Comment | AC-06.1–5 | Validate; simulate success/error branches |
| C-D10 | S-03 | Comment list metadata | AC-06.2–4 | Author, timestamp, saved entries |
| A-L01 | S-02/S-03 | Issue metadata | AC-01.4/5, AC-02.2/4 | Visible, not all fields user-editable |
| A-L02 | SUP | Permission/transition annotations | BR-06/08.1, AC-07.4 | Reference only, not product UI |

## 5. Permission matrix — source-derived

| Action | Team Member non-assignee | Team Member assignee | Team Lead non-assignee | Team Lead assignee |
|---|---|---|---|---|
| View issue/list | Allow | Allow | Allow | Allow |
| Create issue | Allow | Allow | Allow | Allow |
| Add comment | Allow | Allow | Allow | Allow |
| Assign assignee | Deny | Deny | Allow | Allow |
| Set/change priority | Deny | Deny | Allow | Allow |
| Change issue status | Deny | Allow per transition rules | Deny | Allow per transition rules |

**Notes:** All are authenticated team users (BR-01). `assignee` is a relationship to an issue, **not a third global role**. Unassigned issue: nobody satisfies assignee rule, hence status change denied until assigned. A Team Lead who is not assignee cannot change status (AC-07.4). A Closed issue has no outgoing status transition; this does **not** independently prohibit comments, assignment or priority change. A disabled control is a visual UX choice (D-05), not proof of server authorization.

## 6. Complete status transition matrix

Current status → candidate next status; `current` is not a new transition. Only allow when user is current assignee.

| Current \ Next | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| Open | Current | **ALLOW** | Deny | Deny |
| In Progress | Deny | Current | **ALLOW** | Deny |
| Resolved | Deny | **ALLOW** | Current | **ALLOW** |
| Closed | Deny | Deny | Deny | Current |

**Allowed edges exactly:** Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed (BR-08.1). Status values cannot go beyond `{Open, In Progress, Resolved, Closed}` (AC-07.2/5).

## 7. Navigation and action transitions (TR-ID, local)

| TR-ID | From → To | Actor / condition | Trigger | Observable prototype result / rule |
|---|---|---|---|---|
| TR-01 | S-01 → S-02 | Demo visitor; D-02 | C-A01 | Demo list, **not** authenticated session proof |
| TR-02 | S-02-I → S-02 | Authenticated user | C-L01 | All Issues fixture |
| TR-03 | S-02 → S-02-I | Authenticated user | C-L02 | Same issues filtered by Important predicate |
| TR-04 | S-02 / S-02-I → S-03 | Authenticated user; row exists | C-L03 | Selected issue details, ID matches row |
| TR-05 | S-02 / S-02-I → M-01 | Authenticated user | C-L04 | Create modal opens |
| TR-06 | M-01 → prior list | Any creator | C-C04 Cancel | No new issue |
| TR-07 | S-03 → prior list | Authenticated user | C-D01 Back | Return; previous tab context is D-07 pending |
| TR-08 | S-02 → S-02-E | Fixture has zero issues | Show empty fixture | Empty list message, no row to open |
| TR-09 | S-02-E → M-01 | Authenticated user | C-L04 | Create from empty state if prototype supports it |
| TR-10 | M-01-F → S-03-N (proposed) | Valid non-empty Title/Description | C-C03 Create | New ID, Open, Not Set, author, created_at and entered text |
| TR-11 | M-01 → M-01-V | Empty Title or Description | C-C03 Create | Required errors; no new issue |
| TR-12 | S-03 → updated S-03 fixture | Team Lead, valid team assignee | C-D02 then commit C-D03 | Updated assignee visible; D-06 commit TBD |
| TR-13 | S-03 → updated S-03 fixture | Team Lead, allowed priority | C-D04 then commit C-D05 | Updated priority visible; D-06 commit TBD |
| TR-14 | S-03-CF → S-03-C | Authenticated user; non-empty comment, simulated success | C-D09 | New comment entry, author and time |
| TR-15 | S-03 empty comment → validation | Authenticated user; empty comment | C-D09 | Validation; no entry |
| TR-16 | S-03-CF → S-03-CE | Authenticated user; predefined failed save | C-D09 | Error; no added entry |
| TR-17 | S-03 → updated S-03 fixture | Current assignee, allowed status edge | C-D06 then commit C-D07 | Status changed visibly; D-06 commit TBD |
| TR-18 | S-03 → unchanged S-03 | Non-assignee / invalid edge / Closed | Attempt denied control | **No transition** and no changed status (visual example) |

**Prototype caution:** Entries TR-08–18 specify **target behavior/test cases**; they are **not confirmed as clickable in the current Figma file**. Even earlier documented interactions need re-testing and recorded evidence.

## 8. Full AC-level traceability — 33/33 coverage in specification

Column `Verification` lists possible level(s). A mapping is **coverage in the contract**, not passed implementation or proof that the Figma state exists.

| Source AC / criterion | Local UIR-ID | Screen / state | Control / annotation | Test | Verification |
|---|---|---|---|---|---|
| AC-01.1 — Title + Description inputs | UIR-01 | M-01 | C-C01, C-C02 | PT-01 | V/P |
| AC-01.2 — Title required | UIR-02 | M-01-V | C-C01, C-C03 | PT-02 | V/P/I |
| AC-01.3 — Description required | UIR-03 | M-01-V | C-C02, C-C03 | PT-03 | V/P/I |
| AC-01.4 — ID, Open, created_at, author | UIR-04 | S-03-N (planned) | A-L01 | PT-04 | V/P/I |
| AC-01.5 — priority absent on creation | UIR-05 | S-03-N (planned) | A-L01 / C-D04 | PT-04 | V/P/I |
| AC-02.1 — view registered issues | UIR-06 | S-02 | C-L01 | PT-05 | V/P/I |
| AC-02.2 — list ID/Title/Status/Priority/Assignee | UIR-07 | S-02, S-02-I | A-L01 | PT-05 | V/I |
| AC-02.3 — select issue to see details | UIR-08 | S-02 → S-03 | C-L03 | PT-06 | V/P |
| AC-02.4 — detail fields + author/date | UIR-09 | S-03 | A-L01 | PT-06 | V/I |
| AC-02.5 — empty issue list | UIR-10 | S-02-E | C-L01 / empty annotation | PT-07 | V/P |
| US-03, AC, пункт 1 — select one assignee | UIR-11 | S-03, SUP-A (planned) | C-D02 | PT-10 | V/P/I |
| US-03, AC, пункт 2 — assignee team member | UIR-12 | S-03, SUP-A (planned) | C-D02 / A-L02 | PT-10 | V/I |
| US-03, AC, пункт 3 — Lead only assignment | UIR-13 | S-03, SUP | C-D02, C-D03 / A-L02 | PT-11 | V/P/I |
| US-03, AC, пункт 4 — current assignee shown | UIR-14 | S-03, SUP-A (planned) | A-L01 | PT-10 | V/P/I |
| AC-04.1 — Low/Normal/High/Critical | UIR-15 | S-03, SUP-A (planned) | C-D04 | PT-12 | V/P/I |
| AC-04.2 — Lead only priority change | UIR-16 | S-03, SUP | C-D04, C-D05 / A-L02 | PT-13 | V/P/I |
| AC-05.1 — current status per issue | UIR-17 | S-02 | A-L01 | PT-05 | V/I |
| AC-05.2 — status in details | UIR-18 | S-03 | A-L01 | PT-06 | V/I |
| AC-05.3 — status in list | UIR-19 | S-02, S-02-I | A-L01 | PT-05 | V/I |
| AC-06.1 — comment non-empty | UIR-20 | S-03, SUP | C-D08, C-D09 | PT-08 | V/P/I |
| AC-06.2 — comment saved and shown | UIR-21 | S-03-CF → S-03-C | C-D09, C-D10 | PT-09 | V/P/I |
| AC-06.3 — comment author saved/shown | UIR-22 | S-03-C | C-D10 | PT-09 | V/I |
| AC-06.4 — comment datetime saved/shown | UIR-23 | S-03-C | C-D10 | PT-09 | V/I |
| AC-06.5 — failed save no comment + error | UIR-24 | S-03-CE (planned) | C-D09, C-D10 | PT-18 | V/P/I |
| AC-07.1 — new status Open | UIR-25 | S-03-N (planned) | A-L01 | PT-04 | V/P/I |
| AC-07.2 — four status values | UIR-26 | S-03, SUP-S (planned) | C-D06 | PT-14 | V/I |
| AC-07.3 — updated status persists/reappears | UIR-27 | S-03, SUP-S (planned) | C-D06, C-D07 | PT-15 | V/P/I |
| AC-07.4 — only current assignee can change | UIR-28 | S-03, SUP | C-D06, C-D07 / A-L02 | PT-16 | V/P/I |
| AC-07.5 — undefined status rejected | UIR-29 | S-03, SUP-S (planned) | C-D06 / A-L02 | PT-17 | V/P/I |
| AC-08.1 — High and not Closed included | UIR-30 | S-02-I | C-L02 / filter annotation | PT-19 | V/P/I |
| AC-08.2 — Critical and not Closed included | UIR-31 | S-02-I | C-L02 / filter annotation | PT-19 | V/P/I |
| AC-08.3 — Low/Normal excluded | UIR-32 | S-02-I | C-L02 / filter annotation | PT-19 | V/P/I |
| AC-08.4 — Closed excluded at any priority | UIR-33 | S-02-I | C-L02 / filter annotation | PT-19 | V/P/I |

**Derived additional Important case (not a 34th AC):** absence of priority (`Not Set`) does not satisfy High/Critical → excluded; High/Critical `Resolved` remains included because it is not `Closed` (BR-09.1 + AC-08.1/2).

## 9. Test cases — executable verification plan

**Statuses for this draft:** `SPECIFIED / NOT RETESTED` for all rows below. Existing `07_Prototype_Test_Record.md` contains some historic visual evidence and reported successes, **but this file makes no new PASS claim**. Record actual result, Figma version, evidence and tester in doc 07 after performing each test. If a planned frame is absent, record `BLOCKED — FRAME MISSING`, not PASS.

| PT-ID | Actor/context and precondition | Action | Expected visible result | Cannot establish with Figma |
|---|---|---|---|---|
| PT-01 | Authenticated user, M-01 open | Inspect form | Editable Title + Description only; Create/Cancel | Persistence |
| PT-02 | Any auth user, Title blank | Click Create | `Title is required`; issue not created in simulated route | True server validation |
| PT-03 | Any auth user, Description blank | Click Create | Required-field error, no simulated success | True server validation |
| PT-04 | Any auth user; both fields filled | Click Create; inspect new result | Entered text, new ID, Open, Not Set, author and timestamp; proper create route | Unique ID generation and persisted author/time |
| PT-05 | Auth user, issues fixture | Open All; inspect rows | All rows, required fields, per-issue current status | Real data loading/live state |
| PT-06 | Auth user, choose ISS-003 or another fixture | Click row, inspect S-03 | Matching ID + Title, Description, Status, Priority, Assignee, Author, Created at | Live data loading |
| PT-07 | Auth user, zero-issue fixture | Open S-02-E | Empty message, no rows | Database count |
| PT-08 | Auth user, empty comment | Click Add Comment | Validation; comment count unchanged | API-side validation |
| PT-09 | Auth user, nonempty comment in S-03-CF | Add Comment → success | Added text, current author, timestamp, count coherent | Actual comment save and durable metadata |
| PT-10 | Lead; team-member choices; issue in details | Select an eligible single assignee; commit using agreed model | One current assignee shown; no non-team entries | Backend membership validation and persisted assignment |
| PT-11 | Member non-assignee / member assignee / Lead contexts | Attempt assignment | Members denied; Lead allowed regardless of assignee relationship | Server-side role enforcement |
| PT-12 | Lead, issue with Not Set or known priority | Open priority options, set a value | Only Low/Normal/High/Critical selectable; Not Set denotes absence | Server enum and persistence |
| PT-13 | Lead vs Member, issue in details | Attempt priority update | Lead allowed; Member denied; updated value shown for Lead | Server-side authorization |
| PT-14 | Current assignee, Open/In Progress/Resolved/Closed fixtures | Open status options | Only BR-08.1 outgoing choices; Closed none | Server transition validation |
| PT-15 | Current assignee, allowed edge | Commit change, navigate away/back in prepared prototype if possible | Updated status reflected; in fixture, visually consistent | Persistent status after refresh/re-login |
| PT-16 | Non-assignee (including Lead), or unassigned issue | Attempt status change | Disabled/denied or blocked; no changed status | Real authorization |
| PT-17 | Assignee with status Closed, or invalid target candidate | Attempt prohibited transition | No status change; undefined value not selectable | Server rejection of invalid input |
| PT-18 | Auth user, nonempty comment, simulated failed save | Trigger error route | Error visible; new comment not shown; count unchanged | Actual network/API error handling |
| PT-19 | Auth user; fixtures High, Critical, Low, Normal, Not Set; Open/Resolved/Closed | Switch All ↔ Important, compare rows | High+Resolved included, Critical+Closed excluded, Low/Normal/Not Set excluded; existing fixture 001/002/003/007 | Dynamic backend filtering |
| PT-20 | Auth user, create open from list | Cancel | Return to list, no new issue | No backend insertion |
| PT-21 | Auth user, from Important selected row | Open details then Back | Return to previous list tab **only if D-07 approved** | Navigation context beyond prototype |

### 9.1 Implementation-only checks (not Figma PASS)

| I-ID | Source | Required implementation test |
|---|---|---|
| IT-01 | BR-01, NFR-02 | Unauthenticated user denied access; predefined team users authorized |
| IT-02 | AC-01.2/3/4/5 | Reject missing fields; generate unique ID, Open, author/date, absent initial priority; persist and reload |
| IT-03 | US-03 AC bullets 2–4, AC-04.2, AC-07.4 | Tamper with requests; deny unauthorized assignment, priority, status updates |
| IT-04 | BR-08.1, AC-07.3/5 | Reject all invalid transitions and unknown status; persist valid transition |
| IT-05 | AC-06.2–5 | Store comment author/time; failed save creates none and returns error |
| IT-06 | AC-08.1–4 | Query Important from real data: exactly High/Critical AND status != Closed |
| IT-07 | NFR-01/03/04 | Measure response time under defined conditions; HTTPS-only deployment; backup of all data |

## 10. Evidence-to-test map and rework checklist

Existing repository screenshot evidence (as documented in `07_Prototype_Test_Record.md`):

| Evidence path | Supports visually | Does **not** establish |
|---|---|---|
| `evidence/all_issues.png` | PT-05, list metadata | Rows are clickable or loaded dynamically |
| `evidence/important_issues.png` | PT-19 fixture of four issues | Dynamic filter correctness under changes |
| `evidence/empty_state.png` | PT-07 empty illustration | Actual zero-record database case |
| `evidence/create_default.png` | PT-01 form | Successful Create |
| `evidence/create_validation.png` | PT-02/03 validation illustration | Clickable validation behavior |
| `evidence/issue_details.png` | PT-06 details of ISS-003 | Created-new-issue result |
| `evidence/comment_added.png` | PT-09 prepared success **screen** | Nonempty field before click or real save |
| `evidence/role_lifecycle.png` | PT-11/14/16 rule examples | Complete In Progress/Closed control options |
| `evidence/comment_errors.png` | PT-08/18 error examples | True failed-save route / exact count coherence |
| `evidence/reusable_components.png` | Control appearances | Real Figma components, instances, Auto Layout |

**Required additions before final approval:**

1. Fill `M-01-F → S-03-N` and save screenshots; use a **new issue**, not ISS-003, with new ID/author/date and `Open / Not Set` (PT-04).
2. Fix comment flow by making `S-03-CF` contain nonempty text before success. Empty comment must go to validation; failed save must show error without new entry (PT-08/09/18).
3. Add `SUP-S` status examples for `In Progress → Resolved` and `Closed → none`, and `SUP-A` menus for assignee team members and priority four choices; show result of changes (PT-10–17).
4. Choose and explicitly approve **immediate change vs Select + Apply** (D-06) before asserting exactly how C-D03/C-D05/C-D07 work. Align Figma, docs 02/03/05 and tests.
5. Resolve D-04, D-05, D-07 with a human decision record (owner/date/approval); never mark unresolved issues approved retrospectively.
6. Walk real Figma Present paths and update `07_Prototype_Test_Record.md` with `PT-ID/TR-ID`, actor, fixture state, observed result, Figma version, screenshot/recording, tester/date; distinguish V/P/I. Keep any unexecuted action `NOT VERIFIED`.
7. Keep this document **REVISED DRAFT** until source version, decisions and re-tests are confirmed. Then mark an actual reviewed version with approver/date.

## 11. Coverage/source check

| Story | Source AC items | UIR entries | Count |
|---|---|---|---:|
| US-01 | AC-01.1–AC-01.5 | UIR-01–05 | 5 |
| US-02 | AC-02.1–AC-02.5 | UIR-06–10 | 5 |
| US-03 | AC bullets 1–4 (unnumbered) | UIR-11–14 | 4 |
| US-04 | AC-04.1–AC-04.2 | UIR-15–16 | 2 |
| US-05 | AC-05.1–AC-05.3 | UIR-17–19 | 3 |
| US-06 | AC-06.1–AC-06.5 | UIR-20–24 | 5 |
| US-07 | AC-07.1–AC-07.5 | UIR-25–29 | 5 |
| US-08 | AC-08.1–AC-08.4 | UIR-30–33 | 4 |
| **TOTAL** | | **UIR-01–33** | **33** |

**Source check:** BDD examples in US-01 clarify expected behavior, but are not counted as additional AC. Rules BR-08.1 and BR-09.1 are enforced in contracts and test scenarios. Source-linked controls and planned tests cover 33 AC, but proof is incomplete pending Figma changes, real walkthrough, and approval of UX decisions. No fake approval or fabricated PASS is claimed.
