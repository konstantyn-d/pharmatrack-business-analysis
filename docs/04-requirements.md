# 04 · Business Requirements Document (BRD)

> **Document purpose:** a single, numbered list of what PharmaTrack must do (functional) and how well it must do it (non-functional), prioritised with MoSCoW and traceable to the business objectives in [01 · Business Case](01-business-case.md).
>
> **Status:** v1.0, baselined after stakeholder session #4 (acceptance).

---

## 1. Conventions

| Field | Meaning |
|---|---|
| **ID** | `BR-` business requirement · `FR-` functional · `NFR-` non-functional |
| **Priority** | **M**ust · **S**hould · **C**ould · **W**on't (this release), MoSCoW |
| **Source** | `CEO` stakeholder sessions · `GDP` EU GDP guidelines 2013/C 343/01 · `Team` derived by the analysis |
| **Objective** | Business objective it serves (BO-1 … BO-5) |

## 2. Business requirements

| ID | Business requirement | Objective |
|---|---|---|
| BR-01 | 4Viso shall manage every transport lane as a chain of actionable nodes and legs. | BO-1 |
| BR-02 | 4Viso shall know, before a lane is used, whether every participant is certified and capable. | BO-2 |
| BR-03 | 4Viso shall be warned during transit when a product leaves its temperature band. | BO-3 |
| BR-04 | 4Viso shall be able to prove afterwards who did what, when and why. | BO-4 |
| BR-05 | 4Viso shall restrict actions to the people responsible for them. | BO-5 |

## 3. Functional requirements

### 3.1 Lane management

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-01 | The system shall let a user create a lane with a code, cargo category, temperature band (preset or custom) and handling requirements. | M | CEO | BR-01 |
| FR-02 | The system shall let a user add, remove and reorder nodes (warehouse, airport, port, hub, customs, final delivery) in a visual lane builder. | M | CEO | BR-01 |
| FR-03 | The system shall let a user assign a responsible company to every node and a carrier and transport mode to every leg. | M | CEO | BR-01 |
| FR-04 | The system shall show a lane on a world map with the status of each leg. | S | CEO | BR-01 |
| FR-05 | The system shall flag a route that is incomplete, has a gap, or uses a transport mode that does not fit the location. | M | Team | BR-02 |
| FR-06 | The system shall archive (soft-delete) a lane instead of deleting it, so its history is kept. | M | GDP | BR-04 |

### 3.2 Company register & shipments

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-07 | The system shall store each company's type (carrier, warehouse, forwarder, airport handler, port operator, customs broker) and its capabilities: temperature ranges, security level, track & trace, real-time monitoring. | M | CEO | BR-02 |
| FR-08 | The system shall list shipments per lane with status (`loading`, `in transit`, `customs`, `delayed`, `arrived`, `delivered`), current node and progress. | M | CEO | BR-01 |
| FR-09 | The system shall let a user filter shipments and lanes by status, mode and risk level and search by code or carrier. | S | Team | BR-01 |

### 3.3 Certifications & validation

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-10 | The system shall keep a register of certificates per company (GDP, IATA CEIV Pharma, ISO 9001, ISO 13485, ISO 28000, GMP, TAPA) with issue date, expiry date and supporting document. | M | CEO, GDP | BR-02 |
| FR-11 | The system shall track each certificate through the statuses `claimed`, `pending review`, `valid`, `rejected`, `expired`. | M | CEO | BR-02 |
| FR-12 | The system shall automatically mark a certificate as *expired* after its expiry date and as *expiring soon* within 60 days of it. | M | GDP | BR-02 |
| FR-13 | The system shall let an independent validator verify or reject a certificate or a claimed capability, recording who decided and when. | M | CEO | BR-02, BR-04 |

### 3.4 Risk assessment

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-14 | The system shall assess every lane against rules in 8 categories: temperature, certifications, validation, handling, security, carriers & facilities, monitoring, route. | M | CEO | BR-02 |
| FR-15 | Each finding shall have a code, a severity, a plain-language explanation and a recommended action. | M | CEO (session #3) | BR-02 |
| FR-16 | The system shall compute a lane score of 0–100 (higher is safer) and a score per category. See [08 · Risk Rules](08-risk-rules.md). | M | Team | BR-02 |
| FR-17 | The system shall map the score to a level: excellent, low, medium, high, critical. | M | Team | BR-02 |
| FR-18 | The system shall recalculate the assessment whenever a node, leg, company or certificate on the lane changes. | M | CEO | BR-02 |

### 3.5 Monitoring & alerts

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-19 | The system shall record temperature readings per shipment with value, time, node and source (sensor, manual, carrier API). | M | GDP | BR-03 |
| FR-20 | The system shall flag a reading outside the lane's temperature band as a deviation. | M | GDP | BR-03 |
| FR-21 | The system shall raise a **critical** alert when a deviation exceeds the band by more than 2 °C and a **warning** otherwise. | M | CEO | BR-03 |
| FR-22 | Alerts shall follow the lifecycle `open → assigned → resolved` or `dismissed`, with an owner and a resolution comment. | M | CEO | BR-03, BR-04 |
| FR-23 | Users shall choose which notifications they receive (temperature, compliance, arrivals, weekly digest) and through which channel (e-mail, SMS, push). | C | CEO | BR-03 |

### 3.6 Audit, reporting & dashboard

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-24 | Every state-changing action shall be written to an audit log with actor, action, entity and timestamp. | M | GDP | BR-04 |
| FR-25 | The audit log shall be append-only: no user, including an admin, may edit or delete an entry. | M | GDP | BR-04 |
| FR-26 | Users shall filter and search the audit log and export it, and the compliance overview, as CSV. | M | CEO | BR-04 |
| FR-27 | The system shall produce a printable risk report per lane listing every finding and recommended action. | S | CEO | BR-02 |
| FR-28 | The dashboard shall show portfolio KPIs (see [09 · KPIs](09-kpis.md)) and let a user rearrange its widgets. | S | CEO | BR-01 |

### 3.7 Access control

| ID | Requirement | Priority | Source | BR |
|---|---|:---:|---|---|
| FR-29 | Every user shall sign in; every API call except the health check requires a valid token. | M | Team | BR-05 |
| FR-30 | The system shall enforce five roles (admin, operations manager, compliance officer, validator, viewer) as defined in [06 · Roles & Permissions](06-roles-and-permissions.md). | M | CEO | BR-05 |

### 3.8 Won't have (this release)

| ID | Requirement | Reason |
|---|---|---|
| FR-W1 | Live integration with carrier telematics / IoT sensor platforms | Requires partner API contracts; demo readings used instead |
| FR-W2 | Automatic customs declarations | Outside 4Viso's role |
| FR-W3 | Customer self-service portal | Planned for a later phase |

## 4. Non-functional requirements

| ID | Category | Requirement | Priority | Source |
|---|---|---|:---:|---|
| NFR-01 | Data integrity | Audit records are immutable, enforced at database level (row-level security), not only in the UI. | M | GDP |
| NFR-02 | Security | Row-level security is enabled on every table and service keys are never exposed to the browser. Role permissions are enforced in the UI in the MVP and bound to the user's role in the database in phase 2. | M | Team |
| NFR-03 | Explainability | Every point removed from a risk score can be traced to a named finding. | M | CEO |
| NFR-04 | Consistency | The overall score always equals 100 minus the sum of the category deductions shown in the report. | M | Team |
| NFR-05 | Validation | All input is validated against a schema before it reaches business logic; invalid input returns a clear error. | M | Team |
| NFR-06 | Usability | A new user can build a four-node lane without training in under 5 minutes. | S | CEO |
| NFR-07 | Performance | Dashboard and lane pages load in under 2 seconds for a portfolio of 100 lanes. | S | Team |
| NFR-08 | Availability | Deployed as a web application reachable from any modern browser; no installation. | M | CEO |
| NFR-09 | Maintainability | Risk points and thresholds are defined in one place, so 4Viso can tune the policy without touching rules. | S | Team |
| NFR-10 | Traceability | Every temperature reading keeps its source and timestamp for record keeping. | M | GDP |

---

⬅️ Previous: [03 · Process Models](03-process-models.md) · ➡️ Next: [05 · User Stories](05-user-stories.md)
