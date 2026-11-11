# Resident & Flat Management — Team Guide (Start Here)

**Product:** SMART GATE — Multi-Society Residential ERP Platform
**Module:** Resident & Flat Management
**Last updated:** 11 November 2026

This guide tells anyone joining the project **which document to read, where to find things, and the steps to follow** before building, testing or changing anything in this module. Read this page first.

---

## 1. What this module is

Resident & Flat Management is the society's master register of **blocks, floors, flats, owners, tenants and family members**. Every other SMART GATE module (Visitor & Gate, Billing, Helpdesk, Amenities, Parking, Communication, Reports) reads from it to know *who lives in which flat and in what role*.

If this module's data is wrong, the rest of the platform is wrong. Treat changes here with care.

---

## 2. The documents

| File | What it answers | Read it when you are… |
| --- | --- | --- |
| [README.md](README.md) | How to use the documents and how we work | New to the project, or unsure where to start |
| [BRD.md](BRD.md) | **Why** we build this and **what the business needs** | Discussing scope with the client, deciding priorities, writing proposals |
| [PRD.md](PRD.md) | **What** the product does and **how** it behaves | Designing, building, testing or reviewing a feature |

**Rule of thumb:** BRD = the "why" and "what", PRD = the "how". Every PRD requirement traces back to a BRD requirement (PRD section 17).

---

## 3. Where to find things

| I need… | Go to |
| --- | --- |
| The business problem and goals | BRD §2, §3 |
| What is in and out of scope | BRD §5 |
| Business requirements (BR-xx) | BRD §6 |
| Business rules (RULE-xx) | BRD §7 |
| Who the users are | PRD §3 Personas |
| User stories (US-xx) | PRD §4 |
| Functional requirements (FR-xx) and priority | PRD §5 |
| Step-by-step flows (onboarding, tenant, move-out, import) | PRD §6 |
| Database tables and fields | PRD §7 |
| Who can do what (permissions) | PRD §8 |
| Import file columns and validation | PRD §9 |
| API endpoints | PRD §10 |
| Performance, security, privacy targets | PRD §11 |
| Notifications to send | PRD §12 |
| Reports | PRD §13 |
| How a feature is accepted | PRD §14 |
| Release phases | PRD §15 |
| Unresolved decisions | PRD §16 |
| BR → FR mapping | PRD §17 |
| Terms (primary contact, billing party, etc.) | Glossary in either document |

---

## 4. ID conventions

Every requirement has a stable ID. **Use these IDs in tickets, branch names, commits, test cases and pull requests** so anyone can trace work back to the documents.

| Prefix | Meaning | Lives in |
| --- | --- | --- |
| `BO-xx` | Business objective | BRD §3 |
| `BR-xx` | Business requirement | BRD §6 |
| `RULE-xx` | Business rule | BRD §7 |
| `US-xx` | User story | PRD §4 |
| `FR-xx` | Functional requirement | PRD §5 |

**Priority** (PRD): `P0` must have for launch · `P1` should have · `P2` could have.
**Priority** (BRD): Must · Should · Could.

Never reuse or renumber an ID. If a requirement is dropped, mark it **(Removed)** and leave the ID in place.

---

## 5. How to pick up and build a feature

Follow these steps for every task:

1. **Find the requirement.** Locate the `FR-xx` in PRD §5. If your task has no FR, stop and raise it (see §7 below).
2. **Understand why.** Use PRD §17 to find the linked `BR-xx` in the BRD and read it.
3. **Check the rules.** Read BRD §7 Business Rules; your feature must not break any of them.
4. **Check permissions.** Confirm in PRD §8 which roles may perform the action. Enforce it **on the server**, not only in the UI.
5. **Check data and APIs.** Use the tables in PRD §7 and endpoints in PRD §10. If you need a new field or endpoint, update the PRD in the same pull request.
6. **Check the flow.** If the feature is part of a workflow in PRD §6, follow every step, including notifications in PRD §12.
7. **Check open questions.** If PRD §16 has an unanswered question that affects your work, ask before building on an assumption.
8. **Build and test against acceptance criteria** in PRD §14 and the non-functional targets in PRD §11.
9. **Reference IDs** in your ticket, branch, commits and PR (examples in §6).

### Non-negotiables for this module

- Every table carries `society_id`; every query is filtered by the logged-in user's society. **No exceptions.**
- Never hard-delete residents, flats or blocks with history. Deactivate or mark *Moved out*.
- Every create, update, approval, import and move-out writes to the audit log.
- Guard roles must never see full mobile numbers.
- Self-registered residents get no access until an admin approves.

---

## 6. Naming examples

| Item | Format | Example |
| --- | --- | --- |
| Ticket title | `[FR-xx] Short description` | `[FR-26] Import preview with row errors` |
| Branch | `feature/FR-xx-short-name` | `feature/FR-26-import-preview` |
| Commit | `FR-xx: what changed` | `FR-26: show error reasons per row` |
| Pull request | `[FR-xx] Title` + linked BR in description | `[FR-26] Import preview (BR-06)` |
| Test case | `TC-FR-xx-nn` | `TC-FR-26-03 duplicate mobile flagged` |
| Bug | `[BUG][FR-xx] Description` | `[BUG][FR-41] Primary contact not reassigned` |

---

## 7. How to change the documents

The documents are the single source of truth. If the code and the documents disagree, the documents win until they are updated.

| Type of change | Who approves | What to update |
| --- | --- | --- |
| Typo or wording fix | Any team member | The document only |
| New or changed FR, API, field or permission | Product Owner + Technical Lead | PRD (relevant section + §17 if needed) |
| New or changed business requirement, rule or scope | Client + Product Owner | BRD first, then PRD |
| Answer to an open question | Client | Move it out of PRD §16 into the right section |

**Steps**

1. Edit the `.md` file in a branch named `docs/<short-description>`.
2. Keep IDs stable; add new ones at the end of the sequence.
3. Add a row to the **Document History** table at the bottom of the changed file (version, date, author, change).
4. Bump the version: `1.0 → 1.1` for small changes, `1.x → 2.0` for scope changes.
5. Open a pull request and get the approval listed above.

---

## 8. Definition of Done (for any feature in this module)

- [ ] Linked `FR-xx` and `BR-xx` identified in the ticket
- [ ] Business rules (BRD §7) respected
- [ ] Permissions (PRD §8) enforced on the server and reflected in the UI
- [ ] Society isolation tested (a second society cannot see or change the data)
- [ ] Audit log entry written for every change
- [ ] Notifications sent as listed in PRD §12
- [ ] Acceptance criteria (PRD §14) pass; non-functional targets (PRD §11) met
- [ ] Works on web portal and, where relevant, Android and iOS apps
- [ ] API documented in Swagger/Postman
- [ ] PRD updated if behaviour, data or APIs changed

---

## 9. Technology at a glance

| Layer | Technology |
| --- | --- |
| Admin portal and website | React / Next.js |
| Mobile apps | React Native (Android and iOS) |
| Backend | Node.js REST APIs, versioned under `/api/v1` |
| Database | PostgreSQL |
| Auth and security | JWT, role-based access control, OTP via SMS, rate limiting, audit logs |
| Integrations | SMS gateway (DLT-registered), email, Firebase push notifications |

---

## 10. Contacts

Fill in names as the team is confirmed.

| Role | Name | Contact for |
| --- | --- | --- |
| Product Owner | | Scope, priorities, PRD changes |
| Technical Lead | | Architecture, data model, API changes |
| Client representative | | Business requirements, open questions, sign-off |
| QA Lead | | Test plans, acceptance |

---

## 11. Folder layout

```
docs/
├── README.md   ← this guide (start here)
├── BRD.md      ← business requirements
└── PRD.md      ← product requirements
```
