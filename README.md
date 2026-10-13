# PL-300 Power BI: AI CapEx, Tech Restructuring & Labor Dynamics

This repository serves as a study environment and portfolio project for the **Microsoft Power BI Data Analyst (PL-300)** certification. It models the relationship between global Big Tech capital expenditures (CapEx) in AI infrastructure and macroeconomic shifts in regional software engineering hubs (focusing on Silicon Savannah, Nairobi).

---

## 📂 Repository Architecture

- `datasets/`
  - `ai_market_data.json`: Nested JSON tracking quarterly CapEx, corporate revenues, net income, and regional labor impacts.
- `notes/`
  - `1-prepare-data.md`: Power Query ingestion pipelines, M code, and JSON parsing.
  - `2-model-data.md`: Star schema setup, DAX measures, and time intelligence formulas.
  - `3-ai-labor-impact.md`: Macroeconomic correlation between AI automation spend and regional labor reallocation.
- `dax-scripts/`: Reusable DAX measures for financial efficiency ratios.

---

## 📊 Project Overview: AI Infrastructure vs. Global Tech Labor

The dataset contrasts two market phenomena:
1. **The Infrastructure Buildout:** Hundreds of billions invested in computing clusters, GPU hardware, and data centers globally.
2. **The Regional Workforce Impact:** Corporate restructurings and automation shifts in regional hubs, including:
   - **Microsoft ADC Nairobi:** Engineering department restructuring under global operational reviews.
   - **Sama / Meta Data Annotation:** Redundancies following automated internal AI moderation transitions.

---

## 🚀 Quick Start: Data Ingestion in Power BI

To ingest the JSON dataset directly into Power BI Desktop or Service:

1. Click on `datasets/ai_market_data.json` in this repository.
2. Click **Raw** to get the direct URL link.
3. In Power BI: **Get Data > Web**, paste the Raw URL, and apply the M Code transformation script in `notes/1-prepare-data.md`.
