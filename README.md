# shotfleet skills

shotfleet is a macOS command-line tool that captures your App Store and Google Play screenshots in every language
your app ships, from one English Maestro flow. It also checks that each screenshot is really in the right language,
and you can get it at [shotfleet.com](https://shotfleet.com).

This repo holds only the agent skills for it, so your AI coding agent knows how to install, set up, run and check
shotfleet, and how to read the report:

| Skill | What it does |
|---|---|
| `shotfleet` | the main one: which command to run, exit codes, `--json`, writing the flow, troubleshooting |
| `shotfleet-review` | turns a check report into a fix list (which language to capture again, and if the fix is in the app or the flow) |
| `shotfleet-ci` | adds `shotfleet check` to GitHub Actions or another CI |

The skills tell your agent what to type. The agent still needs shotfleet itself on your Mac:

```bash
curl -fsSL https://shotfleet.com/install.sh | sh
```

## Install

### Claude Code

In a Claude Code session:

```
/plugin marketplace add noloman/shotfleet-skills
/plugin install shotfleet@shotfleet
```

Or from your shell:

```bash
claude plugin marketplace add noloman/shotfleet-skills
claude plugin install shotfleet@shotfleet
```

The plugin brings the three skills and the shotfleet MCP server (`shotfleet mcp`, with `check`, `run` and `doctor`).
The MCP server only starts if shotfleet is installed; without it, `/mcp` shows it as failed and the skills still work.
If you already ran `shotfleet skill install`, you'll see the skills twice. Remove one copy (`~/.claude/skills/shotfleet*`).

### GitHub Copilot, Codex, Cursor, Gemini CLI and others (gh)

With GitHub CLI 2.90 or newer:

```bash
gh skill install noloman/shotfleet-skills --all --scope user
```

Pick the agent with `--agent`, for example `--agent codex`, `--agent cursor`, `--agent gemini-cli` or
`--agent claude-code`. Leave out `--scope user` to install into the current project instead.

### Any agent (npx)

```bash
npx skills add noloman/shotfleet-skills --skill '*' -g
```

### Gemini CLI

```bash
gemini skills install https://github.com/noloman/shotfleet-skills.git --path skills/shotfleet
gemini skills install https://github.com/noloman/shotfleet-skills.git --path skills/shotfleet-review
gemini skills install https://github.com/noloman/shotfleet-skills.git --path skills/shotfleet-ci
```

### Already have shotfleet?

Then you already have the skills too. This copies them where Claude Code, Codex, Cursor, Gemini CLI and Copilot look:

```bash
shotfleet skill install
```

Start a new agent session after any of these, then ask something like "check my fastlane screenshots with shotfleet".

## Price

The skills are free, MIT licensed. In shotfleet, `check` is free and `run` is free for up to 2 languages. `run`
beyond 2 languages and `export` need a licence: [shotfleet.com](https://shotfleet.com).

## Your licence key

Never paste your licence key into an agent config, a chat, an MCP setting or a repo. Run this once yourself, in
your own terminal:

```bash
shotfleet activate <your key>
```

After that your agent uses shotfleet and never sees the key. In CI, put the key in a secret called `SHOTFLEET_KEY`.
Don't pass it with `claude mcp add --env`: it would end up in plain text in `~/.claude.json`.

## Questions

Write to me at hello@shotfleet.com. The files here are copied from the shotfleet source at each release, see
[SYNC.md](SYNC.md).
