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

## Usage

Start your agent **inside your NSF project directory** — the skill treats the
current working directory as the active project. Then it's three steps.

### 1. Create the project context file

Ask the skill to start a report for your reporting period:

```
start #nsf-annual-report for 2025-2026
```

The skill copies `references/project-context-template.md` into your project as
`nsf-report-context.md`, pre-filled with the reporting period. This file is the
durable, reusable source of truth for the project — it lives in your project
folder, not in this repo.

### 2. Fill out `nsf-report-context.md`

Open the new `nsf-report-context.md` and fill in your project's variables and
this period's facts: award number, title, PI/team, approved goals, people
supported, activities, results, products, publications, dissemination, and next
steps. Rough bullets are fine, and `none` / `not applicable` / `unknown` are
valid answers.

### 3. Generate the report

Ask the skill to draft the report:

```
create report using #nsf-annual-report
```

The skill reads your filled-in `nsf-report-context.md`, asks targeted follow-up
questions for anything still missing (rather than inventing facts), and writes a
paste-ready draft into your folder — mindful of Research.gov's field limits and
free of `[TODO]` placeholders:

```
nsf_report_2025_2026.md
├── Accomplishments
│   ├── 1. Major goals of the project
│   ├── 2. What was accomplished (Activities / Objectives / Results / Outcomes)
│   ├── 3. Training and professional development
│   ├── 4. Dissemination to communities of interest
│   └── 5. Plans for the next reporting period
└── Impact (principal discipline, other disciplines, human resources, …)
```

Review the markdown, then paste each section into Research.gov. Because the facts
live in `nsf-report-context.md`, next year you only update that file and re-run
step 3.

### Other things you can ask

- "Update my Research.gov accomplishments section for this reporting period."
- "Turn these notes into NSF annual report responses."
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
