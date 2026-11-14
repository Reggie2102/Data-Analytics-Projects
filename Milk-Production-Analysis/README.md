# U.S. Milk Production Analysis (1998–2026)

An interactive 4-page Power BI report analyzing 28 years of USDA quarterly milk production data. This project explores long-term production trends, the drivers of industry growth (yield vs. herd size), and the impact of volatile feed and replacement cow costs.

*Built as a portfolio project to demonstrate data cleaning, star-schema modeling, DAX measure design, and dashboard storytelling.*

## Dashboard Preview

### 1. Overview
<img width="519" height="377" alt="Overview" src="https://github.com/user-attachments/assets/5dcfb8a0-6378-401c-9c8c-d9ea09f039ec" />


### 2. Growth & Efficiency
<img width="522" height="337" alt="Growth and Efficiency" src="https://github.com/user-attachments/assets/aeaa9f01-d96f-4d6e-b7b9-0f6a68d5d1b4" />


### 3. Cost Structure
<img width="526" height="292" alt="Cost Structure" src="https://github.com/user-attachments/assets/e3ba82f0-cc81-4347-87f4-50adc1f4ef74" />


### 4. Executive Summary & Data Notes
<img width="509" height="281" alt="Executive Summary and Data Notes" src="https://github.com/user-attachments/assets/35170f72-fe45-4ad1-b3d2-35bf1ac81347" />


##  Key Findings
*   **Production Growth:** U.S. milk production grew **47%** from 1998 to 2025 (157B to 232B lbs).
*   **The Yield Engine:** The national herd size has remained virtually flat (~9,200–9,500 head). The entire production gain was driven by a **42% increase in yield per cow** (17,185 to 24,390 lbs).
*   **Cost Pressures:** Feed costs peaked in 2008 and 2022. Replacement cow prices surged to all-time highs post-2020, squeezing farmer margins.

## Data Preparation & Modeling
**Data Source:** USDA Economic Research Service (*U.S. quarterly milk production and related data*, published Aug 2026).

**ETL & Data Cleaning (Power Query):**
*   Stripped footnote markers (`¹ ² ³`) from metric names.
*   **Grain Split:** Separated the raw data into two distinct Fact tables (`Quarterly` and `Annual`) to prevent double-counting.
*   **Null Handling:** Preserved 2013 Q1–Q2 missing values (unavailable in source) rather than imputing them.
*   **Partial Data Management:** Excluded 2026 from YoY calculations as the year is incomplete (only Q1–Q2 available).

**Data Model (Star Schema):**
*   **Fact Tables:** `MilkData_Quarterly`, `MilkData_Annual`
*   **Dimensions:** `Calendar` (marked as date table), `DimMetric`
*   **Relationships:** 4 total, all 1:many, all single-direction. No ambiguous paths.

**DAX Highlights:**
*   Used `CALCULATE` to filter metrics dynamically through the dimension table.
*   Differentiated between **Flow variables** (SUM for production) and **Stock variables** (AVERAGE for herd size and prices).
*   Implemented Time Intelligence (`SAMEPERIODLASTYEAR`) for YoY growth calculations.
*   Created "Latest Snapshot" measures using `LASTNONBLANK` for the KPI cards.

## Known Limitations
*   **No milk price column** in the source data — the classic USDA milk-feed ratio cannot be calculated.
*   **2013 Q1–Q2** milk cow and yield values are null per the source.
*   **2026 is partial** (Q1–Q2 only).

## Repository Structure
*   `milk-production-dashboard.pbix` - The interactive Power BI file.
*   `data/` - The raw untouched USDA Excel file.
*   `powerbi/screenshots/` - Page images for quick viewing.
---

*Built by [Medupi Reginald Mathunyane]
