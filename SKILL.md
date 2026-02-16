---
name: granola
description: Search and retrieve meeting notes, summaries, and transcripts from Granola.
version: 1.1.0
metadata:
  openclaw:
    emoji: "🥣"
    requires:
      bins:
        - granola
      env: []
---

# Granola (Meeting Notes)

Use the `granola` CLI from `https://github.com/magarcia/granola-cli` to access the user's Granola meeting notes.

## Setup

First-time setup:

```bash
npm install -g github:magarcia/granola-cli
granola auth login
granola auth status
```

Remote server (headless) auth:

- `granola auth login` does not run browser OAuth; it imports tokens from Granola desktop's `supabase.json`
- On Linux servers, place that file at `~/.config/granola/supabase.json` before running `granola auth login`
- If the server has no system keyring, use `TS_KEYRING_BACKEND=file` so credentials are stored in encrypted local files
- Verify with `granola auth status`

## Commands

### Find meetings
```bash
granola meeting list --search "partner standup" --since "last week"
```
Use filters like `--attendee`, `--date`, `--since`, `--until`, `--workspace`, and `--folder` to narrow results.

### View meeting metadata
```bash
granola meeting view <meeting-id>
```
Shows title, date, attendees, and links to follow-up commands.

### View AI summary and action items
```bash
granola meeting enhanced <meeting-id>
```
Best command for decisions, takeaways, and action items.

### View manual notes
```bash
granola meeting notes <meeting-id>
```
Shows user-authored notes for the meeting.

### Get transcript
```bash
granola meeting transcript <meeting-id>
```
Returns the verbatim transcript. Add `--timestamps` if timing context matters.

### Export structured output
```bash
granola meeting export <meeting-id> --format json
```
Use for machine-readable output when downstream tools need full meeting data.

## When to use

- User asks about what was discussed, decided, or action items from meetings
- User asks about follow-ups, todos, or commitments
- User references "meeting notes", "Granola", or "what did we talk about"
- Preparing for a meeting by reviewing past meetings with the same people

## When NOT to use

- Calendar scheduling or upcoming events (use `gog` instead)
- Creating or modifying calendar invites

## Tips

- Start with `meeting list` to find the right meeting ID, then use `enhanced`, `notes`, or `transcript`
- Use `meeting enhanced` for summaries/action items and `meeting notes` for user-written notes
- Use `meeting transcript` only when exact wording matters
- Use `--output json` (or `-o json`) for scripting where supported
- Use `meeting export --format json` for the most complete structured payload

## Auth

Credentials are stored in your system keychain by `granola-cli`. If auth fails or credentials become invalid, run `granola auth login` again.
