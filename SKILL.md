---
name: nsf-annual-report
description: Interview the user and create concise, simple-language but technically rich NSF Research.gov Project Report drafts from a proposal folder and reusable report templates. Use when asked to draft, update, revise, organize, or prepare NSF annual report responses, Research.gov Accomplishments responses, Impact page responses, annual progress logs, project outcomes, training/professional development, dissemination, or next-period plans for an NSF award or proposal folder.
---

# NSF Annual Report

## Overview

Use this skill to help prepare annual NSF Research.gov report responses for a specific award or proposal. Treat the current working directory as the active project folder unless the user gives another folder.

Keep the skill generic. Store project-specific variables and annual-report facts in `nsf-report-context.md` in the active proposal folder, not in the skill files.

Always read `references/project-context-template.md` when creating or updating a project's `nsf-report-context.md` file.

Always read the active proposal folder's `nsf-report-context.md` before drafting or revising report content. If it does not exist, create it from `references/project-context-template.md` or ask the user for the missing variables before drafting.

Always read `references/researchgov-accomplishments-template.md` before drafting or revising report content. It contains reusable Research.gov prompts, field limits, and generic response structure.

Always read `references/researchgov-impact-questions.md` before drafting or revising Impact page responses. It contains the Research.gov Impact prompts and writing guidance.

Always read `references/report-intake-questionnaire.md` before asking the user for information. It contains the reusable question set for gathering all annual-report facts before drafting.

## Workflow

1. Identify the active proposal/report folder.
   - Use the current working directory by default.
   - Inspect top-level files and likely folders such as `Submitted Documents`, `Annual Reports`, `Reports`, `Research.gov`, `Products`, `Publications`, and `REU Supplement`.
   - Prefer existing proposal documents, prior report drafts, annual logs, publications, notes, and user-supplied updates over generic language.
   - Look for `nsf-report-context.md` in the active folder. Treat this as the project's durable source of variables and annual facts.
   - If `nsf-report-context.md` is absent, create one from `references/project-context-template.md` when the user wants reusable project setup.

2. Build a project context brief before writing.
   - Start with variables in `nsf-report-context.md`: award number, reporting period, project title, PI/team, approved project goals, major research threads, broader impacts, planned evaluation, and writing preferences.
   - Extract annual facts: people supported, activities completed, results, products, publications, software/data, presentations, outreach, mentoring, deviations, and next-period plans.
   - Use local proposal files and prior drafts to fill gaps, but let explicit values in `nsf-report-context.md` override inferred facts.
   - Treat missing or uncertain facts as questions for the user; do not invent accomplishments, dates, publications, trainee names, or dissemination events.

3. Interview the user before drafting.
   - Ask the consolidated intake questions needed to complete the report without `[TODO]`, `[VERIFY]`, or `[EDIT]` markers.
   - Prefer one organized questionnaire with short section headings over many scattered interruptions.
   - If the folder already answers a question, show the inferred answer and ask the user to confirm or correct it.
   - If the user answers partially, ask targeted follow-up questions until each report section can be drafted cleanly.
   - Accept "none", "not applicable", or "unknown" as explicit answers; reflect them appropriately in the final text.
   - When the user supplies durable project facts or annual facts, add or update them in `nsf-report-context.md` unless the user asks not to.
   - Only create a placeholder draft when the user explicitly asks for a draft with placeholders.

4. Draft or update the report using the template sections.
   - Keep stable project-level language consistent across years unless the user indicates agency-approved changes.
   - For annual progress sections, include only work that occurred during the reporting period.
   - Connect accomplishments to NSF intellectual merit and broader impacts when relevant.
   - Preserve Research.gov field limits by drafting concise responses and noting when a section may need trimming.
   - Make each answer as short as possible while still answering the prompt. A sentence, two short sentences, or a numbered list is acceptable.
   - Avoid overlap between answers. Put a fact in the one field where it fits best, then do not repeat it unless Research.gov specifically requires it.
   - Use simple language that remains technically rich. Simplify sentence structure, not the technical meaning.
   - Preserve central technical terms when they are the accurate object of the work, such as hybrid limit cycles, invariant sets, reachability analysis, contraction, trajectory optimization, robust motion synthesis, and contact-rich CPS.
   - Briefly explain specialized terms in plain language when useful, for example "hybrid limit cycles, meaning periodic behaviors with continuous motion and discrete contact events."
   - Do not replace precise terms with broader but inaccurate phrases. For example, do not replace "hybrid limit cycles" with "periodic robot motions" when the hybrid-system structure matters.
   - Avoid dense jargon, acronyms without expansion, and proposal-style hype. Use concrete nouns, active verbs, and technically accurate explanations of why the work matters.
   - Do not hardcode reusable project variables in the skill. Use `nsf-report-context.md` values instead.
   - Do not leave bracketed internal notes in a Research.gov-ready draft. If an answer remains unavailable, pause and ask the user rather than filling the section with placeholders.

5. Prepare user-review output.
   - Create or update a markdown draft in the active folder unless the user asks for another format.
   - Use a filename that includes the reporting year when known, such as `nsf_report_2025_2026.md`.
   - Include an internal source/evidence note only if useful, but keep the Research.gov response text clean.
   - Before final Research.gov-ready text, remove internal comments and bracketed notes.

## Evidence Standards

- Use proposal PDFs and submitted documents for approved goals and stable framing.
- Use `nsf-report-context.md` for durable project variables and annual-report facts.
- Use current-period notes, user updates, publication lists, repositories, student records, and calendars only when available or explicitly provided.
- If documents are PDFs, spreadsheets, or Word files, use the appropriate document/spreadsheet/PDF tooling to inspect them rather than guessing from filenames.
- When the user asks for a final paste-ready answer, provide clean section text and no unresolved placeholders. If facts are still missing, ask for them before finalizing.

## Common Requests

- "Use this folder to draft the annual NSF report."
- "Update my Research.gov accomplishments section for this reporting period."
- "Turn these notes into NSF annual report responses."
- "Create a progress log for the next annual report."
- "Revise the training, dissemination, and next-year plan sections."
