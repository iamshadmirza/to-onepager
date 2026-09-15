# to-onepager

A Cursor skill that turns a research or decision conversation into a one-pager that is easy to read and follow, then publishes it where you choose: **local Markdown**, **Google Docs**, or **Confluence**.

**Author:** [Mohammad Shad Mirza](https://github.com/iamshadmirza) (`iamshadmirza`)

```bash
npx skills add iamshadmirza/to-onepager -g -a cursor
```

Use the page as a **meeting pre-read**: share ahead or read in silence at the start, then discuss. The page carries the context so the meeting does not.

## What it does

`/to-onepager` mines a transcript, routes to a page type, drafts a grounded one-pager, grounds it, and publishes to your configured destination.

| Page type | Use when |
| --- | --- |
| `research-finding` | Empirical question: what is true? |
| `proposal` | Decision bet: Problem / What / Why / How |

Shared on every page: Status, Owner, Reviewer, Page type, cold-reader Answer (Finding = TLDR), Review. Recommendation lists follow-ups only when the session discussed them; closed research may say None.

## When to use it

* `/to-onepager` with a transcript path or paste
* `/to-onepager` with no args (current conversation)
* `/to-onepager setup` to set or change publish destination
* Before a decision meeting, when a short written pre-read beats slides

## Install

Uses the open [skills](https://github.com/vercel-labs/skills) CLI (same as most skills on [skills.sh](https://skills.sh)).

### Cursor (recommended)

```bash
npx skills add iamshadmirza/to-onepager -g -a cursor
```

List without installing:

```bash
npx skills add iamshadmirza/to-onepager --list
```

The CLI installs the whole skill folder (`SKILL.md`, `templates/`, `publish.md`, …). Global Cursor installs typically land under `~/.agents/skills/to-onepager` (canonical copy, registered for Cursor). Reload Cursor / skills if `/to-onepager` does not appear yet.

### Other agents

```bash
npx skills add iamshadmirza/to-onepager -g -a claude-code
# or omit -a and pick agents interactively
```

### Alternatives

* Ask Cursor: install `https://github.com/iamshadmirza/to-onepager` as a skill (whole folder).
* Clone: `git clone https://github.com/iamshadmirza/to-onepager.git ~/.cursor/skills/to-onepager`
* Project skill: copy into `.cursor/skills/to-onepager/` or `.agents/skills/to-onepager/`. Keep `config.md` out of git.

## First-run setup

On first use (or `setup`), the skill asks for destination and paths, then writes `config.md` beside `SKILL.md` in the install directory. That file is local to your install.

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
