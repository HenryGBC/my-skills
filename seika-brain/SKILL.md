---
name: seika-brain
description: Query and update Seika AI's CRM/knowledge system. Use when you need client context, project info, billing data, or to log calls, decisions, and pending items.
argument-hint: [command] [args...]
allowed-tools: Bash, Read
---

# Seika Brain — CRM & Knowledge System

You have access to `seika-brain`, Seika AI's internal CRM CLI. Use it to get client context, update records, and track operations.

## Quick Reference

### Get full client context (most useful command)
```bash
seika-brain brain <company-slug>
```
This returns EVERYTHING about a client: company info, contacts, subscriptions, billing, projects, repos, pending items, recent calls, decisions, context notes, and open pipeline.

For machine-readable output:
```bash
seika-brain --json brain <company-slug>
```

### Dashboard — global executive summary
```bash
seika-brain dashboard
```

### Search across all entities
```bash
seika-brain search "<query>"
```

## All Commands

| Command | Subcommands | Description |
|---------|-------------|-------------|
| `company` | add, list, show, edit, remove | Manage companies |
| `contact` | add, list, show, edit, remove | Manage contacts |
| `pipeline` | add, list, show, edit, advance, lose | Sales opportunities |
| `proposal` | add, list, show, edit, send, accept, reject | Proposals |
| `sub` | add, list, show, edit, pause, cancel | Subscriptions |
| `billing` | add, list, show, pay, mrr | Billing & MRR |
| `project` | add, list, show, edit, complete | Projects |
| `repo` | add, list, show, edit, archive | Repositories |
| `decision` | add, list, show | Decision log |
| `call` | add, list, show | Call summaries |
| `pending` | add, list, show, edit, done, assign | Action items |
| `context` | add, list, show, edit, remove | Tribal knowledge |

## Common Patterns

### Before a client meeting
```bash
seika-brain brain <slug>
```

### After a client call
```bash
seika-brain call add <company-slug> \
  --title "Call title" \
  --seika-participants henry,jordano \
  --client-participants "Name1,Name2" \
  --summary "What was discussed" \
  --action-items "Item 1,Item 2"
```

### Log a decision
```bash
seika-brain decision add "Decision title" \
  --company <slug> \
  --project <project-slug> \
  --context "Why this decision was made" \
  --alternatives "Other options considered"
```

### Add a pending item
```bash
seika-brain pending add "Task title" \
  --company <slug> \
  --assignee henry \
  --priority high \
  --due 2026-04-15
```

### Add context note (tribal knowledge)
```bash
seika-brain context add <company-slug> \
  --category technical \
  --content "Important detail about this client"
```
Categories: `preference`, `technical`, `relationship`, `risk`, `insight`, `general`

### Check MRR
```bash
seika-brain billing mrr
```

## Output Formats

- Default: Rich formatted (for humans)
- `seika-brain --json <command>` — JSON output (for parsing)
- `seika-brain --plain <command>` — Plain text (pipe-friendly)

Always use `--json` when you need to parse the output programmatically.

## Team Members

Valid assignees/owners: `henry`, `jordano`, `neida`, `raymond`

## Identifiers

- Companies and projects use **slugs**: `due-legal`, `ai-suite-legal`
- Other entities use **hex IDs** (first 8 chars shown): `seika-brain pending done a1b2c3d4`
