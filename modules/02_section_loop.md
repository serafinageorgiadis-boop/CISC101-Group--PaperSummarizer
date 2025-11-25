# Module 2: Section Loop

> **Change Log (2025-11-25)**  
> - Added `summary_level` variable with two modes: `"short"` and `"detailed"`.  
> - Implemented conditional behavior: compact 1–2 sentence summary vs. paragraph + 3–5 bullet points.  
> - Kept PS2 word-limit table logic (≤50 words per section for the *Section-by-Section Table*), while allowing richer text for other outputs.

## Purpose
Iterate through sections in the provided order and produce section-level summaries that can render both a compact table view and richer narrative outputs while respecting PS2 constraints.

## Inputs
- `sections`: ordered list of section objects (name, text)
- `summary_level`: `"short"` | `"detailed"` (default `"short"` if not provided)
- `table_word_budget_per_section`: `50`
- `table_total_budget`: `200`

## Core Loop (pseudologic for the LLM)
For each `section` in `sections` **in order**:
1. **Guard: empty/short**  
   - If text is missing or < 50 words, record a flag (Module 3 handles warnings).
2. **Summarization mode**
   - If `summary_level == "short"`:  
     - Generate a **compact** 1–2 sentence summary of the section’s core aim, method/evidence, and takeaway.  
     - This compact version is also the candidate text for the **Section-by-Section Table**.  
     - Enforce **≤ 50 words** for the table entry.
   - If `summary_level == "detailed"`:  
     - Generate a **short paragraph** (3–5 sentences) capturing aims, methods/data, key results, and implications.  
     - Additionally produce a **bullet list (3–5 bullets)** of key points (metrics, definitions, datasets, limitations).  
     - For the **Section-by-Section Table**, still produce a **separate compact entry** (≤ 50 words) derived from the detailed paragraph.
3. **Accumulate table budget**  
   - Track cumulative table word count; ensure **≤ 200 words total**.
4. **Emit per-section payload**
   - `compact_summary` (≤50 words, for the table)  
   - `narrative_summary` (1–2 sentences if short; paragraph if detailed)  
   - `bullet_points` (only if detailed; 3–5 concise bullets)

## Outputs
- **Table entries**: one compact entry per section, ≤50 words; table total ≤200 words.
- **Narrative bundle**: per-section narrative (short or detailed) + optional bullets (detailed mode only).

## Notes
- Never invent content; all claims must be text-bounded (Module 3 enforces).
- Never reorder sections or add missing sections.
