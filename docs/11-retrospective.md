# 11 · Retrospective & Lessons Learned

> **Document purpose:** an honest look back at how the analysis was done, what worked, what I would change, and what 4Viso should do next.

---

## 1. Outcome

| | |
|---|---|
| **Delivered** | Deployed web platform, accepted by 4Viso's CEO in the final session |
| **Academic result** | 17 / 20 |
| **Business impact** | 4Viso reused the team's code and concepts in its own product development |
| **Requirements coverage** | 29 of 30 functional requirements delivered, 1 partially ([10 · Traceability](10-traceability.md)) |

## 2. What went well

| ✅ | Why it mattered |
|---|---|
| **Talking directly to the decision-maker.** Four sessions with the CEO, no intermediaries. | Scope decisions were made in the room, not over weeks of e-mail. |
| **Remodelling the lane as a graph** after session #1 ([07 · Data Model](07-data-model.md#3-why-a-graph-not-a-single-row-per-lane)). | Turned a tracking dashboard into a tool that pinpoints the failing link, which is what the CEO actually wanted. |
| **Explainable risk instead of a black-box number.** | The CEO's feedback in session #3 became the product's main differentiator: every point lost has a reason and an action. |
| **Three scripted demo scenarios** (ideal, disputed, critical). | The acceptance demo told a story from *healthy* to *on fire* and made the value obvious in five minutes. |
| **Clear "won't have" list.** | Live IoT integration was explicitly parked, which protected the timeline. |

## 3. What I would do differently

| ⚠️ What happened | 💡 What I do now |
|---|---|
| Requirements were agreed **verbally** and lived in the team's notes and code. | Send a one-page summary of decisions after every session and ask the stakeholder to confirm it. This repository is that documentation, written up after delivery. |
| The first technical brief modelled a lane as a single row; the graph model came later and caused rework. | Model the domain (entities and relationships) with the stakeholder **before** writing a technical brief. |
| The risk score had **two polarities** for a while: the first backend version treated *higher = riskier*, the risk engine *higher = safer*. | Write a **glossary and KPI definitions** in week 1 ([09 · KPIs](09-kpis.md)), so every team member computes the same number the same way. |
| Non-functional requirements (performance, usability) were never measured formally. | Define a measurable target for each NFR and test it before the final demo. |
| End users (operations, compliance) were represented only through the CEO. | Interview at least one real user per persona, even briefly. |

## 4. Recommendations for phase 2

| Priority | Recommendation | Requirement |
|:---:|---|---|
| 1 | Bind database write policies to the signed-in user's role | NFR-02 |
| 2 | Connect one carrier telematics or IoT sensor feed for live readings | FR-W1 |
| 3 | Send e-mail / SMS notifications for critical alerts | FR-23 |
| 4 | Start measuring excursion rate, MTTR and certificate coverage | [09 · KPIs §3](09-kpis.md#3-proposed-kpis-for-phase-2) |
| 5 | Run a usability test with an operations manager and a compliance officer | NFR-06 |

## 5. Skills this project demonstrates

`Requirements elicitation` · `Stakeholder management` · `Process modelling (AS-IS / TO-BE, BPMN)` · `User stories & acceptance criteria (Gherkin)` · `MoSCoW prioritisation` · `Data modelling (ERD)` · `Business rules & decision tables` · `KPI definition` · `Requirements traceability` · `Domain knowledge: pharma cold chain, EU GDP` · `SQL / PostgreSQL` · `Agile delivery`

---

⬅️ Previous: [10 · Traceability](10-traceability.md) · 🏠 [Back to README](../README.md)
