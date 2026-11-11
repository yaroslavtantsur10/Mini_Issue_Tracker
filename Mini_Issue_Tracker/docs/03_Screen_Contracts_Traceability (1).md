# 03 — Developer-Verifiable Screen Contracts, AC-Level Traceability & Test Cases

**Project:** Mini Issue Tracker · **Release:** MVP (US-01–US-08)  
**Version:** 2.0 · 2026-11-11 · **Status:** REVISED DRAFT — NOT APPROVED; Figma re-test pending  
**Canonical source:** `SD_Spec(1).docx` (provided full specification), §1 (users and answers), §3 (SR-01–SR-11, BR-01–BR-12), §5 (US and AC), §8 (final Release Scope and NFR).  
**Secondary context:** current GitHub `03_Screen_Contracts_Traceability.md` (v1.1 draft, 2026-11-10), `02_Screen_Map_Decision_Log.md` and referenced `07_Prototype_Test_Record.md`; methodological guide `Mini_Issue_Tracker_UX_UI_Methodological_Guide_UA.docx`.  
**Figma:** https://www.figma.com/design/B5nr6SR4YnQztz8cmqTPaa/Untitled?node-id=0-1  
**Repository:** https://github.com/yaroslavtantsur10/Mini_Issue_Tracker

> **Verification warning.** This file is a complete **planned** mapping of 33 acceptance criteria, not evidence of 33 successful tests. Figma frames, interactions and screenshot correspondence have **not been independently re-tested for this revision**. All 33 rows have verification status `NOT VERIFIED`. Historical references from the repository are candidate evidence, not newly verified observations. Do not change to `PASS` without a dated, attributable test record and reproducible evidence. A Figma prototype cannot prove backend persistence, server authorization, real authentication, HTTPS, backup or runtime performance.

## 1. Scope, source hierarchy and conventions

1. **Release MVP** (§8): **US-01–US-08**. **Deferred:** US-09 (attachments). **Future:** SR-10 (AI categorization), SR-11 (AI priority recommendation). Earlier §4 *Candidate MVP* does not override §8. Exclude attachments, AI UI, deletion (BR-10), end-user issue change history (BR-11), integrations (KC-05), mobile app (A-07) and invented Reviewer/Approve roles.
2. **33 semantic AC:** US-01 5 + US-02 5 + US-03 4 + US-04 2 + US-05 3 + US-06 5 + US-07 5 + US-08 4. The four original **unnumbered** items for US-03 are cited as `US-03, AC, пункт 1` to `пункт 4`, reflecting their order in §5, **not** as fictitious `AC-03.x`. The US-01 BDD examples do not add new criteria.
3. **Source precedence:** `SD_Spec(1).docx` source requirements > explicitly signed human decisions (`D-*`) > derived screen contracts > existing Figma/prototype examples. `SOURCE` = stated in specification; `DERIVED` = logically necessary implication with source; `PROPOSED` = optional design choice requiring approval; `UNRESOLVED` = not decided. `UIR-*`, `C-*`, `A-*`, `TR-*`, `PT-*`, `IT-*` and `EV-*` are local IDs only.
4. **Verification levels:** `V` = inspect visible Figma frame; `P` = execute Figma Present interaction; `I` = test actual implementation. Levels describe possible tests, not proof. **Verification Status** in the 33-row matrix is `NOT VERIFIED` throughout; `N/A IN FIGMA` in evidence notes means that only an implementation can verify that aspect. Planned states may not yet exist.
5. **Evidence rule:** evidence must identify concrete Figma frame/node/version or screenshot path, tester, date, actor, preconditions, actions and observed outcome. `evidence/...` references below are **candidate historical filenames** from the repository, **not accepted PASS evidence** in this revision. Use `EV-PENDING` until checked; link a verified `EV-ID` to `07_Prototype_Test_Record.md` when executed.

## 2. Source-derived business invariants

- `BR-01`: only authenticated team users (two predefined Team Members, one Team Lead). Authentication mechanism is **not** specified; the `S-01` boundary is a design placeholder, not a login implementation.
- `BR-02`: any authenticated team user can create an issue. Create **user inputs**: Title and Description (`AC-01.1`); both required (`AC-01.2/3`). **System values**: ID, `status = Open`, `created_at`, `author` (`AC-01.4`, `BR-03`); priority initially **unset** (`AC-01.5`, `BR-04/05`). `Not Set` is a label for absence, not a fifth selectable priority or a specified DB enum/null encoding.
- `US-03` and §1 Open Questions: only Team Lead selects **one** assignee who is a team member; selected/current assignee appears in issue. Reassignment and initial assignee are **not fully specified** (D-04 unresolved).
- `BR-05/06`, `AC-04.1/2`: **only Team Lead** selects/changes priority; permitted set exactly `{Low, Normal, High, Critical}` once set. `BR-06` concerns **priority**, never assignee.
- `BR-07/08/08.1`, `AC-07.4`: statuses exactly `Open`, `In Progress`, `Resolved`, `Closed`; changes performed **only by current assignee**, regardless of global Team Lead role. Only allowed edges are `Open → In Progress`, `In Progress → Resolved`, `Resolved → In Progress`, `Resolved → Closed`. `Closed` has no outgoing **status** transition. This does not impose a general prohibition on comments or priority changes.
- `BR-09/BR-09.1`, `AC-08.1–4`: **Important** = `priority ∈ {High, Critical} AND status != Closed`. Thus `High + Resolved` and `Critical + Resolved` are included; `Critical + Closed`, Low, Normal and unset priority are excluded. `Resolved` **is not** `Closed`.
- `AC-06.1–5`: comment text nonempty; saved comment visible on its issue with saved/displayed author and creation date/time. Failed save yields error and **does not create** a comment.
- **NFR:** §8 `NFR-01` response time < 1 s; `NFR-02` authentication required; `NFR-03` HTTPS only; `NFR-04` backup of all data (attachments removed from final release's updated NFR). These need implementation/deployment checks, not new Figma product screens.

## 3. Decision log — human approval required

| ID | Proposed UX choice / open question | Source vs decision boundary | Status |
|---|---|---|---|
| D-01 | Desktop grayscale low-fi; All/Important tabs of same list; Create as modal | Presentation, not source requirement | PROPOSED — approval missing |
| D-02 | `S-01` placeholder; demo starts in already-authenticated `S-02` | Auth required, mechanism unknown | PROPOSED — approval missing |
| D-03 | Show unset priority as `Not Set`; only four selectable values; no reset | Unset state and values SOURCE; precise UI format PROPOSED | PROPOSED — approval missing |
| D-04 | New issue starts Unassigned; may Team Lead reassign an existing assignee? | §5 does not unambiguously specify both | UNRESOLVED — functional clarification |
| D-05 | Render forbidden controls disabled instead of hidden | Rights SOURCE, presentation PROPOSED | PROPOSED — approval missing |
| D-06 | Immediate commit vs explicit `Apply` after assignee/priority/status choice | Commit mechanism not an AC | **BLOCKER** — select one and sync docs/Figma |
| D-07 | Back from Details restores the prior All/Important tab | Convenience not SOURCE | PROPOSED — approval missing |
| D-08 | Predefined mock data and result states; no real DB/login | Demo-only limitation consistent with README | PROPOSED — document simulation boundaries |

**Rule:** No D-ID above is presumed APPROVED. Pending D-06, `C-D03/05/07` mean a *conceptual commit action*, **not** a verified physical `Apply` button.

## 4. Screen and state contracts

### S-01 — Authentication boundary (prototype placeholder)
- **Actors:** three predefined team users; **entry:** optional introductory frame; **exit:** `TR-01` demo shortcut, if D-02 approved. **Visible:** product name, annotation `Authentication entry — mechanism TBD`; do not fabricate password or SSO.
- **C-A01** `Continue to demo`: proposed prototype-only link to `S-02`, explicitly **not** login. `BR-01/NFR-02` can only be enforced in implementation (`IT-01`).

### S-02 (All) / S-02-I (Important) / S-02-E (Empty) — one issue list with states
- **Actors/entry:** authenticated team user, from demo or Details. **Fields per row:** ID, Title, Status, Priority (absent presented as Not Set), Assignee when assigned; unassigned display text requires D-04 approval. `AC-02.2`, `AC-05.1/3`.
- **C-L01** All tab (`TR-02`), **C-L02** Important tab (`TR-03`), **C-L03** issue row/details link (`TR-04`, must open matching issue), **C-L04** Create Issue (`TR-05`), all allowed for authenticated users. Tabs/modal are D-01 proposed.
- Important is a view of **same** issues with predicate in §2. Include reference cases: High+Resolved included; Critical+Closed excluded; Not Set excluded. Empty All state `S-02-E` contains no rows and a meaningful no-issues message (`AC-02.5`). Empty Important when no match is a design extension, not a new AC.
- **States/errors:** `S-02`, `S-02-I`, `S-02-E`; runtime loading error behavior not specified. **Verification:** static V, navigation P, live filtering/data I.

### M-01 / M-01-V / M-01-F — Create Issue
- **Entry:** C-L04; **actors:** authenticated Team Member/Lead; **visible inputs:** **C-C01** Title (required), **C-C02** Description (required); **actions:** **C-C03** Create and **C-C04** Cancel (Cancel is a proposed UI control, not a source AC).
- `M-01-V` validation: missing Title prevents creation and BDD source gives exact example **`Title is required`**. Missing Description prevents creation; error wording is not prescribed. `M-01-F` pre-submit populated example; `S-03-N` proposed result showing entered Title/Description plus auto ID/Open/created_at/author and absent priority. Do not put status/priority/ID/author/time inputs on Create.
- **Transitions:** `TR-06` Cancel; `TR-10` valid Create → `S-03-N` (post-create destination proposed); `TR-11` invalid Create → validation. **Evidence limits:** mock result cannot prove unique ID, true database insertion or account-derived author.

### S-03 / S-03-N — Issue Details and management
- **Entry:** C-L03 selected issue or valid create route. **Actors:** all authenticated users can view/comment; editing depends on role/assignee. **Visible metadata:** ID, Title, Description, Status, Priority, Assignee if set, Author, Created at (`AC-02.4`). Preserve selected record identity.
- **C-D01** Back (D-07 behavior pending); **C-D02** single assignee select, team members only (Lead edit); **C-D03** assignment commit (interaction form D-06 pending); current assignee displayed via **A-L01**.
- **C-D04** priority select `{Low, Normal, High, Critical}` (Lead edit); **C-D05** priority commit (D-06); display unset as `Not Set` (D-03 UI representation).
- **C-D06** status choices (edit exclusively by **current assignee** with allowed outgoing edge); **C-D07** status commit (D-06). `Closed` no outgoing status option. `Team Lead non-assignee` cannot change status.
- **C-D08** comment text; **C-D09** Add Comment; **C-D10** saved comments list with text, author and date/time. Empty text → validation without entry; nonempty successful save → visible entry; failed save → error **without** new entry. No unspecified Closed-comments restriction.
- **Additional display fixtures:** `S-03-CF` comment form filled, `S-03-C` saved comment, `S-03-CE` failed save; `SUP-A` assignment/priority options and resulting values; `SUP-S` all four statuses and options; `SUP` role examples. These are **planned evidence states/annotations** (not independently confirmed). Keep reviewer annotations outside product frame.

### 4.1 Control / annotation registry

| ID | Location | Control / data | Allowed users / condition | Source / decision |
|---|---|---|---|---|
| C-A01 | S-01 | Demo entry (optional) | All demo visitors; **not** authentication | D-02 |
| C-L01 | S-02 | All tab | Authenticated | AC-02.1, D-01 |
| C-L02 | S-02-I | Important tab | Authenticated; apply predicate | AC-08.1–4, BR-09.1, D-01 |
| C-L03 | S-02 | Issue row / details link | Authenticated | AC-02.3 |
| C-L04 | S-02 | Create Issue | Authenticated | BR-02, D-01 |
| C-C01 | M-01 | Title input | Authenticated; nonempty | AC-01.1/2 |
| C-C02 | M-01 | Description input | Authenticated; nonempty | AC-01.1/3 |
| C-C03 | M-01 | Create | Validate required fields then submit | AC-01.2–5 |
| C-C04 | M-01 | Cancel | No creation | D-01 |
| C-D01 | S-03 | Back | Authenticated | D-07 |
| C-D02 | S-03 | Assignee selection | Team Lead edits; one team member | US-03 AC bullets 1–3 |
| C-D03 | S-03 | Commit assignee | Team Lead; method TBD | US-03, D-06 |
| C-D04 | S-03 | Priority selection | Team Lead edits; four values | BR-05/06, AC-04.1/2 |
| C-D05 | S-03 | Commit priority | Team Lead; method TBD | BR-06, D-06 |
| C-D06 | S-03 | Status selection | Current assignee; BR-08.1 edges only | BR-07/08.1, AC-07.4/5 |
| C-D07 | S-03 | Commit status | Current assignee; method TBD | BR-08.1, D-06 |
| C-D08 | S-03 | Comment text | Authenticated; nonempty | AC-06.1 |
| C-D09 | S-03 | Add Comment | Validate; success / failed-save branches | AC-06.1–5 |
| C-D10 | S-03 | Comment list | Saved text, author and time visible | AC-06.2–4 |
| A-L01 | S-02/S-03 | Read-only issue metadata | Visible; not an editable Create input | AC-01.4/5, AC-02.2/4, AC-05.1–3 |
| A-L02 | SUP | Role, filter and transition reference | Reviewer annotation only | BR-06/08.1/09.1, AC-07.4 |

## 5. Source-derived permission matrix

| Action | Team Member non-assignee | Team Member assignee | Team Lead non-assignee | Team Lead assignee |
|---|---|---|---|---|
| View list / details | ALLOW | ALLOW | ALLOW | ALLOW |
| Create issue | ALLOW | ALLOW | ALLOW | ALLOW |
| Comment | ALLOW | ALLOW | ALLOW | ALLOW |
| Assign one assignee | DENY | DENY | ALLOW | ALLOW |
| Set/change priority | DENY | DENY | ALLOW | ALLOW |
| Change status | DENY | ALLOW **only** BR-08.1 | DENY | ALLOW **only** BR-08.1 |

**Source:** §3 `BR-01/02/06/08/08.1`, §5 `US-03`, `AC-04.2`, `AC-07.4`. Assignee is an **issue-specific relationship**, not a third global role. When no assignee exists, nobody is eligible to change status. A disabled/hide choice is D-05 and never proves server authorization.

## 6. Complete BR-08.1 status transition matrix

| Current → Target | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| Open | CURRENT, no transition | **ALLOW** | DENY | DENY |
| In Progress | DENY | CURRENT, no transition | **ALLOW** | DENY |
| Resolved | DENY | **ALLOW** | CURRENT, no transition | **ALLOW** |
| Closed | DENY | DENY | DENY | CURRENT, no transition |

The four ALLOW edges apply **only** when `current user == current assignee`; no actor may set undefined values or skip transitions. A Closed status is terminal for **status transitions only**.

## 7. Navigation / action transitions (local TR IDs)

| TR-ID | From → To | Trigger / precondition | Observable contract | Source / decision |
|---|---|---|---|---|
| TR-01 | S-01 → S-02 | C-A01 demo shortcut | List; not a real login | D-02 |
| TR-02 | S-02-I → S-02 | C-L01 All | Complete fixture list | US-02, D-01 |
| TR-03 | S-02 → S-02-I | C-L02 Important | Correct subset of **same issues** | AC-08.1–4 |
| TR-04 | S-02/S-02-I → S-03 | C-L03 selected row | Matching ID and issue details | AC-02.3/4 |
| TR-05 | S-02/S-02-I → M-01 | C-L04 Create | Required-field form | US-01, D-01 |
| TR-06 | M-01 → prior list | C-C04 Cancel | No issue created | D-01 |
| TR-07 | S-03 → list | C-D01 Back | Previous tab only if D-07 approved | D-07 |
| TR-08 | S-02 → S-02-E | Zero-issue example fixture | Empty state | AC-02.5 |
| TR-09 | S-02-E → M-01 | C-L04 Create | Open modal from empty state, if designed | D-01 |
| TR-10 | M-01-F → S-03-N | C-C03 with valid fields | New issue metadata with Open and unset priority | AC-01.1–5, D-01 |
| TR-11 | M-01 → M-01-V | C-C03 with missing required field | Error, no created issue | AC-01.2/3 |
| TR-12 | S-03 → updated S-03 | Lead selects team assignee and commits | One current assignee displayed | US-03, D-06 |
| TR-13 | S-03 → updated S-03 | Lead selects allowed priority and commits | Updated priority shown | AC-04.1/2, D-06 |
| TR-14 | S-03-CF → S-03-C | C-D09 with nonempty text, simulated success | Saved-entry display with author/time | AC-06.2–4 |
| TR-15 | S-03 empty text → validation | C-D09 | Error, no new comment | AC-06.1 |
| TR-16 | S-03-CF → S-03-CE | Simulated failed save | Error, no new comment | AC-06.5 |
| TR-17 | S-03 → updated S-03 | Assignee commits an allowed edge | Changed status displayed | BR-08.1, AC-07.3 |
| TR-18 | S-03 → unchanged S-03 | Non-assignee / forbidden edge / Closed | Action blocked, no status change | AC-07.4/5, BR-08.1 |

Transitions describe **planned** UX, not independently executed Figma tests. In particular, TR-18 is a denied action and must not be represented as a successful navigation.

## 8. AC-level Traceability Matrix — complete 33 / 33

**Column meanings.** `Requirement ID` is the **original** §5 AC code or `US-03, AC, пункт N`; `Source` cites the canonical specification and supporting BR/SR if relevant; `Screen/State` is the intended UI location; `UI Control` is the local registry ID; `Test Case` is an executable plan in §9; `Expected Result` states the observable outcome (and, where needed, a backend condition); `Evidence` gives a candidate artifact and `EV-PENDING`, **not** a verified claim. All `Verification Status` are **NOT VERIFIED** pending actual tests and, where necessary, implementation tests. `V/P/I` appear in evidence as applicable verification levels.

| Requirement ID | Source | Screen / State | UI Control | Test Case | Expected Result | Evidence (candidate; not verified) | Verification Status |
|---|---|---|---|---|---|---|---|
| AC-01.1 | `SD_Spec(1).docx` §5 US-01 | M-01 | C-C01, C-C02 | PT-01 | Title and Description can both be entered. | `EV-PENDING`; create_default.png; V/P | **NOT VERIFIED** |
| AC-01.2 | `SD_Spec(1).docx` §5 US-01; BDD Title error | M-01-V | C-C01, C-C03 | PT-02 | Empty Title blocks creation; message `Title is required` in source BDD example. | `EV-PENDING`; create_validation.png; V/P; I validation | **NOT VERIFIED** |
| AC-01.3 | `SD_Spec(1).docx` §5 US-01 | M-01-V | C-C02, C-C03 | PT-03 | Empty Description blocks creation and shows required-field feedback. | `EV-PENDING`; create_validation.png; V/P; I validation | **NOT VERIFIED** |
| AC-01.4 | `SD_Spec(1).docx` §5 US-01; §3 BR-03 | M-01-F → S-03-N | C-C03, A-L01 | PT-04 | Created issue has ID, status Open, created_at and author; unique/persisted values require I. | `EV-PENDING`; planned S-03-N; V/P; I creation | **NOT VERIFIED** |
| AC-01.5 | `SD_Spec(1).docx` §5 US-01; §3 BR-04/05 | S-03-N | A-L01, C-D04 | PT-04 | New issue priority is unset (display proposed Not Set), not chosen automatically. | `EV-PENDING`; planned S-03-N; V/P; I default | **NOT VERIFIED** |
| AC-02.1 | `SD_Spec(1).docx` §5 US-02; §3 BR-01 | S-02 | C-L01 | PT-05 | Authenticated team user can view registered issues list. | `EV-PENDING`; all_issues.png; V/P; I access | **NOT VERIFIED** |
| AC-02.2 | `SD_Spec(1).docx` §5 US-02 | S-02, S-02-I | A-L01 | PT-05 | Each row shows ID, Title, Status, Priority, and Assignee if assigned. | `EV-PENDING`; all_issues.png; V; I live data | **NOT VERIFIED** |
| AC-02.3 | `SD_Spec(1).docx` §5 US-02 | S-02 → S-03 | C-L03 | PT-06 | Selecting a row opens that same issue’s details. | `EV-PENDING`; all_issues.png + issue_details.png; P | **NOT VERIFIED** |
| AC-02.4 | `SD_Spec(1).docx` §5 US-02 | S-03 | A-L01 | PT-06 | Details show ID, Title, Description, Status, Priority, Assignee if assigned, Author and Created at. | `EV-PENDING`; issue_details.png; V; I data | **NOT VERIFIED** |
| AC-02.5 | `SD_Spec(1).docx` §5 US-02 | S-02-E | A-L01 (empty annotation) | PT-07 | When no issues exist, empty list or no-issues message appears. | `EV-PENDING`; empty_state.png; V/P | **NOT VERIFIED** |
| US-03, AC, пункт 1 | `SD_Spec(1).docx` §5 US-03, unnumbered bullet 1; §1 A-04 | S-03, SUP-A | C-D02 | PT-10 | Exactly one assignee can be chosen for an issue, never multiple. | `EV-PENDING`; planned SUP-A; V/P; I cardinality | **NOT VERIFIED** |
| US-03, AC, пункт 2 | `SD_Spec(1).docx` §5 US-03, unnumbered bullet 2; §3 BR-01 | S-03, SUP-A | C-D02 | PT-10 | Available assignee belongs to team; reject outsiders in implementation. | `EV-PENDING`; planned SUP-A; V; I membership | **NOT VERIFIED** |
| US-03, AC, пункт 3 | `SD_Spec(1).docx` §5 US-03, unnumbered bullet 3; §1 Open Questions | S-03, SUP | C-D02, C-D03, A-L02 | PT-11 | Only Team Lead can assign; Members cannot make assignment changes. | `EV-PENDING`; role_lifecycle.png; V/P; I authz | **NOT VERIFIED** |
| US-03, AC, пункт 4 | `SD_Spec(1).docx` §5 US-03, unnumbered bullet 4 | S-03 | A-L01, C-D02 | PT-10 | Current assignee is visible on issue details after assignment. | `EV-PENDING`; issue_details.png; V; I persisted value | **NOT VERIFIED** |
| AC-04.1 | `SD_Spec(1).docx` §5 US-04; §3 BR-05 | S-03, SUP-A | C-D04 | PT-12 | Only Low, Normal, High, Critical are settable priority values. | `EV-PENDING`; planned SUP-A; V/P; I enum | **NOT VERIFIED** |
| AC-04.2 | `SD_Spec(1).docx` §5 US-04; §3 BR-06 | S-03, SUP | C-D04, C-D05, A-L02 | PT-13 | Team Lead can set/change priority; Team Member cannot. | `EV-PENDING`; role_lifecycle.png; V/P; I authz | **NOT VERIFIED** |
| AC-05.1 | `SD_Spec(1).docx` §5 US-05; §3 BR-07 | S-02, S-03 | A-L01 | PT-05, PT-06 | Current status shown for every issue. | `EV-PENDING`; all_issues.png + issue_details.png; V | **NOT VERIFIED** |
| AC-05.2 | `SD_Spec(1).docx` §5 US-05 | S-03 | A-L01 | PT-06 | Current status visible on issue details. | `EV-PENDING`; issue_details.png; V | **NOT VERIFIED** |
| AC-05.3 | `SD_Spec(1).docx` §5 US-05 | S-02, S-02-I | A-L01 | PT-05 | Current status visible in issues list. | `EV-PENDING`; all_issues.png; V | **NOT VERIFIED** |
| AC-06.1 | `SD_Spec(1).docx` §5 US-06 | S-03, validation | C-D08, C-D09 | PT-08 | Empty comment is rejected; no comment entry is added. | `EV-PENDING`; comment_errors.png; V/P; I validation | **NOT VERIFIED** |
| AC-06.2 | `SD_Spec(1).docx` §5 US-06 | S-03-CF → S-03-C | C-D09, C-D10 | PT-09 | Nonempty comment is saved and shown under the correct issue; real save requires I. | `EV-PENDING`; comment_added.png + planned S-03-CF; V/P; I save | **NOT VERIFIED** |
| AC-06.3 | `SD_Spec(1).docx` §5 US-06 | S-03-C | C-D10 | PT-09 | Saved comment author is displayed and stored. | `EV-PENDING`; comment_added.png; V; I author storage | **NOT VERIFIED** |
| AC-06.4 | `SD_Spec(1).docx` §5 US-06 | S-03-C | C-D10 | PT-09 | Saved comment creation date/time is displayed and stored. | `EV-PENDING`; comment_added.png; V; I datetime | **NOT VERIFIED** |
| AC-06.5 | `SD_Spec(1).docx` §5 US-06 | S-03-CF → S-03-CE | C-D09, C-D10 | PT-18 | Failed save displays error and does not create any new comment. | `EV-PENDING`; comment_errors.png + planned S-03-CE; V/P; I failed save | **NOT VERIFIED** |
| AC-07.1 | `SD_Spec(1).docx` §5 US-07; §3 BR-03 | S-03-N | A-L01 | PT-04 | Newly created issue has status Open. | `EV-PENDING`; planned S-03-N; V/P; I default | **NOT VERIFIED** |
| AC-07.2 | `SD_Spec(1).docx` §5 US-07; §3 BR-07 | S-03, SUP-S | C-D06 | PT-14 | Only Open, In Progress, Resolved, Closed exist as statuses. | `EV-PENDING`; planned SUP-S; V; I domain | **NOT VERIFIED** |
| AC-07.3 | `SD_Spec(1).docx` §5 US-07; §3 BR-08.1 | S-03, SUP-S | C-D06, C-D07 | PT-15 | Allowed update is saved and shown on next viewing; persistence needs I. | `EV-PENDING`; planned SUP-S; P; I reload | **NOT VERIFIED** |
| AC-07.4 | `SD_Spec(1).docx` §5 US-07; §3 BR-08 | S-03, SUP | C-D06, C-D07, A-L02 | PT-16 | Non-assignee (even Team Lead) cannot change status. | `EV-PENDING`; role_lifecycle.png; V/P; I authz | **NOT VERIFIED** |
| AC-07.5 | `SD_Spec(1).docx` §5 US-07; §3 BR-07/08.1 | S-03, SUP-S | C-D06 | PT-17 | Undefined status cannot be set; server rejects invalid submitted values. | `EV-PENDING`; planned SUP-S; V/P; I rejection | **NOT VERIFIED** |
| AC-08.1 | `SD_Spec(1).docx` §5 US-08; §3 BR-09/09.1 | S-02-I | C-L02, A-L02 | PT-19 | High and status != Closed appears, including High+Resolved. | `EV-PENDING`; important_issues.png; V/P; I filter | **NOT VERIFIED** |
| AC-08.2 | `SD_Spec(1).docx` §5 US-08; §3 BR-09/09.1 | S-02-I | C-L02, A-L02 | PT-19 | Critical and status != Closed appears, including Critical+Resolved. | `EV-PENDING`; important_issues.png; V/P; I filter | **NOT VERIFIED** |
| AC-08.3 | `SD_Spec(1).docx` §5 US-08; §3 BR-09 | S-02-I | C-L02, A-L02 | PT-19 | Low/Normal issues absent from Important. | `EV-PENDING`; important_issues.png; V/P; I filter | **NOT VERIFIED** |
| AC-08.4 | `SD_Spec(1).docx` §5 US-08; §3 BR-09.1 | S-02-I | C-L02, A-L02 | PT-19 | All Closed issues absent from Important regardless of priority. | `EV-PENDING`; important_issues.png; V/P; I filter | **NOT VERIFIED** |

### 8.1 Explicit coverage checks

| Story | Source AC range / bullet positions | Matrix rows | Count |
|---|---|---|---:|
| US-01 | AC-01.1–AC-01.5 | rows 1–5 | 5 |
| US-02 | AC-02.1–AC-02.5 | rows 6–10 | 5 |
| US-03 | Four unnumbered §5 bullets, cited in source order | rows 11–14 | 4 |
| US-04 | AC-04.1–AC-04.2 | rows 15–16 | 2 |
| US-05 | AC-05.1–AC-05.3 | rows 17–19 | 3 |
| US-06 | AC-06.1–AC-06.5 | rows 20–24 | 5 |
| US-07 | AC-07.1–AC-07.5 | rows 25–29 | 5 |
| US-08 | AC-08.1–AC-08.4 | rows 30–33 | 4 |
| **TOTAL** | **Release MVP: US-01–US-08** | **33 distinct source criteria** | **33** |

**Not a 34th AC:** `priority = Not Set` is excluded from Important because it satisfies neither High nor Critical (DERIVED from `BR-04/05/09`, `AC-08.1–4`). US-01 BDD examples are illustrative, not additional AC. `Resolved` with High/Critical stays Important (`BR-09.1`).

## 9. Test cases — repeatable Figma checks (and their limits)

**Execution instructions:** record `PT-ID`, chosen Figma page/frame/node link + version, test actor, initial fixture, actual clicks, expected vs observed behavior, tester, date, screenshot/video link and verdict in `07_Prototype_Test_Record.md`. Do **not** infer PASS merely from existing screenshot filenames. For any absent frame record `BLOCKED — FRAME MISSING`; for any unexecuted path use `NOT TESTED`. This revision has **no executed test record**, so all matrix rows remain `NOT VERIFIED`.

| Test Case | Actor / precondition | Steps | Expected result | Not proven by Figma |
|---|---|---|---|---|
| PT-01 | Authenticated team user; M-01 open | Inspect and fill both fields | Title and Description editable; Create action available | Saving to DB |
| PT-02 | User; blank Title, valid Description | Click Create | `Title is required`; no success state/new issue | Server-side rejection |
| PT-03 | User; valid Title, blank Description | Click Create | Description required feedback, no success state/new issue | Server-side rejection |
| PT-04 | User; both required fields populated in M-01-F | Create → inspect **new** S-03-N, not existing issue | Title/Description plus ID, Open, created_at, author; priority absent | Actual unique ID, timestamp provenance, persistence |
| PT-05 | Authenticated user; list fixture | Open All and inspect every row | List visible with ID, Title, Status, Priority, Assignee where assigned | Auth/session and live records |
| PT-06 | User; selected row known | Click row → S-03; match ID | Correct selected issue; all detail fields including Author/Created at | Real database consistency |
| PT-07 | User; zero-issues fixture | Open S-02-E | Empty message/list; no fake issue row | Actual count in database |
| PT-08 | Authenticated user; comment field empty | Add Comment | Validation; comment list/count unchanged | Server validation |
| PT-09 | User; S-03-CF **nonempty** comment | Add Comment → S-03-C | One new visible comment with correct text, author, timestamp | Real storage, generated audit fields |
| PT-10 | Team Lead; issue, valid team choices | Open assignee choices, select exactly one, commit via approved D-06 | One current assignee shown, all options team members | Real membership validation/persistence |
| PT-11 | Member non-assignee; Member assignee; Lead contexts | Attempt assignment in each | Members denied, Leads allowed; no unauthorized state mutation | Server-side authorization |
| PT-12 | Team Lead; issue unset or already prioritized | Inspect choices and select priority | Four valid settable values; Not Set is display of absence, not fifth choice | Backend enum and persistence |
| PT-13 | Team Lead and Member fixtures | Attempt change priority | Lead permitted; Member prevented | Backend authorization |
| PT-14 | Assignee; Open, In Progress, Resolved, Closed fixtures | Inspect available outgoing transitions in each | Exactly four allowed BR-08.1 edges overall, no Closed outgoing | Backend transition rules |
| PT-15 | Assignee; issue with allowed edge | Commit edge; navigate away and reopen | Updated current status visually consistent | Actual saved value after refresh/new session |
| PT-16 | Non-assignee Member, non-assignee Lead, unassigned issue | Attempt status update | Denied/blocked; unchanged state | Server-side authorization |
| PT-17 | Assignee; Closed / invalid status case | Attempt illegal edge or unknown value | No change, invalid values not selectable | API injection rejection |
| PT-18 | Authenticated user; nonempty comment; simulated failure | Attempt save that enters failure fixture | Error shown, **no new comment**, same count | Real API error handling/transaction |
| PT-19 | User; fixtures across priorities and statuses | Switch All ↔ Important, compare cases | Include High/Critical non-Closed incl. Resolved; exclude Closed, Low, Normal, Not Set | Dynamic filtering on real data |
| PT-20 | Authenticated user; create modal open | Cancel | Back to list; no simulated new issue | DB absence |
| PT-21 | User; opened an Important row | Details → Back | Return to Important **only if D-07 approved** | Routing in actual application |

### 9.1 Implementation-only checks (needed for full AC verification)

| IT-ID | Source | Execute in real application (not Figma) |
|---|---|---|
| IT-01 | BR-01, NFR-02 | Unauthenticated access denied; exactly preconfigured team user/roles exercised; auth method to be decided |
| IT-02 | AC-01.2–5, AC-07.1 | Reject missing required values; actual unique ID, Open, author, created_at, unset priority; reload and compare |
| IT-03 | US-03 bullets 1–4, AC-04.1/2, AC-07.4 | Validate team membership and single assignee; block non-Leads assigning/changing priority; block non-assignee status writes even if Lead |
| IT-04 | BR-07/08.1, AC-07.2/3/5 | Validate all transition edges + disallowed edges + malformed status; verify saved state after reload |
| IT-05 | AC-06.1–5 | Persist comments with author/date/time; force failed save and prove no comment created |
| IT-06 | AC-08.1–4, BR-09.1 | Query persisted records to check exact Important predicate including Resolved and Closed cases |
| IT-07 | §8 NFR-01/03/04 | Define load/measurement environment then measure response < 1 s; verify HTTPS-only and backup of all data |

## 10. Evidence register (candidate sources, no re-validation)

The following filenames are noted in the previously published `03` document as existing/referenced repository screenshot evidence. **Their bytes and correspondence to latest Figma nodes have not been independently audited for this revision**. `Candidate` means *where to look*, not proven correctness.

| EV-ID | Candidate repository file | Useful for planned test(s) | Limitation / action |
|---|---|---|---|
| EV-01 | `evidence/all_issues.png` | PT-05/06 | Reinspect columns and navigation separately |
| EV-02 | `evidence/important_issues.png` | PT-19 | Static fixture alone cannot prove predicate dynamically |
| EV-03 | `evidence/empty_state.png` | PT-07 | Verify no-issue fixture; not real DB empty |
| EV-04 | `evidence/create_default.png` | PT-01 | Does not prove creation |
| EV-05 | `evidence/create_validation.png` | PT-02/03 | Verify both validation scenarios separately |
| EV-06 | `evidence/issue_details.png` | PT-06 | Existing issue details **not** new-issue success proof |
| EV-07 | `evidence/comment_added.png` | PT-09 | Requires preceding nonempty input and observed click |
| EV-08 | `evidence/role_lifecycle.png` | PT-11/14/16 | Reference annotation cannot prove enforcement |
| EV-09 | `evidence/comment_errors.png` | PT-08/18 | Distinguish empty validation from failed save |
| EV-10 | `evidence/reusable_components.png` | Visual components | Does not prove Figma-native component structure |
| EV-11 | **Missing / to create** `M-01-F`, `S-03-N` | PT-04 | New issue populated form + result, unique ID/Open/Not Set/author/time |
| EV-12 | **Missing / to create** `S-03-CF`, `S-03-CE` | PT-08/09/18 | Proper prefilled success path and failed save without addition |
| EV-13 | **Missing / to create** `SUP-A`, `SUP-S` | PT-10–17 | Explicit choices, outcomes, denied roles, complete transitions |
| EV-14 | **Missing / to capture** Present recording with node/version | PT-02/03/04/06/09/10–19 | Actual interactions and tester/date required |

**Verification status values for future use:** `NOT VERIFIED` (not tested or unconfirmed), `BLOCKED` (prerequisite/frame/decision absent), `PASS — V`, `PASS — P` (only when recorded), `FAIL — V/P`, and `PASS — I` (implementation-only proof). For full-source compliance, pass visual/prototype aspects **and** applicable `I` checks. Never use `PASS` for a merely proposed flow or an inherited screenshot reference.

## 11. Known unverified Figma coverage / required remediation

1. **All 33 criteria currently lack new independently documented test confirmation** in this revision: `NOT VERIFIED` is a statement of **evidence status**, not a claim that all 33 features are defective or absent.
2. **Requires new/prepared states or flows:** Create success and generated metadata (`AC-01.4/5`, `AC-07.1`; PT-04), complete assignee/priority choices and permission examples (US-03 bullets 1–4; `AC-04.1/2`; PT-10–13), full status choices and permitted/forbidden transitions (`AC-07.2–5`; PT-14–17), comment text-before-success + save failure without new entry (`AC-06.1–5`; PT-08/09/18).
3. **Existing screen candidates still require re-test:** fields and navigation (`AC-01.1–3`, `AC-02.1–5`, `AC-05.1–3`), Important selection/filter examples (`AC-08.1–4`). An image of the result is not evidence that clicking reached it, or that filtering is implemented.
4. **Never fully provable in Figma alone:** generated/persisted ID, author/time and absence of initial priority; server validation, assignee/team membership and permissions; priority mutation rights; saved comments and failed persistence; durable status changes/reload and rejection of fabricated status; dynamically computed Important predicate; authentication/NFR. Track their `IT-*` tests separately.
5. **Decisions before prototype sign-off:** approve D-01–D-08 or explicitly decline/replace each, particularly **D-06 commit behavior**, D-04 reassignment/initial assignee, and D-05 forbidden-control presentation. Log owner, date, decision and affected frames. Do not silently promote proposed UX behavior into source requirements.

## 12. Source-consistency review checklist / release gate

- [x] Source specification supplied and read, with §8 final Release MVP selected.
- [x] 8 included US and exactly **33** distinct AC items represented in matrix; four US-03 bullets cited by position.
- [x] AC test targets, UI controls, expected outcomes, candidate evidence and NOT VERIFIED verdicts provided.
- [x] BR-08.1 four-edge matrix, assignee-only change, priority-only Team Lead, BR-09.1 Resolved/Important and Not Set interpretation preserved.
- [x] No US-09 / SR-10 / SR-11 promoted to MVP; US-01 BDD not double counted.
- [ ] Human approvals for D-IDs recorded, including blocking D-06.
- [ ] Evidence artifact existence / exact Figma frame/version independently inspected.
- [ ] PT-01–PT-21 executed and results entered into `07_Prototype_Test_Record.md`.
- [ ] Applicable IT-01–IT-07 executed in a real implementation (outside Figma practical's proof scope).
- [ ] Independent reviewer signs `03` version/date and gives approval.

**Document acceptance decision:** **SOURCE TRACEABILITY COMPLETE (33/33); FIGMA VERIFICATION INCOMPLETE; DOCUMENT NOT APPROVED.**

**Human approval record (fill only after real review):** Reviewer: _pending_ · Date: _pending_ · Approved D-IDs: _none recorded_ · Open blockers: D-04, D-06 and remaining unsigned D-IDs.
