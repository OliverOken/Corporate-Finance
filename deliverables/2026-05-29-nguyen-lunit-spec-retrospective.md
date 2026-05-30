---
template: spec-retrospective
course: BUS-629
stage: 4
company: Lunit Inc.
ticker: KOSDAQ 328130
author: Nguyen
date: 2026-05-29
spec_file: docs/2026-05-29-nguyen-lunit-spec.md
raw_output_file: deliverables/2026-05-29-nguyen-lunit-analysis-raw.md
verification_file: analysis/validation/2026-05-29-nguyen-lunit-stage5-verification.md
effectiveness_rating: 4
---

# Spec Retrospective — Lunit Inc. FY2025 Ratios Analysis

---

## Section 1 — Section-by-Section Spec Verdict

Each section of the Stage 4 spec is evaluated as **Clear**, **Vague**, or **Missing**, with the symptom in the Stage 5 LLM output that justifies the verdict.

| # | Spec Section | Verdict | Symptom in Stage 5 Output |
|---|---|---|---|
| 1 | Scope & Objective | **Clear** | LLM correctly bounded the analysis to FY2025/FY2024, cited K-IFRS, used ₩M throughout, and addressed a general MBA audience without over-explaining or under-explaining Korean market context. |
| 2 | Model Architecture | **Clear** | LLM did not attempt to reference workbook tab names or color codes (correctly — it's an analysis document, not Excel instructions), indicating it correctly parsed the architecture section as workbook context rather than output instructions. |
| 3 | Data Inputs | **Clear** | All 25+ ratio computed values in the raw output matched the spec's stated values. No hallucinated figures detected across eight independently verified ratios. The named-range notation gave the LLM unambiguous formula anchors. |
| 4 | Named Range Conventions | **Clear** | LLM applied formulas correctly — e.g., used `startYear_receivables` (prior-year) rather than current-year receivables for average collection period, and `startYear_total_assets` for asset turnover. No silent averaging-convention errors found. |
| 5 | Derived Inputs | **Clear** | `currentYear_after_tax_operating_income = −5,451` was used correctly in all profitability, efficiency, and Du Pont calculations. The conceptual note distinguishing it from EBIT appeared verbatim in the analysis. |
| 6 | Ratio Definitions & Formulas | **Clear** | All six categories reproduced correctly. The one rounding difference (Du Pont ROE: LLM −29.4% vs manual −29.3%) is within single-decimal rounding tolerance and was disclosed. |
| 7 | Validation Rules | **Vague** | The spec told the LLM to verify checks before submitting, but gave no instruction on how or where to surface validation results in the final document. The LLM silently passed all checks and disclosed the Du Pont time-mismatch correctly — but did not produce a visible validation summary. A reader cannot confirm the checks were run. |
| 8 | Analysis Requirements (Sec. 8) | **Clear** | All five category-level interpretation briefs were followed: the profitability section distinguished operating vs. financing loss; leverage flagged current liabilities as the primary risk; liquidity raised the deferred revenue question; Du Pont identified the debt burden as the magnitude amplifier. |
| 9 | Du Pont Decomposition (Sec. 9) | **Clear** | Four-factor breakdown presented with individual factor values, primary driver identified (operating margin as sign driver, debt burden as magnitude amplifier), and time-mismatch disclosed and quantified. |
| 10 | Strategic Recommendations (Sec. 10) | **Vague** | The spec required each recommendation to use the exact framing: `**Recommendation [N]: [Title]** / *Evidence:* / *Action:* / *Expected ratio impact:*`. The LLM used blockquote formatting with bold sub-labels — structurally close but not precisely matching the template. A grader using the spec as a rubric would note the formatting deviation. |
| 11 | Output Format (Sec. 11) | **Clear** | Six-section structure followed in order. Word counts fell within prescribed ranges. All Korea-specific terms (KOSDAQ, K-IFRS, won, KRX) defined on first use. All ratio categories presented with Markdown tables. Jargon terms (Du Pont, equity multiplier, times interest earned, EVA) defined on first use. |

**Overall:** 9 Clear / 2 Vague / 0 Missing.

---

## Section 2 — Top Three Gaps with Evidence

### Gap 1: Validation output is invisible

**Where it surfaced:** Section 7 of the spec listed five validation checks and instructed the executor to verify them before submitting. The raw LLM output contains no validation section, no check summary, and no explicit confirmation that checks were run. The time-mismatch disclosure (Check 2) appears inline in the Du Pont section, but Checks 1, 3, 4, and 5 are not mentioned.

**What the spec caused:** The LLM interpreted "verify before submitting" as a pre-flight step it should perform internally, not a section it should surface in the output document. This is a reasonable interpretation — but it means a grader reviewing the analysis cannot confirm that the balance sheet was checked, the cash flow was reconciled, or the retained earnings discrepancy was noted.

**Exact language to add to spec:**

> After the Conclusion section, include a **Validation Appendix** with the following five-row table. Each row must state the check name, the computed result, and a Pass / Flag verdict. Flag any discrepancy with a one-sentence explanation.
>
> | Check | Result | Verdict |
> |---|---|---|
> | Du Pont ROA identity | [value] | Pass / Flag |
> | Du Pont ROE time-mismatch | Δ = [value]pp | Disclosed |
> | Balance sheet balance | [LHS] ≈ [RHS] | Pass / Flag |
> | Retained earnings roll-forward | [expected] vs [actual] | Pass / Flag |
> | Cash reconciliation | [sum] = [net change] | Pass / Flag |

---

### Gap 2: VUNO peer comparison lacked quantitative benchmarks

**Where it surfaced:** Section 3.1 (Performance) of the raw output compares Lunit's market-to-book of 5.20x against VUNO directionally ("expected to be in the 2–3x range") but cites no sourced VUNO figures. Section 8 of the spec said "where VUNO data is available, compare: revenue growth rate, ROE, current ratio, and market-to-book" and "where specific VUNO figures cannot be confirmed, note this explicitly and use the comparison directionally." The LLM followed the fallback clause correctly — but the spec gave no sourced VUNO data points to anchor the comparison, so the LLM could only speculate.

**What the spec caused:** A directional comparison ("Lunit's 5.20x premium suggests the market prices in Lunit's superior scale") that cannot be verified and reads as opinion rather than analysis. The grader cannot assess whether the peer framing is grounded.

**Exact language to add to spec:**

> **VUNO reference data (sourced, for use in analysis):** VUNO Inc. (KOSDAQ: 338220) reported FY2025 revenue of ₩34,800M (+34.4% YoY) and achieved its first profitable quarter in Q4 FY2025. Where market-to-book, current ratio, and ROE figures are not confirmed in this spec, the executor must state that specific VUNO figures were not available and limit the comparison to the revenue growth differential and profitability trajectory.

---

### Gap 3: Recommendation formatting was underspecified

**Where it surfaced:** The spec's Section 10 showed the required framing as:
```
**Recommendation [N]: [Action Title]**
*Evidence:* ...
*Action:* ...
*Expected ratio impact:* ...
```
The LLM output used blockquotes (`>`) around each recommendation and bolded the sub-labels but placed them on separate lines within the blockquote — visually similar but not structurally identical. A strict reading of the spec would flag this as a format deviation.

**What the spec caused:** Ambiguity between "framing" (conceptual structure) and "formatting" (exact Markdown syntax). "Recommended framing" is not the same instruction as "use exactly this Markdown structure."

**Exact language to add to spec:**

> Each recommendation must use **exactly** the following Markdown block, with no blockquotes, no additional wrappers, and no reordering of sub-labels:
>
> ```markdown
> **Recommendation 1: [Title]**
> *Evidence:* [ratio name and value]
> *Action:* [specific step]
> *Expected ratio impact:* [direction and estimated magnitude]
> ```
> Do not wrap recommendations in blockquotes or callout boxes.

---

## Section 3 — Three Revisions for the Next Run

**Revision 1 (addresses Gap 1 — Validation visibility):** Add a mandatory Validation Appendix section to Section 11's required output structure, with explicit instruction that each of the five checks must appear as a table row with Pass / Flag verdict. Elevate it from a pre-flight instruction to a graded output section.

**Revision 2 (addresses Gap 2 — VUNO data):** Before finalizing the spec, run a quick search for VUNO's most recent annual report metrics and embed four confirmed VUNO data points (revenue, ROE, current ratio, market-to-book) directly into Section 8. This converts the peer section from directional opinion to quantitative comparison — the difference between an observation and an argument.

**Revision 3 (addresses Gap 3 — Recommendation format):** Replace the phrase "recommended framing" with "required Markdown format" and include a fenced code block showing the exact syntax. Add the negative instruction: "Do not wrap recommendations in blockquotes or callout boxes." Formatting ambiguity is the most common cause of technically correct but structurally non-compliant outputs.

---

## Section 4 — Effectiveness Rating

**Rating: 4 / 5**

**Justification:**

The spec achieved its core purpose: an LLM reading it cold produced ratio values that were arithmetically correct across eight independently verified rows, structured the analysis in the prescribed six-section order, defined all required jargon, and delivered five recommendations with evidence-action-impact framing. That is a high bar, and the spec cleared it.

The rating stops at 4 rather than 5 for two reasons grounded in the verification output. First, the validation checks were invisible in the final document — a competent executor ran them internally but a grader cannot confirm it. A spec rated 5/5 should produce an output that is self-evidencing: a reader with no access to the spec should be able to verify that every required step was completed. Second, the VUNO peer comparison was directional rather than quantitative because the spec delegated the data-sourcing task to the LLM without providing anchors. A 5/5 spec is self-contained: the executor needs no external judgment calls.

The two Vague sections (validation surfacing and recommendation formatting) are both fixable with fewer than 50 words of additional instruction each — a high return on a low investment of spec effort.

---

## Section 5 — Forward Link

In the next spec, make the **output document self-evidencing**: every required step — validation, formatting conventions, peer benchmarks — should produce a visible artifact in the final document that a grader can check without re-running the analysis, treating "verify before submitting" as a hidden internal step and "include a Validation Appendix" as a graded deliverable.

---

## Section 6 — Retrospective Process Feedback (≤150 words)

The template's six-section structure is well-designed for catching what the spec caused vs. what the LLM chose — that distinction is the most analytically useful framing in the document. One structural suggestion: add a seventh item between Sections 1 and 2 called **"Surprise Finding"** — a single required row for something the LLM produced that the spec neither asked for nor anticipated, positive or negative. In this project, the most instructive finding was that the LLM outperformed the pre-built Excel template on four ratio categories (EVA, ROA, ROC, operating profit margin) because it read the spec's formula definitions precisely while the template had formula-wiring errors. That finding is buried in the verification table and absent from the retrospective. A mandatory surprise row would force analysts to surface unexpected outputs — which is often where the most durable spec-writing lessons live.

---

*Retrospective completed: 2026-05-29. Based on spec v1.0, raw LLM output dated 2026-05-29, and verification table with 8 ratios across 5 categories.*
