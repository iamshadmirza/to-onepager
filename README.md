# to-onepager

A Cursor skill that turns a research or decision conversation into a one-pager and publishes it where you choose: **local Markdown**, **Google Docs**, or **Confluence**.

Use the page as a **meeting pre-read**: share ahead or read in silence at the start, then discuss. The page carries the context so the meeting does not.

## What it does

`/to-onepager` mines a transcript, routes to a page type, drafts a grounded one-pager, grounds it, and publishes to your configured destination.

| Page type | Use when |
| --- | --- |
| `research-finding` | Empirical question: what is true? |
| `proposal` | Decision bet: Problem / What / Why / How |

Shared on every page: Status, Owner, Reviewer, Page type, cold-reader Answer (Finding = TLDR), Review, near-term next steps.

## When to use it

* `/to-onepager` with a transcript path or paste
* `/to-onepager` with no args (current conversation)
* `/to-onepager setup` to set or change publish destination
* Before a decision meeting, when a short written pre-read beats slides

## Install (Cursor)

Install the **whole folder** (not only `SKILL.md`):

### Option 1: Ask Cursor

> Install https://github.com/iamshadmirza/to-onepager into `~/.cursor/skills/to-onepager/` (all files, including `templates/` and `publish.md`).

### Option 2: Clone

```bash
git clone https://github.com/iamshadmirza/to-onepager.git ~/.cursor/skills/to-onepager
```

### Option 3: Project skill

Copy the repo into `.cursor/skills/to-onepager/` in your project. Keep `config.md` out of git.

## First-run setup

On first use (or `setup`), the skill asks for destination and paths, then writes `config.md` beside `SKILL.md`. That file is local to your install.

See [config.example.md](./config.example.md).

## Repo layout

| Path | Role |
| --- | --- |
| `SKILL.md` | Steps: Setup → Mine → Route → Distill → Ground → Publish |
| `templates/research-finding.md` | Research spine (loaded after Route) |
| `templates/proposal.md` | Proposal spine (loaded after Route) |
| `publish.md` | Destination-specific publish steps |
| `config.example.md` | Shape of local `config.md` |
| `.gitignore` | Ignores local `config.md` |

## License

Use and adapt. No warranty.
