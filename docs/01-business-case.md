# 01 · Business Case & Scope

> **Document purpose:** explain *why* PharmaTrack was built, what it must achieve and where its boundaries are.
> **Sources:** four requirements sessions with the CEO of 4Viso (May–Aug 2026), the delivered system, EU GDP guidelines.

---

## 1. Client context

**4Viso** is a Belgian compliance and risk-assessment company working with the pharmaceutical supply chain. Its customers ship temperature-sensitive medicines (vaccines, biologics, APIs) across multi-party international routes: a manufacturer's warehouse, a road carrier, an airport handler, an airline, a customs broker, a destination distributor.

Every party in that chain must:

- hold **valid certifications** (EU GDP, IATA CEIV Pharma, ISO 9001 / 28000, TAPA …),
- be **able to keep the product in its temperature band** (typically 2–8 °C),
- leave an **auditable trail** that a regulator or a Qualified Person can inspect afterwards.

## 2. Problem statement

| | |
|---|---|
| **The problem of** | assessing and controlling the risk of a pharmaceutical transport lane that crosses many companies, countries and transport modes |
| **affects** | 4Viso's operations and compliance teams, their pharma customers and, ultimately, patients |
| **the impact of which is** | slow manual assessments, certificates that expire unnoticed, temperature excursions discovered too late and an audit trail spread over e-mails, PDFs and spreadsheets |
| **a successful solution would** | model every lane as a chain of nodes and legs, check each link automatically against the lane's requirements, raise alerts when something breaks and record every action in an immutable audit log |

## 3. What the CEO asked for

The requirements were agreed verbally during four sessions. Condensed into one sentence:

> *"I want to see the whole supply chain as a chain of blocks, and I want to be able to interact with every block: assign tasks, re-route, add or withdraw certificates and permissions, give instructions, and control temperature, transport, people and borders."*

This was translated into five **business objectives**:

| ID | Business objective | How success is measured |
|---|---|---|
| **BO-1** | Give 4Viso a single, visual model of every transport lane | 100 % of lanes represented as a node/leg graph in one tool |
| **BO-2** | Detect compliance gaps before goods move | Every lane receives an explainable risk score on creation and on every change |
| **BO-3** | Detect temperature excursions in transit | Excursions surface as alerts with a recommended action, not in a post-delivery report |
| **BO-4** | Make every decision auditable | Every state-changing action is written to an append-only audit log, exportable as CSV |
| **BO-5** | Control who can do what | Role-based access for 5 roles with a documented permission matrix |

## 4. Scope

### In scope (MVP, delivered)

- Lane builder: create a lane as an ordered chain of **nodes** (warehouse, airport, port, hub, customs, final delivery) connected by **legs** (air, sea, road)
- Assignment of a responsible **company** to every node and leg
- **Certification** register per company with validity window and verification status
- Independent **validator** workflow (verify / reject a certificate or capability)
- Rule-based **risk engine** over 8 categories with explainable findings and recommended actions
- **Temperature monitoring** per shipment with deviation detection
- **Alerts** with lifecycle `open → assigned → resolved / dismissed`
- **Dashboard** with portfolio KPIs and a world map of active lanes
- Append-only **audit log** with filters and CSV export
- **Role-based access control** for 5 roles

### Out of scope (agreed with the stakeholder)

- Live integration with carrier telematics and IoT sensor APIs (demo data only)
- Automatic customs filing
- Billing, invoicing and customer self-service portal
- Native mobile application

## 5. Constraints & assumptions

| Type | Statement |
|---|---|
| Regulatory | The solution must support the principles of the **EU Guidelines on Good Distribution Practice of medicinal products for human use (2013/C 343/01)**: temperature control, qualified suppliers, traceability and record keeping. |
| Time | One university semester (May–Aug 2026), four-person team. |
| Data | Real 4Viso reference data was combined with seeded demo data (22 lanes, 3 scripted demo scenarios). |
| Technology | Web application. Next.js frontend, Node.js / Express API, Supabase (PostgreSQL, Auth, Row-Level Security). |
| Assumption | Certificate validity can be judged from issue and expiry dates plus an independent validator's decision. |

## 6. Expected benefits

- **Faster assessments:** a lane's risk is calculated in seconds instead of being compiled by hand.
- **Fewer surprises:** certificates that are missing, expired or expiring are flagged before the lane is used.
- **Audit readiness:** one exportable trail instead of an inbox search.
- **Transparency for the customer:** every risk finding comes with a plain-language explanation and a recommended action.

---

➡️ Next: [02 · Stakeholder Analysis](02-stakeholders.md)
