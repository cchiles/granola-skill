# Granola Skill for OpenClaw 🥣

Search and query your [Granola](https://granola.ai) meeting notes, summaries, and transcripts directly from OpenClaw.

## What is this?

This is an [OpenClaw](https://openclaw.dev) skill that uses the community-maintained [granola-cli](https://github.com/magarcia/granola-cli) tool to access Granola meeting data.

## Install

```bash
npm install -g github:magarcia/granola-cli
```

Then authenticate:

```bash
granola auth login
granola auth status
```

Credentials are stored securely by `granola-cli` in the system keychain.

### Remote server auth (headless)

`granola auth login` imports credentials from Granola desktop's local token file (`supabase.json`); it does not perform browser OAuth.

For Linux servers:

```bash
mkdir -p ~/.config/granola
# copy supabase.json from a logged-in Granola desktop machine
granola auth login
granola auth status
```

If the host has no usable keyring service, set `TS_KEYRING_BACKEND=file` before `auth login` and runtime commands.

## Requirements

- Node.js 20+
- A Granola account with meeting notes

## Commands

| Command | Description |
|---------|-------------|
| `granola auth login` | Import credentials from Granola desktop app |
| `granola meeting list [filters]` | List/filter meetings |
| `granola meeting view <id>` | View meeting metadata and attendees |
| `granola meeting notes <id>` | View manual notes |
| `granola meeting enhanced <id>` | View AI summary, decisions, and action items |
| `granola meeting transcript <id>` | View verbatim transcript |
| `granola meeting export <id> --format json` | Export complete meeting payload |

## How it works

The skill expects the `granola` binary from `granola-cli` to be available. It then runs CLI commands to retrieve meeting data for summarization and question-answering workflows.

## Files

- `SKILL.md` — Skill definition (loaded by OpenClaw)
- `README.md` — This file
