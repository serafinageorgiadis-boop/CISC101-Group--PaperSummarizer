# Module 3: Guardrails

> **Change Log (2025-11-25)**  
> - Added `evidence_mode = "strict"` option that forces text-bounded extraction only.  
> - Added standardized **Section Warning Messages** for missing/empty or <50-word sections.

## Purpose
Apply safety, evidence, and validation rules to prevent hallucinations, manage incomplete inputs, and keep outputs faithful to source text.

## Inputs
- `section.text`, `section.name`
- `evidence_mode`: `"strict"` | `"standard"` (default `"standard"`)
- thresholds: `min_section_words = 50`

## Evidence Modes
- **standard**: normal summarization with the usual “source-only” rule.  
- **strict**:  
  - Only include claims, equations, numbers, and results **verifiably present** in the provided text.  
  - If required information is missing, output:  
    - **“The source text does not provide enough detail to summarize this section in strict evidence mode.”**

## Section Warning Messages (standardized)
Trigger these messages early so downstream rendering can display them clearly:

- **Missing/empty section** →  
  - `warning_missing = "Section skipped: no usable text was provided."`

- **Too short (< 50 words)** →  
  - `warning_short = "Section very short: summary may be incomplete."`

## Validation Hooks
Run these checks during/after Module 2 processing:

1. **Text-bounded claims**  
   - Reject/strip any statement not directly supported by `section.text` when `evidence_mode == "strict"`.
2. **Completeness**  
   - If `section.text` is missing/empty: attach `warning_missing` and return an empty compact summary for the table.
3. **Short sections**  
   - If `len(section.text) < 50`: attach `warning_short` and allow a minimal compact summary (still ≤50 words).
4. **No fabricated citations**  
   - Disallow invented references; citations in outputs must match the paper (Module 5 handles extraction).
