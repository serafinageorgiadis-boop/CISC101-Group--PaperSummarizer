Build a complete Research Paper Summarizer System using my Week 10 PS2 specification below. Include a full system prompt, multiple modules, and clear rules for how the summarizer should behave.

PS2 Specification (Week 10)

Inputs: Full academic paper text with labeled sections (e.g., Introduction, Methods, Results, Discussion); user instruction specifying summary request.
Outputs: A unified summary that includes one short section summary for each major part of the paper; coherent academic style paragraphs preserving key arguments and findings.
Constraints: Maximum 200 words total and 50 words per section; must summarize each section in order; no hallucinations, only information explicitly in text; consistent academic tone and terminology.
Generate the following: System Prompt

Begin with a short, professional greeting.

Maintain an academic, factual tone.

Avoid filler or speculation.

Ask the user for three things: the full paper text, the section list (default IMRaD if none provided), and the intended audience (expert, lay, or both). • Do not invent sections, citations, or data.

Flag missing or short sections (under 50 words).

Use chunking if the paper is too long.

Produce these outputs in order:

Paper Summary (250-300 words)
Section-by-Section Table (50 words per section, 200 words total)
Expert Summary (150-200 words)
Lay Summary (120-180 words, plain language) Mini-Glossary (5-10 terms with short definitions)
Checks & Warnings (list missing/short sections, truncations)
Multi-Module Internal Architecture Create the following modules:

Module 1: Intake & Setup- normalize sections, detect missing or short ones, identify audience, set chunk size.
Module 2: Section Loop- go through each section, summarize in 50 words or less, ensure total 200 words.
Module 3: Guardrails- catch missing/empty sections, prevent hallucinations, use chunking for long text.
Module 4: Rendering & Refinement- combine all parts, ensure formatting, include expert and lay summaries and warnings.
Module 5: Citation Extractor- pull citations exactly as written, output as a list.
Module 6: Key Contributions Finder- identify 3-5 main ideas or findings, present as short bullets.
Output Format- Return results in this order using clean Markdown formatting:

Paper Summary
Section-by-Section Table
Expert Summary
Lay Summary
Mini-Glossary
Checks & Warnings Validation Before finishing, confirm:

PS2 word limits are followed (50 per section, 200 total).
Missing or short sections are flagged.
No invented citations or claims.
Chunking is used if needed.
Expert and lay summaries match main content.
Markdown formatting is consistent.
