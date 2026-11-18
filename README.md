# Omnia

**A station for your AI agents.** Several agents, each on its own task, all in view.

Omnia is a desktop app with an infinite canvas. Each AI agent runs in its own terminal on the canvas,
next to the browser, notes, diagrams and boards it works with. You see every agent at once and decide
what each one can reach. The AI subscription you already have is enough.

Website: **https://omnia.lketerson.com** · Manual: [English](https://omnia.lketerson.com/manual/) ·
[Español](https://omnia.lketerson.com/es/manual/) · [Português](https://omnia.lketerson.com/pt-br/manual/)

> This repository holds only the installers and the release notes. The source code is not public.

---

## Contents

- [What Omnia does](#what-omnia-does)
- [What fits on the station](#what-fits-on-the-station)
- [Supported agents](#supported-agents)
- [Links and the `omnia` CLI](#links-and-the-omnia-cli)
- [Security](#security)
- [Platforms](#platforms)
- [Install](#install)
- [Getting started](#getting-started)
- [Updates](#updates)
- [Your data](#your-data)
- [Verify a download](#verify-a-download)
- [Reporting a problem](#reporting-a-problem)

## What Omnia does

| Without Omnia                                   | With Omnia                                            |
| ----------------------------------------------- | ----------------------------------------------------- |
| One agent per terminal tab, out of sight        | Every agent on one canvas, each on its own task       |
| Copying context between windows by hand         | Agents talk to each other through links you draw      |
| The agent opens its own hidden browser          | The agent drives a browser you can watch: the Portal  |
| Passwords pasted into the chat                  | Logins filled from the Vault; the agent never sees them |
| Plans and notes lost in the scrollback          | Plans become records, diagrams and kanban cards       |

**One subscription, a whole crew.** An agent from your Claude, Codex or Gemini subscription can call
other agents to work in parallel. Lighter models take the repetitive work (tests, builds, searches),
and the stronger one keeps the plan.

## What fits on the station

- **Terminals and crew.** Each terminal runs an agent or a plain shell. One agent can be the
  commander and hand out work to the rest of the crew.
- **Portal.** A browser the agent drives: it reads the page, clicks, fills forms and takes
  screenshots while you watch.
- **Records.** Markdown notes and Mermaid diagrams that agents write and you read on the canvas.
- **Flowchart.** A diagram you and the agents edit together.
- **Kanban.** A task board the agents pick cards from and move as they work. It imports issues from
  GitHub.
- **Viewscreen** (Windows). Any app on your PC, inside the station, where an agent can operate it.
- **Decks.** One deck per project, each with its own branch and Git worktree, and a Merge when the
  work is done.
- **Android.** Drive a phone or an emulator over `adb`: tap, type, read the screen.
- **Phone access.** Follow the station from your phone after pairing with a QR code.
- **Log.** A shared logbook with a timeline of what each agent did.
- **And also:** Launch buttons, a pull-request panel (through `gh`), a file editor, saved prompts,
  scheduled missions, token telemetry per agent, and a station that comes back as you left it when
  you reopen the app.

## Supported agents

Claude Code, Codex, Gemini CLI, OpenCode, Kimi and Copilot. Omnia runs the CLI you already have
installed and logged in; it does not resell or proxy any model.

## Links and the `omnia` CLI

An agent only talks to the nodes linked to it. Drag a link from a terminal to a portal, a record, a
kanban or another terminal, and that agent can use it. No link, no access.

Inside the station, agents use the `omnia` command-line tool, which ships with the app:

```sh
omnia peers                      # who is linked to me
omnia ask Reviewer "is the diff ready?"
omnia portal goto localhost:3000
omnia frota add - "run the test suite" --modelo leve
```

To teach your agent these commands, send `/omnia` in its chat, or install the skill once:

```sh
omnia skill install claude   # or codex, gemini
```

## Security

- **One token per terminal.** Each agent gets its own credential to the station; one terminal cannot
  act as another.
- **Links are permissions.** An agent reaches only what you linked to it.
- **Locked Vault.** Passwords stay encrypted. The key lives only in memory, and every use asks for
  your approval. The agent fills a login without ever seeing the secret.
- **Explicit approvals.** Sensitive actions wait for you to approve them on screen.
- **Docker sandbox.** Run an agent inside a container when you do not want it touching your machine.

## Platforms

| System  | File                         | Notes                                        |
| ------- | ---------------------------- | -------------------------------------------- |
| Windows | `omnia-<version>-setup.exe`  | Installer. Includes the Viewscreen.          |
| Linux   | `omnia-<version>.AppImage`   | Portable. Make it executable and run it.     |

macOS is not available yet.

## Install

1. Open the [latest release](https://github.com/lketerson/omnia-releases/releases/latest).
2. Download the file for your system (see [Platforms](#platforms)).
3. Optional: [verify the download](#verify-a-download).
4. **Windows:** run the installer. **Linux:** `chmod +x omnia-<version>.AppImage` and run it.

You also need at least one agent CLI installed and logged in (for example Claude Code, Codex or
Gemini CLI).

## Getting started

1. Open Omnia. The canvas is empty.
2. Double-click the canvas to create a terminal. Use **+ Create** for other nodes: portal, record,
   kanban, flowchart.
3. Start your agent in the terminal and send `/omnia`.
4. Draw links from the agent to the nodes it should use.
5. Ask for the work. Watch it happen on the canvas.

The [manual](https://omnia.lketerson.com/manual/) covers each part in detail: the station, decks,
terminals and crew, links and the CLI, portal and Android, records, flowchart, kanban, files,
viewscreen, panels, vault, phone access, sandbox, settings, data and updates, and keyboard shortcuts.

## Updates

The installed app checks this repository for a new version when it opens and every 4 hours. The
update downloads in the background, then Omnia asks whether to restart now or install when you quit.

On Linux, only the AppImage updates itself.

Release notes for each version are on the [Releases](https://github.com/lketerson/omnia-releases/releases)
page.

## Your data

Everything stays on your machine, in the app's data folder:

- Windows: `%APPDATA%\omnia`
- Linux: `~/.config/omnia`

| Path             | Contents                                         |
| ---------------- | ------------------------------------------------ |
| `workspace.json` | The station, with a backup in `workspace.json.bak` |
| `rotinas.json`   | Missions and their run history                   |
| `prompts.json`   | Saved prompts                                    |
| `sessions/`      | History and folder of each terminal              |
| `logs/`          | `omnia.log` and up to 5 older files of 1 MB each |
| `diagnostics/`   | Diagnostic bundles                               |

The log masks API keys, tokens, passwords and the name of your user folder before writing.

## Verify a download

Each release ships a `SHA256SUMS.txt` with the hash of every file.

**Linux**, in the folder with the downloaded files:

```sh
sha256sum -c --ignore-missing SHA256SUMS.txt
```

**Windows** (PowerShell):

```powershell
Get-FileHash .\omnia-<version>-setup.exe
```

Compare the hash with the matching line in `SHA256SUMS.txt`.

## Reporting a problem

Attach a diagnostic bundle (Settings in the app). It holds the versions, the system, a count of nodes
per kind and the end of the logs, with no titles, paths or secrets.

Contact: **contact@omniastation.com.br**
