# NSF Annual Report Skill

An agent skill that drafts concise, plain-language but technically rich **NSF
Research.gov Project Report** responses from a proposal folder and a set of
reusable report templates. It interviews you for the facts it needs, stores
durable project variables in a per-project context file, and produces
paste-ready Accomplishments, Impact, products, training, dissemination, and
next-period text — without inventing accomplishments, dates, or publications.

The skill logic is host-agnostic. The same instructions work under Claude Code
(via `SKILL.md`) and Codex (via `agents/openai.yaml`).

## What's in this repo

| Path | Purpose |
| --- | --- |
| `SKILL.md` | The skill definition and workflow. Claude Code reads this. |
| `agents/openai.yaml` | Codex launcher (display name + default prompt). |
| `references/project-context-template.md` | Template for a project's durable `nsf-report-context.md`. |
| `references/researchgov-accomplishments-template.md` | Research.gov Accomplishments prompts, field limits, response structure. |
| `references/researchgov-impact-questions.md` | Research.gov Impact page prompts and writing guidance. |
| `references/report-intake-questionnaire.md` | The reusable question set for gathering report facts before drafting. |

## Install as a skill

### Claude Code

Skills are discovered from a `skills/` directory. Place this repo (or a symlink
to it) as a folder whose name matches the skill's `name` (`nsf-annual-report`):

```bash
# Personal skill (available in every project):
ln -s "$(pwd)" ~/.claude/skills/nsf-annual-report

# — or — project skill (available only in one repo):
ln -s "$(pwd)" /path/to/your/project/.claude/skills/nsf-annual-report
```

Start a new session and the skill appears as `nsf-annual-report`. Claude invokes
it automatically when a request matches its description, or you can ask for it by
name.

> A symlink keeps the installed skill in sync with this repo as you edit it. Use
> `cp -R` instead if you want a fixed copy.

### Codex

Install per your Codex agent-skills setup, then launch it with the invocation in
`agents/openai.yaml` (default prompt uses `$nsf-annual-report`).

### Without installing

You don't have to install it at all. From a session with this repo available,
just point the agent at `SKILL.md` and ask it to follow the workflow against your
proposal folder.

## How to use it

1. **Point it at a proposal folder.** By default the skill treats the current
   working directory as the active project.
   > "Use this folder to draft the annual NSF report."
2. **Set up project context (first run).** If no `nsf-report-context.md` exists,
   the skill creates one from `references/project-context-template.md` and fills
   it with your award number, reporting period, title, team, approved goals, and
   writing preferences. This file is the durable, reusable source of truth — it
   lives in your proposal folder, not in this repo.
3. **Answer the intake questions.** The skill asks a single organized
   questionnaire for the current period's facts (people supported, activities,
   results, products, publications, presentations, outreach, deviations, next
   steps). "None" / "not applicable" / "unknown" are valid answers.
4. **Review the draft.** Output is a markdown draft in your proposal folder
   (e.g. `nsf_report_2025_2026.md`) with clean, field-limit-aware Research.gov
   text and no leftover placeholders.

### Example requests

- "Update my Research.gov accomplishments section for this reporting period."
- "Turn these notes into NSF annual report responses."
- "Create a progress log for the next annual report."
- "Revise the training, dissemination, and next-year plan sections."

## Design notes

- **Project facts live with the project.** Reusable variables and annual facts
  belong in each proposal folder's `nsf-report-context.md`, never hardcoded into
  the skill.
- **No invented facts.** Missing or uncertain accomplishments, dates,
  publications, trainee names, or events become questions for you rather than
  guesses.
- **Simple language, precise terms.** Sentence structure is simplified;
  technical terms that are the accurate object of the work are preserved (and
  briefly explained in plain language when useful).
