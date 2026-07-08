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

This skill runs in two modes, chosen by what the user asks for:

- **Setup mode** — triggered by requests like "start nsf-annual-report for 2025-2026". Create the project's `nsf-report-context.md` from the template and hand it back to the user to fill in. Do not run the full intake interview here.
- **Draft mode** — triggered by requests like "create report using nsf-annual-report". Read the filled-in `nsf-report-context.md`, offer to interview for any gaps, then draft the report.

If the user's intent is ambiguous, or they ask to draft but no `nsf-report-context.md` exists yet, start with Setup mode and tell them what you did.

### Setup mode: create the project context file

1. Identify the active proposal/report folder.
   - Use the current working directory by default.
   - Inspect top-level files and likely folders such as `Submitted Documents`, `Annual Reports`, `Reports`, `Research.gov`, `Products`, `Publications`, and `REU Supplement`.
   - Look for an existing `nsf-report-context.md` in the active folder.

2. Create `nsf-report-context.md` from `references/project-context-template.md`.
   - If the file already exists, do not overwrite it. Tell the user it exists and ask whether to update specific fields or move on to drafting.
   - If it is absent, copy the template into the active folder as `nsf-report-context.md`.
   - Pre-fill the `reporting_period` from the user's request (for example, "2025-2026"), and pre-fill any variables you can confidently read from local proposal files (award number, title, PI/team). Leave everything else as the template's blank fields.

3. Hand the file back to the user.
   - Tell the user the file is ready and where it is, and ask them to fill in their project variables and this period's facts.
   - Do not run the full intake questionnaire in Setup mode. The goal is to give the user the file to complete.
   - Offer to help fill specific sections if they would rather answer questions than edit the file directly.

### Draft mode: generate the report

1. Read `nsf-report-context.md` in the active folder.
   - If it is missing, switch to Setup mode first, then return here.
   - Treat this file as the project's durable source of variables and annual facts.

2. Build a project context brief before writing.
   - Start with variables in `nsf-report-context.md`: award number, reporting period, project title, PI/team, approved project goals, major research threads, broader impacts, planned evaluation, and writing preferences.
   - Extract annual facts: people supported, activities completed, results, products, publications, software/data, presentations, outreach, mentoring, deviations, and next-period plans.
   - Use local proposal files and prior drafts to fill gaps, but let explicit values in `nsf-report-context.md` override inferred facts.
   - Treat missing or uncertain facts as questions for the user; do not invent accomplishments, dates, publications, trainee names, or dissemination events.

3. Offer to interview the user for gaps before drafting.
   - Identify which report sections cannot yet be drafted cleanly (without `[TODO]`, `[VERIFY]`, or `[EDIT]` markers) from `nsf-report-context.md` and local evidence.
   - If there are gaps, offer to ask the user for the missing facts. Prefer one organized questionnaire with short section headings over many scattered interruptions.
   - If the folder or context file already answers a question, show the inferred answer and ask the user to confirm or correct it.
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

- "Start nsf-annual-report for 2025-2026." (Setup mode: create `nsf-report-context.md`.)
- "Create report using nsf-annual-report." (Draft mode: draft from the filled-in context.)
- "Use this folder to draft the annual NSF report."
- "Update my Research.gov accomplishments section for this reporting period."
- "Turn these notes into NSF annual report responses."
- "Create a progress log for the next annual report."
- "Revise the training, dissemination, and next-year plan sections."
