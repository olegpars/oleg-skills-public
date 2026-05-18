# oleg-skills

Catalog hub for [@olegpars](https://github.com/olegpars)' public Claude Code skills.

This repo **does not contain skill code itself**. Each skill lives in its own companion repo (the homebrew-core pattern: this is the index, the upstream repo is the source of truth). The `.claude-plugin/marketplace.json` here points Claude Code at the skill sources via `git-subdir` references.

## Skill catalog

| Skill | What it does | Source repo |
|---|---|---|
| `dreamina-delogo` | Removes the fixed-position AI badge watermark from Dreamina / Seedance MP4 / MOV videos. Pure FFmpeg, runs locally, ~30s per 15s clip. | [olegpars/dreamina-delogo](https://github.com/olegpars/dreamina-delogo) |

## Install all skills via Claude Code marketplace

```
/plugin marketplace add olegpars/oleg-skills-public
/plugin install dreamina-delogo@oleg-skills
```

This pulls each skill from its source repo into your `~/.claude/skills/` automatically.

## Install one skill directly (without marketplace)

Each skill's source repo is fully self-contained — clone it directly and either open it as cwd in Claude Code (auto-trigger), or junction-mount it globally:

```powershell
# Windows
git clone https://github.com/olegpars/dreamina-delogo.git D:\path\to\dreamina-delogo

New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\dreamina-delogo" `
  -Target "D:\path\to\dreamina-delogo\.claude\skills\dreamina-delogo"
```

```bash
# Linux / macOS
git clone https://github.com/olegpars/dreamina-delogo.git ~/dreamina-delogo
ln -s ~/dreamina-delogo/.claude/skills/dreamina-delogo ~/.claude/skills/dreamina-delogo
```

## Why a separate hub repo

The skill's primary repo (`olegpars/dreamina-delogo`) is a **self-contained tool**: it has FFmpeg scripts, before/after examples, README, and bundles a `SKILL.md` so cloning it as cwd in Claude Code is enough. The Claude skill is one interface to that tool; the CLI scripts are another.

This `oleg-skills-public` repo plays the **registry / catalog** role — analogous to homebrew-core or anthropics/claude-plugins-official. It does not own skill content; it points at where skills actually live.

## Adding a new skill

1. Create or pick the skill's source repo (e.g. `olegpars/new-skill`) and ensure its `SKILL.md` lives at a known path (convention: `.claude/skills/<name>/SKILL.md`).
2. Add a row to the **Skill catalog** table above.
3. Append a `plugins[]` entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) with the `git-subdir` source pointing at that path in the source repo.
4. Commit and push. The new skill becomes installable from this hub.

## Related

- [olegpars/oleg-skills-private](https://github.com/olegpars/oleg-skills-private) — private repo of Oleg's personal Claude Code skills with machine-specific paths. Not relevant to community use.
- [olegpars/dreamina-delogo](https://github.com/olegpars/dreamina-delogo) — first skill source repo, FFmpeg watermark remover.
