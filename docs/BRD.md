# Resident & Flat Management — Business Requirements Document (BRD)

**Product:** SMART GATE — Multi-Society Residential ERP Platform
**Module:** Resident & Flat Management
**Document ID:** RFM-BRD
**Version:** 1.0 (Draft)
**Date:** 11 November 2026
**Status:** For review
**Related documents:** [README.md](README.md) (start here) · [PRD.md](PRD.md)

> The BRD explains **why** this module exists and **what the business needs** from it. It is written for the client, management and anyone deciding scope. For how the product should behave, see PRD.md.

---

## Contents

- [1. Executive Summary](#1-executive-summary)
- [2. Business Background and Problem Statement](#2-business-background-and-problem-statement)
- [3. Business Objectives and Success Measures](#3-business-objectives-and-success-measures)
- [4. Stakeholders](#4-stakeholders)
- [5. Business Scope](#5-business-scope)
- [6. Business Requirements](#6-business-requirements)
- [7. Business Rules](#7-business-rules)
- [8. Assumptions, Constraints and Dependencies](#8-assumptions-constraints-and-dependencies)
- [9. Business Risks](#9-business-risks)
- [10. Approval](#10-approval)
- [Glossary](#glossary)

---

## 1. Executive Summary

Residential societies keep their flat and resident records in registers, spreadsheets and messaging groups. These records are often incomplete, out of date and not shared between the office, the security gate and the accounts team.

The Resident & Flat Management module gives each society one verified, always-current register of its **blocks, floors, flats, owners, tenants and family members**. It is the foundation of the SMART GATE platform: visitor approval, maintenance billing, complaints, amenity booking, parking and communication all depend on knowing who lives in which flat and in what capacity.

## 2. Business Background and Problem Statement

### Current situation

| Area | How it works today | Business impact |
| --- | --- | --- |
| Flat records | Paper register or Excel kept by the society office | No single source of truth; errors in billing |
| Resident details | Collected on paper forms at move-in | Phone numbers go stale; family members unknown |
| Tenants | Often not reported by owners | Security risk; tenants miss notices and bills |
| Gate security | Guards call the flat from an intercom list | Slow; wrong numbers; no record of who approved |
| Move-in / move-out | Informal; register rarely updated | Former residents keep receiving bills and access |
| Multiple societies | Each managed separately | No platform-level view for the operator |

### Problem statement

Society management committees cannot reliably answer *"who lives in flat A-302 right now, and who may approve visitors or receive the bill?"* This causes security gaps at the gate, billing disputes, missed communication and time spent reconciling records by hand.

## 3. Business Objectives and Success Measures

| # | Objective | Success measure | Target (to confirm) |
| --- | --- | --- | --- |
| BO-1 | Create one digital register per society | Flats in the system vs actual flats | 100% within 2 weeks of onboarding |
| BO-2 | Cut onboarding effort for a new society | Time to load an existing society's data | Under 1 working day via bulk import |
| BO-3 | Keep resident data current | Active residents with a verified mobile number | 95% or more |
| BO-4 | Bring tenants on record | Rented flats with an active tenant record | 90% or more |
| BO-5 | Speed up resident approvals | Median time from sign-up to decision | Under 24 hours |
| BO-6 | Protect resident data | Cross-society data access incidents | Zero |
| BO-7 | Drive app adoption | Flats with at least one resident logged into the app | 70% within 3 months |

## 4. Stakeholders

| Stakeholder | Role / interest |
| --- | --- |
| Platform owner (SMART GATE operator) | Onboards societies; needs a scalable, secure multi-society product |
| Society Management Committee | Accountable for accurate records and resident safety |
| Society Admin / Office staff | Day-to-day users who set up flats and approve residents |
| Accountant | Needs the correct billing party for each flat |
| Security Supervisor and Guards | Need to know who lives where and who can approve visitors |
| Flat Owners | Want control over their flat, family and tenants |
| Tenants | Want quick access to gate approvals, notices and payments |
| Family members | Want app access for their household |
| Product, engineering and QA team | Build, test and run the module |

## 5. Business Scope

### In scope

1. Society structure: blocks (towers/wings), floors and flats
2. Resident records: owners, tenants and family members
3. Linking residents to one or more flats with a role in each
4. Excel/CSV bulk import of flats and residents
5. Resident self sign-up, admin approval and onboarding
6. Household management by residents (family members and tenants)
7. Move-out and ownership transfer, keeping history
8. Resident directory search, filters and export
9. Audit trail of all changes
10. Access through the admin web portal and the resident mobile app (Android and iOS)

### Out of scope

1. Visitor approval, billing, complaints, bookings, parking and notices (separate modules that *consume* this module's data)
2. Hardware such as RFID, boom barriers, biometric devices
3. Police verification service integration
4. Rental agreement drafting or e-stamping
5. Property sale or registry workflows beyond recording the change of owner

## 6. Business Requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| BR-01 | The society must be able to record its full physical structure: blocks, floors and flats. | Must |
| BR-02 | Every flat must show its current occupancy: vacant, owner-occupied, rented or locked. | Must |
| BR-03 | The society must be able to record owners, tenants and family members for each flat. | Must |
| BR-04 | One person must be linkable to more than one flat (e.g. an owner of two flats). | Must |
| BR-05 | Each flat must have one primary contact for approvals and communication. | Must |
| BR-06 | The society must be able to load existing records in bulk from Excel/CSV. | Must |
| BR-07 | Residents must be able to request access themselves using their mobile number. | Must |
| BR-08 | No self-registered resident may gain access without approval by the society. | Must |
| BR-09 | Owners must be able to add family members and tenants for their flat. | Must |
| BR-10 | Tenants must be able to add their own family members. | Should |
| BR-11 | The society must be able to record move-outs and ownership changes without losing history. | Must |
| BR-12 | One society's data must never be visible to another society. | Must |
| BR-13 | Access to resident data must depend on the user's role. | Must |
| BR-14 | Every change to flat or resident records must be traceable to a user and time. | Must |
| BR-15 | The society must be able to search and export its resident list. | Should |
| BR-16 | The flat record must state who pays maintenance (owner or tenant). | Should |
| BR-17 | Residents must be reminded before a tenant's lease end date. | Could |

## 7. Business Rules

| ID | Rule |
| --- | --- |
| RULE-01 | A flat number is unique within its block; a block name is unique within its society. |
| RULE-02 | A mobile number identifies one person within a society. |
| RULE-03 | A flat has exactly one primary contact while it is occupied. |
| RULE-04 | A flat may have joint owners, but only one active tenant household at a time. |
| RULE-05 | Only the Society Admin (or Super Admin) approves new self-registered residents and tenants. |
| RULE-06 | A tenant record requires a move-in date. |
| RULE-07 | Records with history (residents, billing, gate logs) are never deleted; they are deactivated or marked moved out. |
| RULE-08 | A moved-out or inactive resident loses app access for that flat immediately. |
| RULE-09 | Guards see only name, flat and photo; mobile numbers are masked for guard roles. |
| RULE-10 | Records created by the admin or by bulk import are active at once; the admin vouches for them. |

## 8. Assumptions, Constraints and Dependencies

### Assumptions

1. Each resident has a personal mobile number that can receive SMS OTP.
2. The society provides an initial list of flats and residents, or enters them in the portal.
3. The Society Admin reviews pending requests at least once a working day.
4. Indian mobile number format (10 digits) applies for the first release.

### Constraints

1. SMS must be sent through a DLT-registered sender ID and templates (India).
2. Personal data must be handled in line with the Digital Personal Data Protection Act, 2023: collected for a stated purpose, accessible only to those who need it, and removable on valid request.
3. The mobile app must work on Android and iOS from a single codebase.

### Dependencies

| Dependency | Needed for |
| --- | --- |
| Authentication service (OTP, JWT, roles) | Login and permission checks |
| Society onboarding by Super Admin | A society must exist before its flats are created |
| SMS gateway | OTP and decision notifications |
| Push notification service (FCM) | In-app notifications |
| File storage | Photos, ID proofs and import error reports |

## 9. Business Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Society's existing data is poor quality | Slow onboarding, wrong records | Validation preview, error report, re-upload |
| Owners do not report tenants | Gate and billing gaps | Tenant self sign-up; occupancy reports for the admin |
| Admin does not act on approvals | Residents cannot use the app | Pending-request reminders; dashboard count |
| Misuse of resident personal data | Legal and reputational damage | Role-based access, masking, audit logs |
| Low app adoption | Benefits not realised | SMS invitation after import; simple OTP login |

## 10. Approval

| Name | Role | Decision | Date |
| --- | --- | --- | --- |
| | Society / Client representative | | |
| | Product Owner | | |
| | Technical Lead | | |

## Glossary

| Term | Meaning |
| --- | --- |
| Society | A residential complex managed as one unit on the platform |
| Block | A tower, wing or building within a society |
| Flat | A residential or commercial unit within a block |
| Owner | Person who owns a flat |
| Tenant | Person renting a flat for a period |
| Family member | Person living with an owner or tenant household |
| Primary contact | The resident who receives approvals and communication for a flat first |
| Billing party | Owner or tenant who receives the maintenance bill |
| Occupancy status | Vacant, Owner-occupied, Rented or Locked |
| OTP | One-time password sent by SMS for login |
| DLT | Distributed Ledger Technology registration required for commercial SMS in India |
| DPDP Act | Digital Personal Data Protection Act, 2023 (India) |
| Society isolation | Guarantee that one society's data is never accessible to another |


---

## Document History

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| 1.0 | 11-11-2026 | Product team | First draft |
