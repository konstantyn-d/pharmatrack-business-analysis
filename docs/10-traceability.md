# 10 · Requirements Traceability Matrix

> **Document purpose:** prove that every business objective is covered by requirements, every requirement by a user story, and every story by something delivered and tested. Read it left to right: *why → what → for whom → where → proven by*.

---

## 1. Coverage summary

| | Total | ✅ Delivered | 🟡 Partial | 🔵 Planned |
|---|:---:|:---:|:---:|:---:|
| Functional requirements | 30 | 29 | 1 | – |
| Non-functional requirements | 10 | 7 | 2 | 1 |
| User stories | 21 | 20 | 1 | – |

## 2. Forward traceability (objective → delivery)

| BO | BR | FR | User story | Delivered in | Status | Verified by |
|---|---|---|---|---|:---:|---|
| BO-1 | BR-01 | FR-01 | US-01 | Lane wizard | ✅ | AC US-01, audit `LANE_CREATED` |
| BO-1 | BR-01 | FR-02 | US-02 | Lane builder canvas | ✅ | AC US-02, audit `NODE_ADDED` |
| BO-1 | BR-01 | FR-03 | US-03 | Company selector in builder | ✅ | AC US-03 |
| BO-1 | BR-01 | FR-04 | US-04 | Dashboard world map | ✅ | Demo step 1 |
| BO-2 | BR-02 | FR-05 | US-02 | Route rules | ✅ | AC US-02 (`ROUTE_BROKEN`) |
| BO-4 | BR-04 | FR-06 | – | Archive action on lane | ✅ | Lane status `archived` |
| BO-2 | BR-02 | FR-07 | US-03 | Compliance › Companies | ✅ | Demo data, 24 companies |
| BO-1 | BR-01 | FR-08 | – | Shipments page | ✅ | Demo step 5 |
| BO-1 | BR-01 | FR-09 | – | Filters & search on lanes, shipments | ✅ | Manual test |
| BO-2 | BR-02 | FR-10 | US-05 | Compliance › Certifications | ✅ | AC US-05 |
| BO-2 | BR-02 | FR-11 | US-05 | Certificate status model | ✅ | AC US-05 |
| BO-2 | BR-02 | FR-12 | US-06 | Expiry calculation (60-day window) | ✅ | AC US-06 |
| BO-2 | BR-02, BR-04 | FR-13 | US-07 | Compliance › Validators | ✅ | AC US-07, audit `CERTIFICATE_REJECTED` |
| BO-2 | BR-02 | FR-14 | US-09 | Risk engine, 8 categories | ✅ | AC US-09 |
| BO-2 | BR-02 | FR-15 | US-10 | Finding cards with recommended action | ✅ | Risk report |
| BO-2 | BR-02 | FR-16 | US-09 | Scoring policy | ✅ | AC US-09 (score = 100 − Σ) |
| BO-2 | BR-02 | FR-17 | US-09 | Risk level badges | ✅ | Lane list |
| BO-2 | BR-02 | FR-18 | US-11 | Live assessment in builder | ✅ | Audit `RISK_RECALCULATED` |
| BO-3 | BR-03 | FR-19 | US-12 | Temperature readings API | ✅ | `POST /api/lanes/:id/temperature` |
| BO-3 | BR-03 | FR-20 | US-12 | Deviation detection | ✅ | Demo scenario *Critical* |
| BO-3 | BR-03 | FR-21 | US-13 | Alert severity rule (> 2 °C) | ✅ | AC US-13 |
| BO-3 | BR-03, BR-04 | FR-22 | US-14 | Alert dialog: assign, resolve with note | ✅ | AC US-14 |
| BO-3 | BR-03 | FR-23 | US-15 | Settings › Notifications | 🟡 | Preferences UI delivered; e-mail/SMS sending in phase 2 |
| BO-4 | BR-04 | FR-24 | US-16 | Audit service | ✅ | Audit log page |
| BO-4 | BR-04 | FR-25 | US-16 | Append-only DB policy | ✅ | AC US-16 |
| BO-4 | BR-04 | FR-26 | US-08, US-17 | CSV export endpoints | ✅ | `GET /api/audit/export`, `/api/compliance/export` |
| BO-2 | BR-02 | FR-27 | US-18 | Lane risk report + export | ✅ | Risk report page |
| BO-1 | BR-01 | FR-28 | US-19 | Dashboard with editable layout | ✅ | Demo step 1 |
| BO-5 | BR-05 | FR-29 | US-20 | Token check on API | ✅ | Every endpoint except `/health` |
| BO-5 | BR-05 | FR-30 | US-21 | Permission matrix in UI | ✅ | AC US-21 |

## 3. Non-functional requirements

| NFR | Status | Evidence |
|---|:---:|---|
| NFR-01 Immutable audit | ✅ | No UPDATE / DELETE policy on `audit_logs` |
| NFR-02 Security | 🟡 | RLS on all 14 tables, role binding at DB level planned |
| NFR-03 Explainability | ✅ | Every deduction linked to a finding |
| NFR-04 Consistency | ✅ | Lane score derived from the same capped figures as the category cards |
| NFR-05 Validation | ✅ | Zod schemas on every API input |
| NFR-06 Usability | 🟡 | Validated informally in the stakeholder demo, no formal usability test |
| NFR-07 Performance | 🔵 | Not load-tested beyond the 22-lane demo portfolio |
| NFR-08 Availability | ✅ | Deployed web application |
| NFR-09 Maintainability | ✅ | One policy file for all points and thresholds |
| NFR-10 Traceability of readings | ✅ | `source` and `recorded_at` on every reading |

## 4. Pain point → solution

| AS-IS pain point | Requirement(s) | Result |
|---|---|---|
| P1 · Evidence chased by e-mail | FR-01 – FR-03, FR-10 | One register, visible gaps per node |
| P2 · Manual certificate checks | FR-12, FR-13 | Expiry and verification checked automatically |
| P3 · Spreadsheet risk scoring | FR-14 – FR-18 | Consistent, explainable score |
| P4 · Excursions found after delivery | FR-19 – FR-22 | Alerts during transit |
| P5 · Decisions in inboxes | FR-24 – FR-26 | Append-only, exportable audit trail |

---

⬅️ Previous: [09 · KPIs](09-kpis.md) · ➡️ Next: [11 · Retrospective](11-retrospective.md)
