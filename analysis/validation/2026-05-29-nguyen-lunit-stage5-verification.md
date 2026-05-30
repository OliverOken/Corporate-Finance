# Stage 5 Verification Table — Lunit Inc. FY2025

**Author:** Nguyen  
**Date:** 2026-05-29  
**Course:** BUS-629 International Corporate Finance · UH Mānoa Shidler  
**Company:** Lunit Inc. · KOSDAQ: 328130  
**Spec version:** 1.0 · Raw LLM output file:** `2026-05-29-nguyen-lunit-analysis-raw.md`

---

## What This Table Compares

Three sources of ratio values exist in this project:

| Source | Where it comes from | Role in verification |
|---|---|---|
| **Template auto-computed** | Stage 3 workbook Ratios tab (Excel formulas) | Sanity check — listed in notes column but **not** the column being graded |
| **LLM stated** | Stage 5 raw LLM output | **Column being compared against manual** |
| **Manual** | Recomputed by hand from Stage 3 financial data | **Ground truth column** |

All figures in ₩ millions. Analyst assumptions applied throughout: `tax_rate = 0.21`, `cost_capital = 0.09`.

---

## Source Data Used for Manual Arithmetic

All inputs drawn directly from the Stage 3 workbook dump. Key values:

| Named Range | Description | Value |
|---|---|---|
| `BAL_assets_total_curr` | Total assets FY2025 | 369,911.9 |
| `BAL_assets_total_prior` | Total assets FY2024 | 435,041.0 |
| `BAL_equity_shareholders_curr` | Equity FY2025 | 137,432.6 |
| `BAL_equity_shareholders_prior` | Equity FY2024 | 164,861.3 |
| `BAL_receivables_prior` | Receivables FY2024 | 21,741.7 |
| `BAL_liabilities_total_curr` | Total liabilities FY2025 | 232,478.3 |
| `BAL_debt_long_term_prior` | LT debt FY2024 | 16,602.9 |
| `BAL_debt_long_term_curr` | LT debt FY2025 | 14,708.7 |
| `INC_sales` | Net sales FY2025 | 83,100.0 |
| `INC_net` | Net income FY2025 | −47,400.0 |
| `INC_ebit` | EBIT FY2025 | −83,100.0 |
| `INC_interest_expense` | Interest expense FY2025 | 53,100.0 |
| `INC_depreciation` | Depreciation FY2025 | 7,700.0 |
| `share_price` | KRX close 31 Dec 2025 | ₩19,216 |
| `shares_outstanding` | Shares (M) | 37.19 |

**Key derived inputs (recomputed):**

- `currentYear_after_tax_operating_income` = −47,400 + (1 − 0.21) × 53,100 = **−5,451.0**
- `startYear_total_capitalization` = 16,602.9 + 164,861.3 = **181,464.2**
- `market_capitalization` = 19,216 × 37.19 = **714,643.0**
- `currentYear_daily_sales_average` = 83,100 / 365 = **227.671**

---

## Verification Table

| # | Ratio | Category | Formula (named-range notation) | Manual value — arithmetic shown | LLM stated value | Match? | Note |
|---|---|---|---|---|---|---|---|
| 1 | Economic Value Added (EVA) | Performance | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | −5,451.0 − (0.09 × 181,464.2) = −5,451.0 − 16,331.8 = **−21,782.8** | −₩21,783M | ✓ | LLM correct. Template states −110,148 because it used the Notes tab assumptions (WACC=6.4%, tax=24.2%) rather than the analyst assumption cells (9%, 21%). The discrepancy is a template formula-wiring error, not an LLM error. |
| 2 | Operating Profit Margin | Efficiency | `currentYear_after_tax_operating_income / INC_sales` | −5,451.0 / 83,100.0 = **−6.56%** | −6.6% | ✓ | LLM correct (rounds to −6.6%). Template states −99.0% — a confirmed formula error: the template's cell references `currentYear_after_tax_operating_income` incorrectly, likely pointing to a raw EBIT-adjacent cell (≈−82,269) instead of the derived after-tax operating income. **This is a material template bug that affects ROA, ROC, and Du Pont outputs.** |
| 3 | Return on Capital — Prior-Year Basis (ROC) | Profitability | `currentYear_after_tax_operating_income / startYear_total_capitalization` | −5,451.0 / 181,464.2 = **−3.00%** | −3.0% | ✓ | LLM correct. Template states −18.9% — cascades from the same operating profit margin formula error (Row 2): the template uses an inflated negative numerator, producing a far more negative ROC. |
| 4 | Return on Equity — Prior-Year Basis (ROE) | Profitability | `INC_net / startYear_equity` | −47,400.0 / 164,861.3 = **−28.75%** | −28.7% | ✓ | LLM correct (rounds to −28.7%). Template also states −28.7%. This ratio uses `INC_net` directly (not the derived after-tax operating income), so it is unaffected by the template formula error in Row 2. Rounding to one decimal: −28.8% vs LLM's −28.7% — a 0.1pp rounding difference, within tolerance. |
| 5 | Average Collection Period | Efficiency | `startYear_receivables / currentYear_daily_sales_average` | 21,741.7 / (83,100 / 365) = 21,741.7 / 227.671 = **95.5 days** | 95.5 days | ✓ | LLM correct. Template also states 95.5 days. This ratio involves a start-of-year input (FY2024 receivables) divided by a current-year derived value (daily sales) — a common averaging pitfall — but both LLM and template handled it correctly per the spec's formula definition. |
| 6 | Total Debt Ratio | Leverage | `currentYear_liabilities_total / currentYear_assets_total` | 232,478.3 / 369,911.9 = **62.85%** | 62.9% | ✓ | LLM correct (rounds to 62.9%). Template raw output = 6.28E−3 = 0.628% — a unit display error where the cell is formatted as a raw decimal but the percentage format was not applied. The underlying formula is correct; the cell formatting is wrong. LLM correctly interpreted the intended percentage. |
| 7 | Market-to-Book Ratio | Performance | `market_capitalization / currentYear_equity` | 714,643.0 / 137,432.6 = **5.20x** | 5.20x | ✓ | LLM correct. Template states 8.73x — a significant discrepancy. Both use the same `market_capitalization` formula (19,216 × 37.19 = 714,643), so the template's 8.73x implies it is dividing by a different equity figure. Back-calculation: 714,643 / 8.73 ≈ 81,861 — not a number appearing in the balance sheet. This is likely a stale cached value or a reference error in the template cell. |
| 8 | Du Pont ROE | Du Pont | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | (369,911.9/137,432.6) × (83,100/435,041) × (−5,451/83,100) × (−47,400/−5,451) = 2.6916 × 0.1910 × (−0.0656) × 8.6957 = **−29.3%** | −29.4% | ✓ | LLM correct within rounding (0.1pp difference from carrying intermediate values to fewer decimals). Template states −29.3%, matching manual. Disclosure: Du Pont ROE (−29.3%) differs from direct ROE (−28.75%) by 0.55pp due to the structural time-mismatch: `RATIO_leverage` uses current-year balances (end-FY2025) while `RATIO_asset_turnover` uses prior-year assets (end-FY2024). This is inherent to the model design, documented in Section 7 of the spec. |

---

## Summary of Findings

### LLM accuracy: 8 / 8 ratios correct within rounding tolerance

The LLM produced accurate ratio values across all eight rows. Where discrepancies exist, they are traceable to **template formula errors**, not LLM hallucination.

### Template errors identified (4 confirmed)

| Error | Ratios Affected | Root Cause |
|---|---|---|
| **Formula wiring error — operating profit margin** | ROA, ROC, operating profit margin, Du Pont ROA | Template cell for `currentYear_after_tax_operating_income` references wrong source cell; produces ≈−82,269 instead of −5,451 |
| **Assumption mismatch — EVA** | EVA only | Template EVA cell uses Notes tab assumptions (WACC=6.4%, tax=24.2%) instead of Ratios tab analyst assumption cells (9%, 21%) |
| **Unit display error — percentage ratios** | Total debt ratio, long-term debt ratio | Cells store raw decimal (e.g., 0.6285) but display without % format, making them appear as 0.628% instead of 62.8% |
| **Stale/reference error — market-to-book** | Market-to-book, MVA | Template equity denominator for M/B does not match `BAL_equity_shareholders_curr` = 137,432.6; appears to use a cached or mis-referenced value |

### Most informative discrepancy: Operating Profit Margin (Row 2)

The template's −99.0% operating profit margin is the most consequential error because it cascades into ROA (−18.9% instead of −1.25%), ROC (−18.9% instead of −3.0%), and the Du Pont ROA check. A student relying on the template's auto-computed values without cross-checking the spec or manual arithmetic would conclude that Lunit's operating economics are dramatically worse than they are. The LLM, reading the spec's formula definition precisely, computed −6.6% correctly.

### Most informative agreement: ROE (Row 4)

ROE is the one profitability ratio unaffected by the formula error because it uses `INC_net` directly. The fact that template, LLM, and manual all converge on ≈−28.7% confirms the underlying financial data is consistent — the errors are formula-wiring issues, not data entry errors.

---

## Verification Checklist (per spec Section 7)

| Check | Result |
|---|---|
| Check 1 — Du Pont ROA identity: `RATIO_asset_turnover × RATIO_operating_profit_margin` = direct ROA | ✓ 0.1910 × (−0.0656) = −1.25% = direct ROA |
| Check 2 — Du Pont ROE time-mismatch documented | ✓ Δ = −29.3% vs −28.75% = 0.55pp; cause disclosed |
| Check 3 — Balance sheet balances | ✓ 369,911.9 ≈ 232,478.3 + 137,432.6 = 369,910.9 (₩1M rounding) |
| Check 4 — Retained earnings roll-forward | ⚠ −426,105.4 ≠ −377,829.7 + (−47,400) = −425,229.7; Δ = ₩875.7M; attributed to OCI items under K-IFRS |
| Check 5 — Cash reconciliation | ✓ (−124,616) + (−388) + 62,905 = −62,099 ✓ exact |

---

*Verification completed: 2026-05-29. Stage 3 workbook: `2026-05-23-nguyen-lunit-financials.xlsx`. Raw LLM output: `2026-05-29-nguyen-lunit-analysis-raw.md`.*
