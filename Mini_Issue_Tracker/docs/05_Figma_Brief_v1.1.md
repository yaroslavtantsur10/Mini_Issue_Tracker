# 05 — Mini Issue Tracker: Figma Design Implementation Brief (Revision v1.1)

**Artifact type:** revised / reconstructed design handoff, **not** a verbatim historical Figma Agent prompt.  
**Prepared:** 2026-11-11  
**Status:** **DRAFT — CONTROL C BLOCKED pending approval of D-01–D-08**, in particular D-04, D-05, D-06 and D-07.  
**Basis:** SD_Spec §3 Business Rules, §5 US/AC, §8 final Release Scope; `02_Screen_Map_Decision_Log.md` revised v1.1; `03_Screen_Contracts_Traceability.md` revised draft; `04_Plan_Review.md` revised v1.1.  
**Usage:** use as a checklist for manual Figma fixes **now**. Do not submit to Figma Agent as an *approved* contract, and do not mark Control C PASSED, until the decision log documents the actual human decisions and this brief matches them. Update the status when resolved. Historic generation evidence must be preserved separately.

## 1. Purpose and release scope [SOURCE §8, US-01–US-08]

Create/edit grayscale low-fidelity **desktop UX wireframes**, demonstrating a small team's internal issue tracker. Users can create and view issues, assign responsibility, set priority, inspect and change status, comment, and see important non-closed issues. The deliverable is an **editable design and annotated navigation intent**, not a running application.

Use fictional users **Member A**, **Member B**, and **Lead** (two Team Members and one Team Lead). **Current assignee** is an issue-specific relationship, not a new role. Release MVP covers US-01–US-08 and all 33 semantic acceptance criteria (US-03's four criteria are unnumbered source bullets).

## 2. Design constraints [PROPOSED D-01, D-02, D-08]

- Desktop frames approximately **1440 × 900**, one working Figma page, neutral grayscale and legible hierarchy; use editable Figma-native text, frames, controls and reusable local components, with Auto Layout wherever useful.
- Keep canonical product frames distinct from supporting examples. Notes and permission matrices are **outside product frames**, in the `SUP` / `REF-01` review area.
- Preserve existing IDs: `S-01`, `S-02` (All), `S-02-I` (Important), `S-02-E` (Empty), `M-01`, `M-01-V`, `S-03`, `S-03-C`, `SUP`. The method's names `S-02-A/B/C` correspond to `S-02/S-02-I/S-02-E`; do not rename existing frames needlessly.
- Use compact supplementary states rather than a complete detail page for every role × status combination. Avoid decorative page icons, unexplained squares, row-selection checkboxes and bulk controls.
- Show role-based restrictions through a documented presentation choice (**D-05 must be decided**). A disabled control and a hidden control are alternative UX representations; neither changes permissions.
- `S-01` is an **authentication boundary** with “Authentication entry — mechanism TBD”; no invented login fields. Demonstration may start at `S-02` in an already-authenticated context. Never depict this as genuine login verification.

## 3. S-02 — Issues List [US-02, US-05, US-08; BR-09/09.1; PROPOSED D-01]

The same product screen has three example states:

| Figma ID | State | Must be shown |
|---|---|---|
| `S-02` | All Issues | Header, tabs `All Issues` / `Important Issues`, `Create Issue`; issue rows with **ID, Title, Status, Priority, Assignee** |
| `S-02-I` | Important Issues | Same columns, same underlying fixture IDs, predicate below |
| `S-02-E` | Empty list | Clear no-issues message and no fake issue row |

**Important predicate:** `(Priority == High OR Priority == Critical) AND Status != Closed`. `Resolved` is **not** `Closed`, so High/Critical + Resolved stays in Important. `Low`, `Normal`, `Not Set` and **all** Closed issues are excluded [AC-08.1–4, BR-09.1].

Canonical sample data (fictional):

| ID | Status | Priority | Assignee | Important? |
|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | Yes |
| ISS-002 | In Progress | High | Member B | Yes |
| ISS-003 | Resolved | High | Member A | Yes |
| ISS-004 | Closed | Critical | Member B | No |
| ISS-005 | Open | Normal | Unassigned | No |
| ISS-006 | Open | Not Set | Unassigned | No |
| ISS-007 | Resolved | Critical | Lead | Yes |
| ISS-008 | In Progress | Low | Member A | No |

**Important Issues must show exactly ISS-001, ISS-002, ISS-003 and ISS-007**, with consistent row data. Title/row takes the user to details of the **selected issue**, not always ISS-003. Tabs are views of one list, not two unrelated issue repositories.

## 4. M-01 — Create Issue overlay [US-01 AC-01.1–5; BR-02/03/04; PROPOSED D-01]

- **Only user-entered fields:** `Title` (required), `Description` (required, multiline). Buttons: `Create` and `Cancel`. Do not add editable fields for ID, author, date, status or priority.
- `M-01`: default blank form. `M-01-V`: invalid-form examples — blank Title → `Title is required` (source BDD wording), blank Description → a clear required-field message (proposed copy). **No issue is created** on either invalid submission.
- **Add `M-01-F` (NEW):** a prepared *filled* form, e.g. Title `Search results fail to load` and Description `An error appears after selecting the search filter.` This is demo data, not an extra product requirement.
- **Add `S-03-N` (NEW):** a resulting **new** issue after a valid `Create`, showing the *same* Title and Description, **new sample ID `ISS-009`**, **Status: Open**, **Priority: Not Set** (absence of value), **Author: Member A** (for the chosen demo persona), and a clearly labeled **sample creation timestamp**. New ID/time/author are prototype fixtures; **do not claim a real ID generator or data persistence**. Show `Assignee: Unassigned` **only if D-04 is human-decided**.
- `Cancel` closes the modal without a new issue. A valid Create navigates to prepared `S-03-N` **if that destination is accepted as the UX route**. This does not require conditional logic or a database.

## 5. S-03 — Issue Details [US-02–US-07]

One details screen contains **ID, Title, Description, Status, Priority, Assignee, Author, Created at**, and a comments section. The existing default example is **ISS-003 — Resolved / High / Member A**. A Team Lead viewing this issue is **not** the current assignee: Lead can change Assignee and Priority but **cannot change Status**. Do not assume that Team Lead overrides the assignee-only rule [BR-08; AC-07.4].

### Assignee [US-03 AC points 1–4]

Only **Team Lead** may choose **one** assignee from actual team members. The current assignee is visible on details. Add a compact `SUP-A` example of allowable assignee options and a before/after assignment or reassignment result. Whether a newly created issue starts `Unassigned` and whether reassignment is supported must be explicitly resolved as **D-04**; do not silently convert that proposal into a source requirement.

### Priority [BR-04–06; AC-04.1–2]

Only **Team Lead** may set or modify priority. Exactly four **selectable** values: `Low`, `Normal`, `High`, `Critical`. `Not Set` displays the absence of priority **before selection**; it is **not** a fifth selectable level and does not imply a reset operation. Add a `SUP-A` menu example with exactly these four choices and one visibly updated result. Membership in Important follows the same predicate when priority changes.

### Status [BR-08/08.1; AC-07.1–5]

Only the **current assignee** may update Status. Valid current-state → next-state options:

| Current status | Allowed next status(es) |
|---|---|
| Open | In Progress |
| In Progress | Resolved |
| Resolved | In Progress; Closed |
| Closed | **None** |

No other transitions. A Lead who is not current assignee **must not** change status; an unassigned issue has no assignee allowed to update it. Add `SUP-S` examples showing all four current statuses and relevant permitted options, especially **In Progress** and **Closed** missing in earlier evidence. Show a deny example for a non-assignee and an example of a valid status result/revisit as a **prepared prototype state only**. Do not imply real persistence.

### D-06 — interaction commit mechanism: BLOCKER

**Select + Apply** and **immediate commit on selection** are different designs. Existing documents leave this **unresolved**; do not invent a final answer inside the brief. Before changing interactive controls, record a human decision (`D-06`, decision, author, date, version), and use **one consistent mechanism** for Assignee, Priority and Status in `S-03`, docs 02/03/04, and prototype connections. If using Apply, show a local Apply control and an outcome; if using immediate commit, show the post-selection outcome and do not claim an Apply action. Absence of Apply **is not itself a defect**.

### Comments [AC-06.1–5]

- `S-03`: `New comment` input and `Add Comment` button; existing comments show **text, author and created date/time**.
- Blank input → validation message and **no new comment**.
- **Add `S-03-CF` (NEW):** non-empty prepared input (e.g. `I can reproduce this in the latest build.`) **before** triggering Add Comment.
- `S-03-C` Comment Added: same text visible as a new saved-looking entry, with demo author and sample timestamp; the `Comments (N)` count must match visible entries or be explicitly labeled as an excerpt. Keep entry typography and New comment field label consistent.
- **Add `S-03-CE` (NEW):** failed save message, **no newly added entry**, unchanged comment count; may be a compact supporting state, not a separate product page.
- Do **not** route a blank comment field directly to Comment Added. Do not claim real storage or error handling just because frames demonstrate outcomes.

## 6. Review notes (`SUP`, `SUP-S`, `SUP-A`) — not product UI

Represent all four role/assignee contexts compactly:

| Viewer context | Assign issue | Set priority | Change status |
|---|---|---|---|
| Member, not assignee | No | No | No |
| Member, current assignee | No | No | Yes, allowed transition only |
| Lead, not assignee | Yes | Yes | No |
| Lead, current assignee | Yes | Yes | Yes, allowed transition only |

Include the four-status transition matrix; compact permitted-menu examples; role-denied examples; comment validation/save-failure state; and a readable distinction between **SOURCE** requirements, **PROPOSED** decisions and demo-only sample data. Reviewer notes belong **outside** interactive frames, not as headings or labels inside the app.

## 7. Navigation intent — annotate before wiring [PROPOSED D-01/02/07/08]

- `S-02` All ↔ `S-02-I` Important.
- Row/title on list → `S-03` corresponding issue details.
- Create Issue → `M-01` default; Cancel → calling list, no issue created.
- Invalid Create → `M-01-V`, no issue; valid prefilled Create `M-01-F` → `S-03-N` prepared success (after route confirmation).
- Empty comment → validation; filled comment `S-03-CF` → `S-03-C`; failure branch → `S-03-CE` (simulate by separate prepared frames/links as appropriate).
- Back from details → list. Returning to the **previously selected All/Important tab** is **D-07 PROPOSED** until decided; don't claim it already works.
- Status/Priority/Assignee changes stay in details with visible before/after outcomes, using only the **approved D-06** commit model.

These are navigation annotations for later manual **Prototype** wiring. Do not request code, backend simulation or working conditional state from Figma Agent.

## 8. Explicit exclusions [SOURCE §8; BR-10/11; method scope]

No US-09 attachments, AI classification/recommendation (SR-10/11), deletion, user-visible change history, dashboards, analytics, integrations, search, sorting, pagination, bulk actions, multi-assignee, extra issue fields, extra status or priority levels, invented authentication method, real backend/API/security mechanisms, or extra product pages for assignment/priority/status/comments/Important. Do not add title/description editing after creation without source support.

## 9. Acceptance checklist / Control C (before Figma Agent invocation)

- [ ] D-01–D-08: necessary choices recorded with **actual human decision, name/role and date**; especially D-04, D-05, **D-06** and D-07. Not merely `USED IN MOCKUP`.
- [ ] All fixed SOURCE rules match SD_Spec; 33/33 AC have traceability in document 03. UI-proposed decisions are distinguished from source requirements.
- [ ] Names/IDs and fixture data match documents 02/03/04; Important contains exactly 001/002/003/007.
- [ ] Form has Title/Description only; successful create shows a **new** issue Open/Not Set with author/time, not existing Resolved ISS-003.
- [ ] Comment success begins with a **nonempty** text field; empty and failed-save examples create no entry.
- [ ] Status reference covers Open, In Progress, Resolved, Closed; no outgoing Closed transition; non-assignee denied.
- [ ] Priority selectable options are exactly Low, Normal, High and Critical. Assignee options show only team members, single-assignee result.
- [ ] Frames are editable; review notes are outside product frames; no decorative row checkboxes; present-mode clicks documented separately.
- [ ] Brief has been compared against accepted D-ID decisions; current `DRAFT / BLOCKED` label changed only if evidence of approval exists.

## 10. Evidence/reporting boundaries

For any Figma correction, log actual date, prompt or manual action, Figma frame, before/after image, and re-test. Later use `06_Generation_Correction_Report.md`, `07_Prototype_Test_Record.md`, `08_Final_Review_Defect_Change_Log.md`, and `09_AI_Interaction_Log.md` to reference evidence. Do not label planned frames `PASS`, claim the Agent created anything it did not create, or imply screenshots verify editable components, authentication, data persistence, authorization, security, or performance.

**Final status: BRIEF RECONSTRUCTED; CONTROL C NOT PASSED.** Resolve documented human UX decisions before treating this as an approved implementation handoff.
