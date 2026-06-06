# ENPA Project — Developer Notes

## Project Overview
ENPA is an educational app focused on **Non-Profit Organization (NPO) Accounting**, built as an interactive learning tool.

**Authors:** Muhammad Zaki bin Ab. Muluk, Zariyah binti Abdullah

---

## App Structure (from DRAF_ENPA.pptx)

The app has a main menu (Slide 3) with 4 modules:

| Option | Module    | Description                          |
|--------|-----------|--------------------------------------|
| A      | eBook     | Theory/reference content             |
| B      | Game      | Mix and Match interactive activity   |
| C      | Quiz      | Assessment questions                 |
| D      | Exercise  | Practice problems                    |

---

## Content Coverage

### Topic: Non-Profit Organization Accounts
Core financial statements covered:
1. **Receipts and Payments Account** — records all cash received/paid
2. **Subscriptions Account**
3. **Trading Account** (for club trading activities e.g. drinks)
4. **Income and Expenditure Account** — determines surplus/deficit
5. **Statement of Financial Position** (Balance Sheet)

### Example Case: Chess Club (year ended 31 August 2024)
Used throughout the app as the primary worked example.

Key figures from the Chess Club example:
- Subscriptions: 12,120
- Tournament fees: 1,300
- Profit from drinks: 1,962
- Surplus: 9,917
- Accrued subscription: 790
- Prepaid subscriptions: 600
- Accumulated fund: 34,500
- Cash: 34,960
- Sport equipment: 47,177 (total assets implied)

---

## Source Files

| File                  | Description                                      |
|-----------------------|--------------------------------------------------|
| `DRAF_ENPA.pptx`      | Full app draft (slides with all 4 modules)       |
| `DRAF_ENPA.pdf`       | PDF export of the pptx (same content)            |
| `Q_N_A_INOVASI.docx`  | Full Q&A for the Exercise/Quiz module            |

---

## Q&A Module Content (from Q_N_A_INOVASI.docx)

**Question:** Chess Club Receipt & Payment Account for year ended 31 Aug 2024.

Students are required to prepare:
- (a) Subscriptions account
- (b) Trading Account for the year ended 31 August 2024
- (c) Income and Expenditure account for the year ended 31 August 2024
- (d) Statement of Financial Position as at 31 August 2024

Additional info:
- Entrance subscriptions treated as capital receipt
- Balance of assets and liabilities given as additional information

---

## Dev Notes / TODOs
- [ ] Implement eBook module with NPO theory content
- [ ] Build Mix and Match game mechanic (matching accounting terms/figures)
- [ ] Build Quiz module (MCQ or short answer)
- [ ] Build Exercise module with worked example (Chess Club Q&A)
- [ ] Navigation between slides/modules (Slide 3 menu → A/B/C/D)
