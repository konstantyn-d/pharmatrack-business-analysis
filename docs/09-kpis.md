# 09 · KPI Definitions

> **Document purpose:** define every metric on the PharmaTrack dashboard precisely enough that two people calculating it get the same number, and propose the next KPIs for phase 2.

---

## 1. Dashboard KPIs (delivered)

| KPI | Question it answers | Formula | Shown as | Good direction |
|---|---|---|---|:---:|
| **Active lanes** | How much of the network is live? | `COUNT(lanes)` where status ∈ {active, in transit, customs, delayed} | Count, split *active / draft* | – |
| **Certification compliant** | Are partners certified where the lane requires it? | `lanes with every required certificate valid ÷ lanes that require certification × 100` | %, split *compliant / with gaps* | ⬆️ |
| **Temperature deviations** | Is the cold chain holding? | `COUNT(temperature readings outside the lane band)` in the last 24 h | Count, split *excursions / shipments in range* | ⬇️ |
| **High-risk lanes** | Where should we act first? | `COUNT(lanes)` with risk level ∈ {high, critical} | Count, split by level | ⬇️ |

**Design rule:** every KPI card reconciles to its own base. The two parts of each split add up to the total printed on the card, so the dashboard never contradicts itself.

## 2. Operational metrics per lane

| Metric | Formula | Used on |
|---|---|---|
| Risk score | `100 − Σ capped category deductions` (see [08](08-risk-rules.md)) | Lane list, lane detail |
| Compliance status | `compliant` / `warning` / `non-compliant` / `pending`, derived from certificate findings | Lane list, compliance page |
| Progress | `% of route completed` by the shipment's current node | Lane detail, shipments |
| Open alerts | `COUNT(alerts)` with status ∈ {open, assigned} | Lane detail, alert queue |

## 3. Proposed KPIs for phase 2

These came out of the retrospective with the stakeholder. They need data the MVP does not yet collect in production.

| KPI | Formula | Why it matters | Target (proposal) |
|---|---|---|---|
| **Excursion rate** | `shipments with ≥ 1 deviation ÷ shipments delivered` | The core quality metric of a cold chain | < 2 % |
| **Mean time to resolve (MTTR) critical alerts** | `AVG(resolved_at − created_at)` for critical alerts | Measures how fast the team reacts | < 4 h |
| **Certificate coverage** | `participants with all required certificates valid and verified ÷ all participants` | Leading indicator of compliance | > 95 % |
| **Expiring in 60 days** | `COUNT(certificates)` expiring within 60 days | Workload forecast for renewals | Trend down |
| **Validation backlog** | `COUNT(certificates in pending review)` and their average age | Bottleneck at validators | < 5 days old |
| **On-time delivery** | `shipments delivered ≤ ETA ÷ shipments delivered` | Customer service level | > 95 % |

## 4. Data quality checks behind the KPIs

| Check | Rule |
|---|---|
| Temperature band | `temp_min < temp_max` for every lane |
| Reading source | Every reading has a source and a timestamp |
| Certificate dates | `valid_from ≤ valid_until` |
| Route integrity | Every leg connects two existing nodes of the same lane |
| Score range | `0 ≤ risk_score ≤ 100` (database constraint) |

---

⬅️ Previous: [08 · Risk Rules](08-risk-rules.md) · ➡️ Next: [10 · Traceability Matrix](10-traceability.md)
