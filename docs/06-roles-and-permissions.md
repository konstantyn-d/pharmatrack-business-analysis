# 06 · Roles & Permissions

> **Document purpose:** define who may do what in PharmaTrack. This matrix was agreed with the stakeholder and is implemented one-to-one in the application's permission model.

---

## 1. Roles

| Role | Who | Responsibility in the process |
|---|---|---|
| **Admin** | 4Viso system owner | Full control, user management |
| **Operations Manager** | 4Viso operations team | Builds and maintains lanes, reacts to delays and excursions |
| **Compliance Officer** | 4Viso compliance team | Owns certificates, GDP status, alerts and audit evidence |
| **Validator** | Independent reviewer | Verifies or rejects certificates and claimed capabilities |
| **Viewer** | Customer, management, auditor | Read-only access to lanes, shipments and reports |

## 2. Permission matrix

| Permission | Admin | Operations Mgr | Compliance Officer | Validator | Viewer |
|---|:---:|:---:|:---:|:---:|:---:|
| View lanes, shipments, dashboard | ✅ | ✅ | ✅ | ✅ | ✅ |
| Create / edit lane (`edit_lane`) | ✅ | ✅ | – | – | – |
| Change route: nodes & legs (`edit_route`) | ✅ | ✅ | – | – | – |
| Update shipment status (`update_shipment`) | ✅ | ✅ | – | – | – |
| Resolve / dismiss alert (`resolve_alert`) | ✅ | ✅ | ✅ | – | – |
| Verify / reject certificate (`verify_cert`) | ✅ | – | ✅ | ✅ | – |
| Generate risk & compliance report (`generate_report`) | ✅ | ✅ | ✅ | – | – |
| View audit log (`view_audit`) | ✅ | – | ✅ | ✅ | – |
| Edit or delete an audit entry | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ |

> ⛔ Nobody, not even an admin, can change the audit log. This is enforced by the database (append-only policy), as required by EU GDP record-keeping principles.

## 3. Design decisions

| Decision | Rationale |
|---|---|
| **Segregation of duties:** operations builds lanes, compliance and validators judge evidence | The person who chooses a partner should not be the one who certifies that partner. |
| **Validators cannot edit lanes** | Keeps their verification independent of operational pressure. |
| **Operations cannot see the audit log** | The audit log is compliance evidence; operations sees its own actions in each lane's timeline instead. |
| **Viewer has no write permission at all** | Safe to share with customers and auditors. |
| **Least privilege by default** | A new user starts as *viewer* until an admin assigns a role. |

## 4. Implementation status

| Layer | MVP (delivered) | Phase 2 (recommended) |
|---|---|---|
| User interface | Every write action is hidden or disabled when the role lacks the permission | – |
| API | Token required on every endpoint except `/health` | Check the role on each write endpoint |
| Database | Row-level security on all 14 tables; audit log append-only | Bind write policies to the signed-in user's role |

---

⬅️ Previous: [05 · User Stories](05-user-stories.md) · ➡️ Next: [07 · Data Model](07-data-model.md)
