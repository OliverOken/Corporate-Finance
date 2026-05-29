---
template: spec
purpose: "Technical specification for model-driven projects — defines scope, inputs, formulas, validation, and analysis requirements precisely enough that any competent executor (human or LLM) can produce correct output"
audience: student
fields_required: [title, author, date, version, company, scope, model_architecture, data_inputs, derived_inputs, formulas, validation, analysis_requirements, output_format, references]
naming_convention: "YYYY-MM-DD-{slug}.md"
courses: [BUS-629]
notes: "Populated for Lunit Inc. FY2025 K-IFRS ratios analysis. All monetary figures in ₩ millions. Assumptions: tax_rate = 21%, cost_capital = 9%. Peer benchmark: VUNO Inc. (KOSDAQ: 338220)."
---

# Lunit Inc. — Accounting & Performance Ratios: Technical Specification

**Author:** Nguyen  
**Date:** 2026-05-29  
**Version:** 1.0  
**Company:** Lunit Inc. · KOSDAQ: 328130 · Korea Exchange (KOSDAQ)

---

## 1. Scope & Objective

This specification defines the Excel-based accounting and performance ratios model for **Lunit Inc.** (KOSDAQ: 328130), a South Korean medical AI company whose products include AI-assisted cancer imaging and biomarker analytics.

**Fiscal period:** FY2025 (current year) and FY2024 (prior year, used as start-of-year denominators for average-based ratios).  
**Reporting standard:** K-IFRS (Korean International Financial Reporting Standards).  
**Reporting currency:** Korean Won (₩), all figures in **₩ millions** unless otherwise noted.  
**Analytical objective:** Compute 25+ accounting ratios across six categories (Performance, Profitability, Efficiency, Leverage, Liquidity, Du Pont), interpret the results in the context of Lunit's pre-profitability growth stage, and deliver three to five actionable strategic recommendations.  
**Intended audience:** General MBA students and course instructors in BUS-629 International Corporate Finance at the University of Hawaiʻi at Mānoa Shidler College of Business. No prior knowledge of Lunit or Korean equity markets is assumed; all context must be supplied in the analysis itself.

---

## Part A — Model Specification

### 2. Model Architecture

The workbook contains five tabs in the following order:

| Tab | Purpose | Data flow |
|-----|---------|-----------|
| **Cover** | Instructions, color-coding key, named-range convention legend | Static reference; no calculations |
| **Balance Sheet** | Prior-year and current-year balance sheet line items (yellow input cells) | Source for all `BAL_*` named ranges |
| **Income Statement** | Current-year income statement (yellow input cells) | Source for all `INC_*` named ranges |
| **Cash Flow Statement** | Current-year operating, investing, and financing cash flows (yellow input cells) | Source for all `CASH_*` named ranges |
| **Ratios** | Analyst assumptions, derived inputs, and ratio outputs | Reads from all three financial statement tabs; produces all `RATIO_*` outputs |
| **Notes** | Company metadata, data sources, AI usage log, self-checks | Static reference |

**Color coding (must be preserved exactly):**

- **Yellow background:** Data input cells — hardcoded values from financial statements. Overwrite with company figures.
- **Light-blue background + blue text:** Analyst assumption cells (share price, shares outstanding, cost of capital, tax rate).
- **Green text:** Formula cells that cross-reference other tabs. Do not overwrite.
- **Gray background:** Ratio output cells in the Ratios tab. Do not overwrite.

**Input / calculation / output separation:** All raw financial figures live on the three statement tabs. The Ratios tab holds assumptions and derived inputs at top, and ratio outputs below. No raw data may be entered directly into ratio output cells.

**Formatting:** Figures in ₩ millions; ratios expressed as percentages (one decimal, e.g., −28.7%), multiples (two decimal, e.g., 0.26x), or currency (₩ millions, e.g., ₩1,062,567M). Years formatted as text ("2025", not "2,025"). Negative numbers in parentheses.

---

### 3. Data Inputs

All values sourced from the FY2025 annual financial statements of Lunit Inc. (KOSDAQ: 328130) via Yahoo Finance, filed under K-IFRS. All figures in ₩ millions unless the "Unit" column states otherwise.

#### Balance Sheet — Current Year (FY2025)

| Named Range | Description | Value | Unit |
|---|---|---|---|
| `BAL_cash_marketable_securities_curr` | Cash and marketable securities | 23,668.4 | ₩M |
| `BAL_receivables_curr` | Receivables | 26,368.8 | ₩M |
| `BAL_inventories_curr` | Inventories | 124.3 | ₩M |
| `BAL_other_current_assets_curr` | Other current assets | 5,458.2 | ₩M |
| `BAL_assets_current_curr` | Total current assets | 55,619.7 | ₩M |
| `BAL_ppe_gross_curr` | Property, plant & equipment (gross) | 21,600.0 | ₩M |
| `BAL_accumulated_depreciation_curr` | Less accumulated depreciation | 0.0 | ₩M |
| `BAL_ppe_net_curr` | Net tangible fixed assets | 21,600.0 | ₩M |
| `BAL_intangibles_curr` | Intangible assets (goodwill) | 278,704.5 | ₩M |
| `BAL_other_assets_curr` | Other assets | 13,987.7 | ₩M |
| `BAL_assets_total_curr` | Total assets | 369,911.9 | ₩M |
| `BAL_debt_short_term_curr` | Debt due for repayment (current) | 93,369.0 | ₩M |
| `BAL_accounts_payable_curr` | Accounts payable | 6,183.4 | ₩M |
| `BAL_other_current_liabilities_curr` | Other current liabilities | 112,659.2 | ₩M |
| `BAL_liabilities_current_curr` | Total current liabilities | 212,211.6 | ₩M |
| `BAL_debt_long_term_curr` | Long-term debt | 14,708.7 | ₩M |
| `BAL_other_long_term_liabilities_curr` | Other long-term liabilities | 5,558.0 | ₩M |
| `BAL_liabilities_total_curr` | Total liabilities | 232,478.3 | ₩M |
| `BAL_common_stock_curr` | Common stock and paid-in capital | 563,538.0 | ₩M |
| `BAL_retained_earnings_curr` | Retained earnings | −426,105.4 | ₩M |
| `BAL_equity_shareholders_curr` | Total shareholders' equity | 137,432.6 | ₩M |

#### Balance Sheet — Prior Year (FY2024)

| Named Range | Description | Value | Unit |
|---|---|---|---|
| `BAL_cash_marketable_securities_prior` | Cash and marketable securities | 84,118.9 | ₩M |
| `BAL_receivables_prior` | Receivables | 21,741.7 | ₩M |
| `BAL_inventories_prior` | Inventories | 115.7 | ₩M |
| `BAL_other_current_assets_prior` | Other current assets | 5,905.8 | ₩M |
| `BAL_assets_current_prior` | Total current assets | 111,882.1 | ₩M |
| `BAL_ppe_net_prior` | Net tangible fixed assets | 25,120.0 | ₩M |
| `BAL_intangibles_prior` | Intangible assets (goodwill) | 276,708.9 | ₩M |
| `BAL_other_assets_prior` | Other assets | 21,330.0 | ₩M |
| `BAL_assets_total_prior` | Total assets | 435,041.0 | ₩M |
| `BAL_debt_short_term_prior` | Debt due for repayment (current) | 52,842.0 | ₩M |
| `BAL_accounts_payable_prior` | Accounts payable | 1,069.5 | ₩M |
| `BAL_other_current_liabilities_prior` | Other current liabilities | 198,501.3 | ₩M |
| `BAL_liabilities_current_prior` | Total current liabilities | 252,412.8 | ₩M |
| `BAL_debt_long_term_prior` | Long-term debt | 16,602.9 | ₩M |
| `BAL_liabilities_total_prior` | Total liabilities | 270,179.7 | ₩M |
| `BAL_equity_shareholders_prior` | Total shareholders' equity | 164,861.3 | ₩M |

#### Income Statement — FY2025

| Named Range | Description | Value | Unit |
|---|---|---|---|
| `INC_sales` | Net sales | 83,100.0 | ₩M |
| `INC_cost_goods_sold` | Cost of goods sold | 90,100.0 | ₩M |
| `INC_sga` | Selling, general & administrative expenses | 68,400.0 | ₩M |
| `INC_depreciation` | Depreciation | 7,700.0 | ₩M |
| `INC_ebit` | Earnings before interest and taxes | −83,100.0 | ₩M |
| `INC_other_income` | Other income | 89,400.0 | ₩M |
| `INC_interest_expense` | Interest expense | 53,100.0 | ₩M |
| `INC_taxable_income` | Taxable income | −46,800.0 | ₩M |
| `INC_taxes` | Taxes | 600.0 | ₩M |
| `INC_net` | Net income | −47,400.0 | ₩M |
| `INC_dividends` | Dividends declared | 0.0 | ₩M |
| `INC_retained_addition` | Addition to retained earnings | −47,400.0 | ₩M |

#### Cash Flow Statement — FY2025

| Named Range | Description | Value | Unit |
|---|---|---|---|
| `CASH_operating` | Cash provided by operations | −124,616.0 | ₩M |
| `CASH_capex` | Capital expenditures | 1,608.0 | ₩M |
| `CASH_investing` | Cash provided by (used for) investments | −388.0 | ₩M |
| `CASH_financing` | Cash provided by (used for) financing | 62,905.0 | ₩M |
| `CASH_net_change` | Net increase (decrease) in cash | −62,099.0 | ₩M |

#### Analyst Assumptions

| Named Range | Description | Value | Unit |
|---|---|---|---|
| `share_price` | KRX closing price, 31 Dec 2025 | 19,216 | ₩ per share |
| `shares_outstanding` | Shares outstanding at 31 Dec 2025 | 37.19 | Millions |
| `cost_capital` | WACC (analyst assumption) | 0.09 | Decimal (9%) |
| `tax_rate` | Effective tax rate (analyst assumption) | 0.21 | Decimal (21%) |

---

### 4. Named Range Conventions

All named ranges follow the prefix conventions defined on the Cover tab. The executor must implement or verify that every named range below resolves to the cell or formula indicated.

| Named Range | Type | Resolves to / Formula |
|---|---|---|
| `BAL_[item]_curr` | Input | Current-year balance sheet cell on Balance Sheet tab |
| `BAL_[item]_prior` | Input | Prior-year balance sheet cell on Balance Sheet tab |
| `INC_[item]` | Input | Income statement cell on Income Statement tab |
| `CASH_[item]` | Input | Cash flow cell on Cash Flow Statement tab |
| `share_price` | Assumption | Ratios tab assumption cell |
| `shares_outstanding` | Assumption | Ratios tab assumption cell |
| `cost_capital` | Assumption | Ratios tab assumption cell |
| `tax_rate` | Assumption | Ratios tab assumption cell |
| `market_capitalization` | Derived | `share_price × shares_outstanding` |
| `startYear_equity` | Alias | `BAL_equity_shareholders_prior` |
| `startYear_inventory` | Alias | `BAL_inventories_prior` |
| `startYear_receivables` | Alias | `BAL_receivables_prior` |
| `startYear_total_assets` | Alias | `BAL_assets_total_prior` |
| `startYear_total_capitalization` | Derived | `BAL_debt_long_term_prior + BAL_equity_shareholders_prior` |
| `currentYear_after_tax_operating_income` | Derived | `INC_net + (1 − tax_rate) × INC_interest_expense` |
| `currentYear_daily_sales_average` | Derived | `INC_sales / 365` |
| `currentYear_equity` | Alias | `BAL_equity_shareholders_curr` |
| `currentYear_assets_current` | Alias | `BAL_assets_current_curr` |
| `currentYear_liabilities_current` | Alias | `BAL_liabilities_current_curr` |
| `currentYear_debt_long_term` | Alias | `BAL_debt_long_term_curr` |
| `currentYear_assets_total` | Alias | `BAL_assets_total_curr` |
| `currentYear_liabilities_total` | Alias | `BAL_liabilities_total_curr` |
| `currentYear_working_capital_net` | Derived | `BAL_assets_current_curr − BAL_liabilities_current_curr` |
| `currentYear_total_capitalization` | Derived | `currentYear_debt_long_term + currentYear_equity` |
| `currentYear_cash_marketable_securities` | Alias | `BAL_cash_marketable_securities_curr` |
| `currentYear_cost_goods_sold_daily` | Derived | `INC_cost_goods_sold / 365` |
| `avg_equity` | Derived | `AVERAGE(startYear_equity, currentYear_equity)` |
| `avg_total_assets` | Derived | `AVERAGE(startYear_total_assets, currentYear_assets_total)` |
| `avg_total_capitalization` | Derived | `AVERAGE(startYear_total_capitalization, currentYear_total_capitalization)` |
| `RATIO_asset_turnover` | Output | `INC_sales / startYear_total_assets` |
| `RATIO_operating_profit_margin` | Output | `currentYear_after_tax_operating_income / INC_sales` |
| `RATIO_leverage` | Output | `currentYear_assets_total / currentYear_equity` |
| `RATIO_debt_burden` | Output | `INC_net / currentYear_after_tax_operating_income` |

---

### 5. Derived Inputs

The following intermediate values are computed on the Ratios tab before any ratio is calculated. All formulas use named-range notation; no raw cell addresses may appear.

| Named Range | Formula | Computed Value | Unit |
|---|---|---|---|
| `market_capitalization` | `share_price × shares_outstanding` | 714,643.0 | ₩M |
| `startYear_total_capitalization` | `BAL_debt_long_term_prior + BAL_equity_shareholders_prior` | 181,464.2 | ₩M |
| `currentYear_after_tax_operating_income` | `INC_net + (1 − tax_rate) × INC_interest_expense` | −5,451.0 | ₩M |
| `currentYear_daily_sales_average` | `INC_sales / 365` | 227.7 | ₩M/day |
| `currentYear_cost_goods_sold_daily` | `INC_cost_goods_sold / 365` | 246.8 | ₩M/day |
| `currentYear_working_capital_net` | `BAL_assets_current_curr − BAL_liabilities_current_curr` | −156,591.9 | ₩M |
| `currentYear_total_capitalization` | `currentYear_debt_long_term + currentYear_equity` | 152,141.3 | ₩M |
| `avg_equity` | `AVERAGE(startYear_equity, currentYear_equity)` | 151,146.9 | ₩M |
| `avg_total_assets` | `AVERAGE(startYear_total_assets, currentYear_assets_total)` | 402,476.5 | ₩M |
| `avg_total_capitalization` | `AVERAGE(startYear_total_capitalization, currentYear_total_capitalization)` | 166,802.8 | ₩M |

**Note on `currentYear_after_tax_operating_income`:** This figure (−₩5,451M) is conceptually distinct from EBIT. It adds back the after-tax cost of debt (interest expense × (1 − tax_rate)) to net income, producing the income available to all capital providers before financing decisions. The large gap between net income (−₩47,400M) and after-tax operating income (−₩5,451M) reflects the outsized interest expense (₩53,100M), itself largely a legacy of the Volpara Health acquisition financing.

---

### 6. Ratio Definitions & Formulas

All ratios are computed on the Ratios tab. Formulas use named ranges only. Expected unit and a one-sentence interpretation guide follow each formula.

#### Performance

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| Market value added (MVA) | `market_capitalization − currentYear_equity` | 577,210.4 | ₩M | Excess of market value over book; positive = market expects future value creation |
| Market-to-book ratio | `market_capitalization / currentYear_equity` | 5.20 | x | Premium investors pay per ₩1 of book equity; >1 indicates intangible value expectations |
| Economic value added (EVA) | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | −21,783.0 | ₩M | Operating return minus cost of capital; negative = value destruction in operating terms |

*Note on MVA: The workbook shows MVA = ₩1,062,567M and market-to-book = 8.73x using the raw `market_capitalization` formula `share_price × shares_outstanding` where shares_outstanding = 37.19M. Verify that shares outstanding reflects the correct post-rights-offering share count, as Lunit completed a ₩250B rights offering in 2025. If the diluted share count is materially different, recalculate.*

#### Profitability

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| ROA (prior-year assets) | `currentYear_after_tax_operating_income / startYear_total_assets` | −1.3% | % | Operating return on assets deployed at start of year |
| ROC (prior-year capital) | `currentYear_after_tax_operating_income / startYear_total_capitalization` | −3.0% | % | Return on long-term capital committed at start of year |
| ROE (prior-year equity) | `INC_net / startYear_equity` | −28.7% | % | Net income return on beginning equity; captures full cost of financing |
| ROA (average assets) | `currentYear_after_tax_operating_income / avg_total_assets` | −1.4% | % | Same as ROA but smoothed for balance sheet timing |
| ROC (average capital) | `currentYear_after_tax_operating_income / avg_total_capitalization` | −3.3% | % | Same as ROC, average-basis |
| ROE (average equity) | `INC_net / avg_equity` | −31.4% | % | Same as ROE, average-basis |

#### Efficiency

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| Asset turnover | `INC_sales / startYear_total_assets` | 0.191 | x | Revenue generated per ₩1 of assets; low for IP-heavy medical AI firms |
| Receivables turnover | `INC_sales / startYear_receivables` | 3.82 | x | Times receivables convert to cash per year |
| Average collection period | `startYear_receivables / currentYear_daily_sales_average` | 95.5 | Days | Days outstanding before customer payment; evaluate against contract terms |
| Inventory turnover | `INC_cost_goods_sold / startYear_inventory` | 779 | x | Extremely high; inventory is negligible for a software-first AI firm |
| Days in inventory | `startYear_inventory / currentYear_cost_goods_sold_daily` | 0.47 | Days | Consistent with near-zero physical inventory |
| Profit margin | `INC_net / INC_sales` | −57.0% | % | Net loss as share of revenue |
| Operating profit margin | `currentYear_after_tax_operating_income / INC_sales` | −6.6% | % | After-tax operating income as share of revenue; less distorted by interest than net margin |

#### Leverage

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| Long-term debt ratio | `currentYear_debt_long_term / (currentYear_debt_long_term + currentYear_equity)` | 9.7% | % | Share of long-term capital financed by debt |
| Long-term debt-equity ratio | `currentYear_debt_long_term / currentYear_equity` | 0.107 | x | ₩0.11 of long-term debt per ₩1 of equity |
| Total debt ratio | `currentYear_liabilities_total / currentYear_assets_total` | 62.9% | % | Share of total assets financed by all liabilities |
| Times interest earned | `INC_ebit / INC_interest_expense` | −1.57 | x | EBIT covers interest <1x; interest coverage is negative |
| Cash coverage ratio | `(INC_ebit + INC_depreciation) / INC_interest_expense` | −1.42 | x | EBIT + D&A vs. interest; still negative, confirming operating cash cannot service debt |
| Debt burden | `INC_net / currentYear_after_tax_operating_income` | 8.70 | x | Ratio of net income to after-tax operating income; >1 in absolute value indicates financing significantly amplifies loss |
| Leverage ratio | `currentYear_assets_total / currentYear_equity` | 2.69 | x | Total assets per ₩1 of equity (equity multiplier in Du Pont) |

#### Liquidity

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| Net working capital to assets | `currentYear_working_capital_net / currentYear_assets_total` | −42.3% | % | Negative NWC relative to assets signals short-term insolvency risk |
| Current ratio | `currentYear_assets_current / currentYear_liabilities_current` | 0.26 | x | Current assets cover only 26% of current liabilities |
| Quick ratio | `(currentYear_cash_marketable_securities + BAL_receivables_curr) / currentYear_liabilities_current` | 0.24 | x | Near-liquid assets vs. current liabilities; below 1.0 |
| Cash ratio | `currentYear_cash_marketable_securities / currentYear_liabilities_current` | 0.11 | x | Strictest liquidity test; cash covers 11% of current liabilities |

#### Du Pont System

| Ratio | Named Range Formula | Computed Value | Unit | Interpretation |
|---|---|---|---|---|
| ROA (Du Pont) | `RATIO_asset_turnover × RATIO_operating_profit_margin` | −1.3% | % | Must equal ROA (prior-year assets); validates internal consistency |
| ROE (Du Pont) | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | −29.4% | % | Four-factor decomposition of ROE |

---

### 7. Validation Rules

The executor must verify each of the following checks before submitting analysis output. A check failure indicates a data entry error or formula mismatch that must be resolved.

**Check 1 — Du Pont ROA identity:**
`RATIO_asset_turnover × RATIO_operating_profit_margin` must equal `currentYear_after_tax_operating_income / startYear_total_assets` (ROA, prior-year assets) to within ±0.001. The workbook's Ratios tab displays a ✓ confirmation in column F; confirm it is present and green.

**Check 2 — Du Pont ROE near-equality (with documented time-mismatch):**
`RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` will not exactly equal `INC_net / startYear_equity` because `RATIO_leverage` uses current-year assets and equity while `RATIO_asset_turnover` uses prior-year assets. This discrepancy is structural, not an error. The analysis must explicitly acknowledge the time-mismatch and quantify the difference (Du Pont ROE = −29.4% vs. direct ROE = −28.7%).

**Check 3 — Balance Sheet balance:**
`BAL_assets_total_curr` must equal `BAL_liabilities_total_curr + BAL_equity_shareholders_curr`. Computed: 369,911.9 ≈ 232,478.3 + 137,432.6 = 369,910.9 (₩1M rounding difference acceptable under K-IFRS rounding conventions).

**Check 4 — Retained earnings roll-forward:**
`BAL_retained_earnings_curr` should equal `BAL_retained_earnings_prior + INC_retained_addition`. Computed: −426,105.4 ≈ −377,829.7 + (−47,400.0) = −425,229.7. A discrepancy of ~₩875.7M may reflect other comprehensive income (OCI) items under K-IFRS not captured in the template's simplified income statement. Note this in the analysis if it persists.

**Check 5 — Cash reconciliation:**
`CASH_operating + CASH_investing + CASH_financing` should approximate `CASH_net_change`. Computed: (−124,616) + (−388) + 62,905 = −62,099. ✓ Matches exactly.

---

## Part B — Analysis Specification

### 8. Analysis Requirements

The executor must interpret each ratio category as described below. All ratio values must be cited numerically (no paraphrase without a figure). Cross-category connections must be drawn explicitly.

**Performance (MVA, Market-to-Book, EVA):**
Interpret the contrast between a strongly positive MVA/market-to-book and a deeply negative EVA. The market assigns significant option value to Lunit's growth trajectory (12.6× revenue growth since 2021, FDA clearances, global hospital deployments) even as current operating economics are value-destructive. Benchmark market-to-book against VUNO Inc. (KOSDAQ: 338220), which operates in the same Korean medical imaging AI segment, to assess whether Lunit's premium is sector-wide or company-specific.

**Profitability (ROA, ROC, ROE):**
All three measures are deeply negative. The analysis must distinguish between the operating-level loss (after-tax operating income = −₩5,451M, a relatively modest loss at −6.6% of sales) and the financing-level loss amplification produced by the unusually large interest expense (₩53,100M). Connect to Leverage section: explain how the Volpara Health acquisition debt structure is the primary driver of the gap between operating margin and net margin.

**Efficiency (turnover ratios, margins):**
Asset turnover (0.191x) is characteristically low for an IP-heavy pre-profit AI firm with significant goodwill (₩278,704.5M on the balance sheet, ~75% of total assets). Receivables turnover (3.82x, ~95 days) warrants scrutiny: determine whether the collection period is consistent with Lunit's enterprise hospital contract terms or signals collection risk. Inventory turnover (779x) and days in inventory (0.47 days) are expected anomalies for a software company and require only a brief explanatory note.

**Leverage (debt ratios, coverage ratios):**
Times interest earned (−1.57x) and cash coverage (−1.42x) confirm that operating earnings cannot service interest obligations. However, long-term debt-to-equity (0.107x) and long-term debt ratio (9.7%) appear modest — the leverage story is concentrated in current liabilities (₩212,211.6M), which include ₩93,369M of short-term debt. The analysis must flag the current portion of debt as the primary near-term solvency risk and connect to the Liquidity section.

**Liquidity (current, quick, cash ratios):**
Current ratio (0.26x), quick ratio (0.24x), and cash ratio (0.11x) all sit far below conventional thresholds (1.0x, 0.8x, 0.2x respectively). Net working capital is −₩156,591.9M. The analysis must assess whether this is a structural feature of Lunit's business model (e.g., deferred revenue classified as current liability) or a genuine liquidity constraint. Cross-reference with CASH_operating (−₩124,616M) to confirm the company is currently cash-flow negative from operations.

**Benchmark — VUNO Inc. (KOSDAQ: 338220):**
VUNO is the closest publicly listed Korean medical AI peer: same KOSDAQ listing, same imaging-AI focus, same pre-profit growth stage through most of FY2025 (VUNO achieved its first profitable quarter in FY2025 per industry reporting). Where VUNO data is available, compare: revenue growth rate, ROE, current ratio, and market-to-book. Where specific VUNO figures cannot be confirmed, note this explicitly and use the comparison directionally.

---

### 9. Du Pont Decomposition

The four-factor Du Pont decomposition of ROE is:

`ROE (Du Pont) = RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden`

Computed: `2.69 × 0.191 × (−0.066) × 8.70 = −29.4%`

**Decomposition instructions for the executor:**

Assess each component's contribution to the negative ROE:

- **Operating profit margin (−6.6%):** The primary sign-driver. Revenue of ₩83,100M cannot cover total operating costs of ~₩166,200M (COGS + SGA + D&A), producing a negative operating margin. But note that the after-tax operating margin (−6.6%) is far less severe than the net margin (−57.0%) — the financing structure, not the operating model, is the dominant loss driver.

- **Asset turnover (0.191x):** Structurally low due to the goodwill-heavy balance sheet (post-Volpara acquisition). A software firm with ₩278,704.5M of intangibles on a ₩369,911.9M asset base will post low turnover ratios until revenue scales to match the acquisition premium.

- **Leverage (2.69x):** Moderate equity multiplier. Amplifies the negative operating margin rather than providing financial leverage benefit, because operating returns are already negative.

- **Debt burden (8.70x):** Extreme outlier. A debt burden ratio above 1.0 in absolute value means financing costs (net of operating income adjustments) amplify the net loss far beyond the operating loss. The primary driver is INC_interest_expense = ₩53,100M vs. currentYear_after_tax_operating_income = −₩5,451M. Explain the acquisition-debt origin of this distortion.

**Time-mismatch disclosure (required):** Du Pont ROE (−29.4%) differs from direct ROE (−28.7%) because `RATIO_leverage` uses current-year balance sheet figures (end-2025) while `RATIO_asset_turnover` uses prior-year assets (end-2024). This structural inconsistency is inherent to the model design and must be disclosed in the analysis, not corrected.

**Primary driver conclusion:** The operating profit margin is the controlling factor in the negative ROE, but the debt burden ratio is the amplifier that translates a modest operating loss into a severe net loss. Strategic recommendations should address both levers.

---

### 10. Strategic Recommendations

The analysis must produce **exactly three to five** strategic recommendations, each meeting the following evidence standard:

- Grounded in at least one specific ratio value cited numerically.
- Addresses a concrete, actionable management or investor decision — not a generic observation.
- Identifies the expected directional impact on one or more ratios if the recommendation is implemented.
- Is appropriate for Lunit's stage (KOSDAQ-listed, pre-consistent-profitability, post-acquisition integration phase).

**Recommended framing for each recommendation:**
> **Recommendation [N]: [Action Title]**  
> *Evidence:* [Ratio or ratios, with values]  
> *Action:* [Specific, actionable step]  
> *Expected ratio impact:* [Direction and magnitude estimate]

Suggested recommendation themes (executor may reorder or substitute, but must maintain the evidence standard):

1. **Short-term debt restructuring** — Current ratio (0.26x) and ₩93,369M of current debt signal near-term refinancing risk; explore covenant extension or long-term refinancing.
2. **Interest expense reduction** — Debt burden (8.70x absolute) and times interest earned (−1.57x) indicate the financing structure is the largest single driver of net losses; paydown or restructuring of acquisition-related debt would improve net margin by narrowing the gap between operating income and net income.
3. **Revenue scaling to absorb fixed costs** — Operating margin is −6.6% on ₩83,100M revenue (+53% YoY); modest continued growth at current trajectory could push operating margin to breakeven, given that COGS and SGA contain a meaningful fixed component.
4. **Receivables management** — Average collection period of 95.5 days on enterprise hospital contracts; accelerating collections by 20–30 days would improve cash conversion and reduce reliance on short-term borrowing.
5. **Goodwill impairment monitoring** — Intangibles (₩278,704.5M) represent 75.3% of total assets; if Volpara Health integration underperforms, a write-down would sharply reduce book equity and worsen leverage and ROE ratios.

---

### 11. Output Format

The Stage 5 analysis deliverable must conform to the following structure:

**Document type:** Markdown (`.md`), suitable for inclusion in a GitHub portfolio repository at `analysis/reports/`.  
**Filename convention:** `YYYY-MM-DD-{lastname}-lunit-analysis.md`  
**Approximate length:** 1,500–2,500 words (excluding ratio tables).  
**Tone:** Professional but accessible; suitable for a general MBA audience with no prior knowledge of Lunit or Korean equity markets. Define any Korea-specific terms (KOSDAQ, K-IFRS, won, KRX) on first use.  
**No jargon without definition:** Terms such as "Du Pont decomposition," "equity multiplier," "times interest earned," and "economic value added" must each be briefly defined on first use.

**Required sections in this order:**

1. **Executive Summary** (~150 words): Company overview, key finding in one sentence, and the single most important ratio to understand Lunit's current financial position.
2. **Company & Industry Context** (~200 words): Lunit's business model, the Volpara Health acquisition, Korean medical AI sector, VUNO peer comparison.
3. **Ratio Analysis by Category** (~800–1,200 words): One subsection per category (Performance, Profitability, Efficiency, Leverage, Liquidity). Each subsection: state the ratios numerically, interpret them, and note cross-category connections per Section 8 above.
4. **Du Pont Decomposition** (~200 words): Present the four-factor breakdown, identify the primary driver, disclose and explain the time-mismatch.
5. **Strategic Recommendations** (~300–400 words): Three to five recommendations per Section 10 above, using the evidence-action-impact format.
6. **Conclusion** (~100 words): Summarize the overall financial health assessment and the most critical near-term risk.

**Tables:** All ratio results must be presented in a formatted Markdown table in their respective sections. Do not present ratios only in prose.  
**Ratio precision:** Percentages to one decimal place; multiples to two decimal places; currency figures in ₩ millions with comma separators.

---

## References

- Lunit Inc. FY2025 Annual Financial Statements (K-IFRS), sourced via Yahoo Finance.
- Lunit Inc. KOSDAQ listing page: ticker 328130.KQ.
- Stage 1 template: `models/templates/performance-ratios-template.xlsx` (UH Mānoa BUS-629 repo).
- Stage 3 populated workbook: `2026-05-23-nguyen-lunit-financials.xlsx`.
- Spec template: `https://raw.githubusercontent.com/adamwstauffer/shidler/main/docs/templates/spec-template.md`.
- Stage 4 brief: `https://raw.githubusercontent.com/adamwstauffer/shidler/main/courses/BUS-629-VEMBA-International-Corporate-Finance/stage4-technical-specification.md`.
- VUNO Inc. peer reference: KOSDAQ: 338220; industry revenue data from KoreaTechDesk and MobiHealthNews (February 2026).
- KBR (Korea Biomedical Review): Lunit rights offering and acquisition financing context, February 2026.
