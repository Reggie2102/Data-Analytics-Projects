

# U.S. Milk Production Analysis (1998–2026)

A Power BI dashboard analyzing 28 years of USDA quarterly milk production data. 
Explores long-term production trends, the split between herd size and yield per cow, 
and the trajectory of feed and replacement cow costs.

> **Built as a portfolio project** to demonstrate data cleaning, star-schema modeling, 
> DAX measure design, and dashboard storytelling in Power BI.

---

## Dashboard Preview

<img width="484" height="284" alt="Screenshot 2026-11-11 203428" src="https://github.com/user-attachments/assets/525acbab-a5cf-464a-851b-ebdb6e982cde" />


---

## Key Findings

- **Production grew 47%** from 1998 to 2025 (157B → 232B lbs), while the national 
  herd **shrank 3%** over the same period.
- **All production gains came from yield per cow**, which rose from 17,185 lbs/year 
  to 24,390 lbs/year (+42%). Herd size has been essentially flat since 2010.
- **Feed value peaked at $14.25/cwt** in 2022 Q3 — more than 3× the 1998 baseline — 
  but has normalized to $8.50–9.50 in 2024–2025.
- **Replacement cow prices hit an all-time high of $3,110/head** in 2025, suggesting 
  continued tightening of replacement supply.

---

## Repository Structure

---

## How It Was Built

**Data source:** USDA Economic Research Service, *U.S. quarterly milk production 
and related data* (published August 13, 2026).

**Cleaning & transformation:**
- Stripped footnote markers (`¹ ² ³`) from metric names
- Split quarterly and annual rows into two separate fact tables to avoid double-counting
- Preserved 2013 Q1–Q2 nulls (unavailable per USDA) — did not impute
- Excluded partial 2026 data (Q1–Q2 only) from year-over-year comparisons

**Data model (star schema):**
- **Fact tables:** `MilkData_Quarterly`, `MilkData_Annual`
- **Dimensions:** `Calendar` (marked as date table), `DimMetric`
- **Relationships:** 4 total, all 1:many, all single-direction

**DAX measures (12 total):**
- Core metrics: production, herd size, yield per cow, feed value, replacement price
- Time intelligence: year-over-year % for production, herd, yield, and feed
- Derived check: `Derived Milk per Cow` (production ÷ herd) to validate the stored yield value

---

## How to Open

1. Download `milk-production-dashboard.pbix`
2. Open in **Power BI Desktop** (free download from Microsoft)
3. All data is embedded — no external connection or credentials required

---

## What I Learned

- How to identify and separate **fact table grains** (quarterly vs. annual) to prevent silent double-counting
- How to build a **star schema** with a proper `Calendar` table and a metric dimension
- The difference between **SUM** (flow variables: production) and **AVERAGE** (stock variables: herd size, prices)
- How to write **`SAMEPERIODLASTYEAR`** measures and validate them against source values
- How to document data decisions so a reviewer can verify the numbers

---

## Known Limitations

- **No milk price column** in the source — the classic USDA milk-feed ratio cannot be computed from this data alone
- **2013 Q1–Q2** milk cow and yield values are null per the source
- **2026 is partial** (Q1–Q2 only at time of analysis)

---

## License

MIT - see [LICENSE](LICENSE) for details.

---

*Built by [Medupi Reginald Mathunyane]
[quarterly-milk-factors.xlsx](https://github.com/user-attachments/files/34585802/quarterly-milk-factors.xlsx)
