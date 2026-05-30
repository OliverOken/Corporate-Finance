# Stage 4 review — 2026-05-30

Reviewing the Stage 4 spec at `docs/specs/2026-05-29-nguyen-Lunit-spec.md`

## Section coverage

| Section | Present | Word count |
|---|---|---|
| 1. Scope & Objective | ✓ | 155 |
| 2. Model Architecture | ✓ | 255 |
| 3. Data Inputs | ✓ | 541 |
| 4. Named Range Conventions | ✓ | 204 |
| 5. Derived Inputs | ✓ | 181 |
| 6. Ratio Definitions & Formulas | ✓ | 647 |
| 7. Validation Rules | ✓ | 239 |
| 8. Analysis Requirements (Part B) | ✓ | 508 |
| 9. Du Pont Decomposition (Part B) | ✓ | 317 |
| 10. Strategic Recommendations (Part B) | ✓ | 289 |
| 11. Output Format (Part B) | ✓ | 402 |

## Observations

- Spec length: **3863 words** (brief targets 3–5 pages, ~1,500–2,500 words).
- Named-range notation usage: **393 hit(s)** across `BAL_*`, `INC_*`, `CASH_*`, `RATIO_*`, `startYear_*`, `currentYear_*`, `avg_*`.
- Ratio categories detected in Section 6: **performance, profitability, efficiency, leverage, liquidity, du pont** (6/6).
- Ratio table rows in Section 6: **29**.
- Prompt log: **not detected** in the submission.

### Kindly-worded suggestions for improvement

**Stage 4 rubric notes**

- **Prompt log not found.** Add a `deliverables/prompt-log.md` entry for each meaningful spec-drafting session — at minimum: intent, exact prompt(s) submitted, LLM used, and a note on what changed between rounds. The prompt log is half of the "spec craft" rubric line.
- **No visible HIL iteration evidence.** The brief asks for one of: (a) a 150–250 word before/after note in the prompt log describing a gap you found in the LLM's first draft and what you changed, (b) a clearly-labeled round-2 prompt that responded to a specific round-1 gap, or (c) an annotated diff at `analysis/validation/YYYY-MM-DD-{lastname}-{company}-stage4-iteration.md`. Self-assessment of the final draft is not the same — the iteration must show *the gap you caught* and *what you changed*.
- The prompt log should live at `deliverables/prompt-log.md` in your repo. The file accumulates across stages — append your Stage 4 session to it rather than creating a separate file per stage.

**Looking ahead to Stage 5**

- **Stage 5 — LLM analysis + manual verification.** Run your Stage 4 spec through the LLM of your choice, then verify at least five of its ratio outputs against the workbook by hand. The polish rubric grades how cleanly the prior four stages tie together as a single deliverable, so revisit your earlier files with fresh eyes.


*This review is feedback-only — no scores included.* Score numbers live in the internal grade report and the instructor's email; this file is intended for review against your repo state.
