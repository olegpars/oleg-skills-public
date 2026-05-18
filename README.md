# oleg-skills-public

Public Claude Code skills by [@olegpars](https://github.com/olegpars). Generic, sharable versions.

For Oleg's personal/local-only skills (with absolute paths to his machine) see private repo `oleg-skills-private`.

## Install

Clone this repo and either:

**Option A — one-time use** in a specific Claude Code session: open this repo as the cwd and the skills auto-trigger.

**Option B — global install** so skills trigger from any Claude Code session (Windows, NTFS):
```powershell
git clone https://github.com/olegpars/oleg-skills-public.git D:\path\to\oleg-skills-public
# Junction-mount into your ~/.claude/skills/ (no admin required):
New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\dreamina-delogo" `
  -Target "D:\path\to\oleg-skills-public\skills\dreamina-delogo"
```

**Linux/macOS symlink equivalent:**
```bash
ln -s /path/to/oleg-skills-public/skills/dreamina-delogo ~/.claude/skills/dreamina-delogo
```

## Skills in this repo

| Skill | What it does | Companion repo |
|---|---|---|
| `dreamina-delogo` | Removes fixed-position AI badge watermark from Dreamina/Seedance MP4/MOV videos using pure FFmpeg | [olegpars/dreamina-delogo](https://github.com/olegpars/dreamina-delogo) (scripts + examples) |

## How this fits

```
olegpars/oleg-skills-private  (private) — Oleg's personal Claude Code skills, all of them, junction-mounted at his ~/.claude/skills/
olegpars/oleg-skills-public   (public, this repo) — generic versions of shareable skills
olegpars/<skill-name>         (public) — script/binary repos for skills that need them (e.g. dreamina-delogo with FFmpeg scripts)
```
