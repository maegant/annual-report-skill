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

## Install

This skill is plain markdown, so **any AI coding agent can run it** — the
workflow lives in `SKILL.md` and the reference files. What differs between agents
is only how they discover and launch it. Instructions for the two most common
hosts are below; a generic fallback for any other agent follows.

The repo is named to match the skill (`nsf-annual-report`), so in every case you
can clone it directly and the folder name is already correct.

### Claude Code

Claude Code discovers skills from a `skills/` directory, where each skill lives
in a folder whose name matches the skill's `name`. Clone this repo straight into
that directory.

**Personal skill** (available in every project):

```bash
git clone https://github.com/maegant/nsf-annual-report \
  ~/.claude/skills/nsf-annual-report
```

**Project skill** (available only in one repo):

```bash
git clone https://github.com/maegant/nsf-annual-report \
  /path/to/your/project/.claude/skills/nsf-annual-report
```

Start a new Claude Code session and the skill appears as `nsf-annual-report`.
Claude invokes it automatically when a request matches its description, or you
can ask for it by name.

> Prefer a symlink if you're editing the skill from a working copy elsewhere:
> `ln -s /path/to/your/clone ~/.claude/skills/nsf-annual-report`. A symlink keeps
> the installed skill in sync with that copy as you edit it.

### Codex

Codex discovers skills from `$CODEX_HOME/skills` (or `~/.codex/skills` if
`CODEX_HOME` is not set), where each skill is its own folder with a `SKILL.md` at
its top level. Clone this repo directly into that directory — its `SKILL.md` is
already at the top level, so the result is `.../skills/nsf-annual-report/SKILL.md`:

```bash
# If CODEX_HOME is set:
git clone https://github.com/maegant/nsf-annual-report \
  "$CODEX_HOME/skills/nsf-annual-report"

# Otherwise:
git clone https://github.com/maegant/nsf-annual-report \
  ~/.codex/skills/nsf-annual-report
```

The `agents/openai.yaml` launcher defines the display name and the default
prompt. Launch the skill with that invocation (default prompt uses
`$nsf-annual-report`), then point it at your proposal folder.

### Any other agent

You don't have to formally install it. From a session with this repo available,
point the agent at `SKILL.md` and ask it to follow the workflow against your
proposal folder. The agent reads `SKILL.md`, which pulls in the reference files
as needed.

### Updating

However you installed it, update later by pulling:

```bash
cd path/to/nsf-annual-report && git pull
```

## Example

Start your agent **inside your proposal/award folder** and ask for the report.
The skill treats the current working directory as the active project.

**First run — it sets up durable project context.** If no `nsf-report-context.md`
exists, the skill creates one from the template and interviews you for the facts
it can't find in the folder:

```
You:   Use this folder to draft my NSF annual report for this period.

Skill: I don't see an nsf-report-context.md here, so I'll create one from the
       template. First, a few durable facts (rough notes are fine):
        - Award number and project title?
        - Reporting period this report covers?
        - PI, co-PIs, and institutions?
        - Any agency-approved changes to goals, scope, or key personnel?

You:   Award #2043872, "Robust Motion Synthesis for Contact-Rich CPS".
       Period 07/2025–06/2026. PI Jane Doe, Georgia Tech. No approved changes.
```

**Then it runs one organized intake questionnaire** for the current period —
people supported, activities, results, products, publications, presentations,
outreach, deviations, and next steps. `none`, `not applicable`, and `unknown`
are all valid answers, and anything already answered by files in the folder is
shown to you for confirmation instead of re-asked.

**Finally it writes a paste-ready draft** into your folder — no invented facts,
no leftover `[TODO]` placeholders, and mindful of Research.gov's field limits:

```
Annual Reports/nsf_report_2025_2026.md
├── Accomplishments
│   ├── 1. Major goals of the project
│   ├── 2. What was accomplished (Activities / Objectives / Results / Outcomes)
│   ├── 3. Training and professional development
│   ├── 4. Dissemination to communities of interest
│   └── 5. Plans for the next reporting period
└── Impact (principal discipline, other disciplines, human resources, …)
```

You review the markdown, then paste each section into Research.gov. Durable
facts you supply are saved back into `nsf-report-context.md`, so next year's
report starts from what you already established.

### Other things you can ask

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
</content>
</invoke>
