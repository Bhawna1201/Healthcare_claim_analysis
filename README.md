# Injectable Anesthesia Claims Analysis


---

## Project Overview

This project analyzes Medicare claims data (2016–2018) for the injectable anesthesia market across four competing products. Using HCPCS procedure codes, we track market share, HCP writer behavior, patient demographics, and territory-level competitive dynamics to diagnose why Product 2 (Midoride) is losing share and prescribe a data-driven recovery strategy.

**Market Basket:**

| Product | Brand | Generic Name | HCPCS Code | Role |
|---|---|---|---|---|
| P1 | Ketotrom | Ketorolac tromethamine | J1885 | Market Leader |
| P2 | Midoride | Midazolam hydrochloride | J2250 | Variant Brand (our product) |
| P3 | Fentirate | Fentanyl citrate | J3010 | Main Competitor |
| P4 | Profativ | Propofol | J2704 | Alternative Competitor |

---

## Repository Structure

```
healthcare-project/
│
├── notebooks/
│   ├── anesthesia_data_prep.ipynb       # Main analysis notebook (all 4 questions)
│   └── Anesthesia_final.ipynb           # Final consolidated notebook
│
├── outputs/
│   └── analysis_ready_claims_python.csv # Cleaned, merged, analysis-ready dataset
│
├── Medicare_Claims_data_part_1.csv      # Raw Medicare claims (part 1 of 5)
├── Medicare_Claims_data_part_2.csv      # Raw Medicare claims (part 2 of 5)
├── Medicare_Claims_data_part_3.csv      # Raw Medicare claims (part 3 of 5)
├── Medicare_Claims_data_part_4.csv      # Raw Medicare claims (part 4 of 5)
├── Medicare_Claims_data_part_5.csv      # Raw Medicare claims (part 5 of 5)
├── Diagnosis_Code_Mapping.csv           # Diagnosis code → specialty mapping
├── Procedure_Code_Mapping.csv           # Procedure code reference
├── Zip_to_Territory_Mapping.csv         # ZIP code → sales territory mapping
│
├── requirements.txt                     # Python dependencies
├── steps.txt                            # Data pipeline steps
└── README.md
```

---

## Setup & Installation

**1. Create virtual environment**
```bash
python3 -m venv --system-site-packages .venv
```

**2. Install dependencies**
```bash
.venv/bin/python -m pip install -r requirements.txt
```

**3. Open the notebook**
```bash
notebooks/anesthesia_data_prep.ipynb
```
When prompted for a kernel, select `.venv/bin/python`

---

## Data Pipeline

The notebook runs a 5-step data pipeline before analysis:

| Step | What it does |
|---|---|
| 1. Load & Merge Raw Claims | Combines all 5 Medicare CSV parts into one DataFrame |
| 2. Load Reference Data | Loads HCP demographics, patient demographics, ZIP-territory mapping, diagnosis codes |
| 3. Filter Market Claims | Identifies claims containing at least one market product code, keeps all lines from those claims |
| 4. Enrich Data | Merges HCP info, patient demographics, territory, diagnosis specialty, and age bands |
| 5. Save Output | Exports `outputs/analysis_ready_claims_python.csv` for analysis |

---

## Business Questions & Analysis

### Question 1 — Market Dynamics and Competitive Landscape (2016–2018)

#### Q1A. Product Market Share by Claims, Patients, and HCP Writers
- 100% stacked bar charts comparing P1–P4 share by year across three dimensions: unique claims, unique patients, unique HCP writers
- **Key Finding:** P1 lost 14.7 pp of claim share; P3 gained 14.4 pp — capturing exactly what P1 lost. P2 shrank from 10.1% to 5.4%, failing to absorb displaced demand.

#### Executive Scorecard
- KPI cards showing P1 and P2 erosion vs. P3 growth in claim share, patient share, and writer share from 2016 to 2018

#### Q1B. Claims per Writer and Patients per Writer
- Line charts showing HCP writer productivity (depth of use) per product per year
- **Key Finding:** P3's patients per writer rose 1.6 → 2.7 (habit forming). P2 remained flat at 1.1 → 1.3 (confidence gap). P1 stable at ~4.1 (loyal but not growing).

#### Competitive Productivity Snapshot
- Head-to-head P2 vs. P3 productivity comparison showing P3's widening depth advantage

#### Q1C. Top 5 Territories with Biggest Product 2 Claims Drop (2017→2018)
- Identified: **St. Louis, MO · Phoenix, AZ · LA-San Diego, CA · New York, NY · Minneapolis, MN**
- Clustered bar charts for P2 and P3 claims in those same 5 territories
- Diverging bar chart showing net P2 loss vs. P3 gain per territory
- **Key Finding:** P2 lost 76 total claims across 5 territories; P3 gained 121. Direct substitution — not market contraction. New York most critical: P2 −23, P3 +72.

#### Geographic Analysis
- USA state-level market map showing total market volume, P2 share, and P3 share by HCP state

---

### Question 2 — Key Market Drivers of the Injectable Anesthesia Market

#### Q2A. Diagnosis Specialty and HCP Specialty Mix
- Pie chart: top 5 diagnosis specialties — **Circulatory System drives 59.1%** of all market claims
- Horizontal bar chart: HCP writers by specialty — **Anesthesiology leads with 228 writers**, 2.6× the next group (Cardiology, 86)
- **Implication:** Focus P2 promotion on Anesthesiology + Cardiology writers treating circulatory cases

#### Q2B. Patient Age and Claim Distribution
- Age bands: 18–30, 31–40, 41–50, 51–60, 61–70, 71–80, 81+
- Bar charts for unique patients and claim share by age group
- 100% stacked bar: product mix within each age group
- **Key Finding:** Patients aged 61+ account for 54.3% of all claims. The 61–70 cohort is the single largest band (21.2%). P3 is winning share fastest in the senior segments.

#### Q2C. New and Continuing Writer Trends (2016–2018)
- Bar charts for new writers per product per year; line charts for continuing writers
- Writer retention visual showing % of each year's writers who are continuing vs. first-time
- **Key Finding:** P2 new writers collapsed from 111 → 34 (−69% YoY in 2018). P3 continuing writers grew 297 → 436 (+47%). P2 is losing on both fronts simultaneously.

---

### Question 3 — Strategies to Stop Market Share Erosion and Gain Traction for P2

A four-phase Recovery Playbook with measurable outcomes:

| Phase | Timeline | Action | Target Outcome |
|---|---|---|---|
| 1 | 0–60 days | **Stop the Competitive Leak** — declare 5 battleground territories, build HCP target lists, deploy competitive detailing | −2 to −4 pp on P3 share in battlegrounds within 90 days |
| 2 | 60–180 days | **Rebuild P2 as Default P1 Substitute** — target P1 and P3 writers, anchor on Anesthesiology (228 writers), build messaging for 61+ patients | P2 positioned as clinical successor, not parallel option |
| 3 | 90–180 days | **Win New Writers Before P3 Entrenches** — target 762 non-prescribing Anesthesiology HCPs, run tele-detailing → KOL webinar → 30-day follow-up sequence | Activate ~150 new writers (~20% conversion) in 6 months |
| 4 | Continuous | **Protect Depth Among Existing Writers** — 30-day second-Rx follow-up, quarterly refresh of switch-risk lists, move retention to primary KPI | +5–10% claims per HCP in P2 segments |

**KPI Targets:**
- Recover **3–5 share points** for P2 in 6–12 months
- Reduce P3 share by **2–4 pp** in top 5 territories
- Lift P2 new-writer acquisition by **+10–15% YoY**
- Improve P2 continuing-writer retention by **+5 pp**

---

### Question 4 — Data Exploration Opportunities and Data Concerns

#### 5 Critical Data Gaps
| Gap | Impact |
|---|---|
| No Sales / Promotion Data | Cannot measure rep call effectiveness or field coverage |
| No Patient Cost / Copay | Cannot assess cost-driven switching to P3 |
| No Procedure / Setting Data | Cannot explain P3 gains in specific clinical segments |
| Medicare-Only Dataset | Missing commercial / Medicaid / cash-pay (~70% of total market) |
| No Provider Affiliation | Cannot separate access-driven from preference-driven losses |

#### 6-Analysis Roadmap (4–16 weeks)
| Analysis | Timeline |
|---|---|
| ML HCP Segmentation — cluster by specialty, territory, demographics | 4–8 weeks |
| Product Cost Analysis — compare allowable charges; triggers patient assistance strategy if P2 priced higher | 4 weeks |
| NPP Channel Audit — identify which channels (email, webinar, ads) actually convert | 8–12 weeks |
| Untapped HCP Pipeline — 762 Anesthesiology HCPs not prescribing any brand | 4 weeks |
| DDD Supply Audit — rule out supply-side causes of P2 decline | 8–12 weeks |
| Formulary / Access Map — separate contracting from clinical preference losses | 8–12 weeks |

---

## Key Findings Summary

| Finding | Detail |
|---|---|
| Cannibalization failed | P3 (+14.4 pp) absorbed P1's decline; P2 (−4.7 pp) did not |
| HCP balance lost | By 2018 portfolio and competitors hold equal 50/50 HCP writer share |
| P3 building habit | Claims per writer: P3 rose 1.8 → 3.4; P2 flat at 1.5 → 1.3 |
| Geographic concentration | 5 territories account for disproportionate P2 loss with simultaneous P3 gain |
| Direct substitution | Total P2 loss 76 claims = P3 gain 121 claims — same writers, same patients |
| Senior patient market | 54.3% of all claims from patients aged 61+ |
| Writer acquisition collapse | P2 new writers fell 111 → 34 (−69%) while P3 continuing writers grew +47% |

---

## Technologies Used

- **Python 3** — pandas, matplotlib, seaborn, plotly
- **Jupyter Notebook** — interactive analysis and SVG visualizations
- **Medicare Claims Data** — HCPCS procedure codes, claim-level billing records
- **Custom SVG Charts** — stacked bar, line, clustered bar, diverging bar, pie, geographic map

---

