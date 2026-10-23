# 05 — Figma Brief v1.0 (English)

## Objective
Create an editable grayscale low-fidelity desktop prototype for **Mini Issue Tracker**. This is a UI/UX learning artifact, not a functional backend.

## Canvas and visual system
Desktop frames 1440×900. Use Auto Layout, reusable local components, clear text hierarchy, neutral grayscale, accessible contrast and consistent spacing. Avoid high-fidelity branding.

## Roles
Two Team Members and one Team Lead. Authenticated members can create/view/comment. Only Team Lead can assign an issue and set priority. Only the **current assignee** can change status, even if the Lead is not the assignee.

## Screens
S-01 auth boundary placeholder; S-02 All Issues (8 sample issues); S-02 Important Issues (4); empty list; M-01 Create default and validation; S-03 Issue Details ISS-003; supplementary permissions/status and comment error states. Include a static Comment Added result frame.

## Required issue fields
List: ID, Title, Status, Priority, Assignee. Details: add Description, Author, Created at, Comments. Create form asks only Title and Description; both required. Created issue starts Open, priority Not Set.

## Rules
Priorities: Low, Normal, High, Critical; Not Set is absence, not a fifth level. Statuses: Open, In Progress, Resolved, Closed. Allowed: Open→In Progress; In Progress→Resolved; Resolved→In Progress; Resolved→Closed. No outgoing from Closed. Important = (High or Critical) and not Closed, including Resolved.

## Fixture data
ISS-001 Open Critical Member A; ISS-002 In Progress High Member B; ISS-003 Resolved High Member A; ISS-004 Closed Critical Member B; ISS-005 Open Normal Unassigned; ISS-006 Open Not Set Unassigned; ISS-007 Resolved Critical Lead; ISS-008 In Progress Low Member A. Important must show exactly 001,002,003,007.

## Prototype interactions
All↔Important, list item→details, Create→modal, validation, Cancel→list, comment→static success. Include error state for failed comment save. Explicitly label any simulated result. Do not imply real typing, persistence, authentication, permissions enforcement, HTTPS, backup or performance testing.

## Out of scope
Attachments US-09, AI recommendations SR-10/11, delete, history, integrations.

## Acceptance
Editable frames and components, consistent names, visible required content, meaningful clickable paths, no accidental hover/drag links, honest test record. **This brief reconstructs the project requirements; it is not claimed to be the verbatim historical Figma Agent prompt.**
