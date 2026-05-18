# oleg-skills

Public Claude Code skills by [@olegpars](https://github.com/olegpars). Generic, shareable versions.

| Skill | What it does | Companion tool |
|---|---|---|
| [`dreamina-delogo`](skills/dreamina-delogo/) | Removes the fixed-position AI badge watermark from Dreamina / Seedance MP4 / MOV videos. Pure FFmpeg, runs locally, ~30s per 15s clip. | [olegpars/dreamina-delogo](https://github.com/olegpars/dreamina-delogo) (scripts + before/after examples) |

---

## dreamina-delogo

Dreamina (ByteDance Seedance) stamps a small **AI** badge in the top-left corner of every generated video. If you're cutting a Reel/Short and want it clean, you need it gone. Online removers want you to upload your footage to their server. This skill does it on your laptop in ~30 seconds per 15s clip — pure FFmpeg, no AI, no cloud.

**See before / after:** [olegpars/dreamina-delogo#examples](https://github.com/olegpars/dreamina-delogo#examples) (two pairs + side-by-side comparison)

### Quick install (the skill + the script)

```bash
# 1. Clone the script repo (the actual FFmpeg work)
git clone https://github.com/olegpars/dreamina-delogo.git

# 2. Clone this skills repo
git clone https://github.com/olegpars/oleg-skills-public.git
```

Then either open `oleg-skills-public` as the cwd of a Claude Code session (auto-trigger), or junction-mount the skill globally — see [global install](#global-install) below.

### Run it directly (no Claude Code needed)

```bash
cd dreamina-delogo
bash delogo.sh /path/to/video.mp4              # single file
bash delogo.sh /path/to/folder                  # whole folder
```
PowerShell: `./delogo.ps1 <file-or-folder>`. Full docs and tunable parameters: [olegpars/dreamina-delogo](https://github.com/olegpars/dreamina-delogo).

---

## Global install

To make these skills trigger from **any** Claude Code session (not only when this repo is cwd):

### Windows (NTFS junction, no admin required)

```powershell
git clone https://github.com/olegpars/oleg-skills-public.git D:\path\to\oleg-skills-public

# Mount one skill into ~/.claude/skills/:
New-Item -ItemType Junction `
  -Path "$env:USERPROFILE\.claude\skills\dreamina-delogo" `
  -Target "D:\path\to\oleg-skills-public\skills\dreamina-delogo"
```

Repeat the `New-Item` line for each skill you want active.

### Linux / macOS

```bash
git clone https://github.com/olegpars/oleg-skills-public.git ~/oleg-skills-public
ln -s ~/oleg-skills-public/skills/dreamina-delogo ~/.claude/skills/dreamina-delogo
```

### Plugin marketplace (when Anthropic's `/plugin install` is available)

This repo includes a [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) manifest, so you can install via:

```
/plugin marketplace add olegpars/oleg-skills-public
/plugin install oleg-skills@oleg-skills-public
```

---

## Structure & rule

```
olegpars/oleg-skills-public   ← this repo: generic SKILL.md files, community-facing
olegpars/<skill-name>         ← optional companion repo: scripts/binaries (e.g. dreamina-delogo)
olegpars/oleg-skills-private  ← Oleg's personal/local copies (private, not relevant to you)
```

A skill that needs no scripts (pure prompt instructions) lives only here. A skill that needs binaries (FFmpeg pipelines, Python scripts, etc.) gets a **companion tool repo** — that repo can be used standalone, and the SKILL.md here wraps it for Claude Code with clone instructions.

## Adding a new skill (PRs welcome)

1. Create folder `skills/<skill-name>/SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: skill-name
   description: One-line trigger description (when Claude should use this skill).
   ---
   ```
2. Body: what the skill does, when to use it, when NOT to use it, quick reference, common mistakes.
3. Add an entry to the catalog table at the top of this README.
4. Append the skill path to `.claude-plugin/marketplace.json` under `plugins[0].skills`.

## License

MIT — see [LICENSE](LICENSE) if/when added. Until then, treat as MIT-equivalent: fork, copy, adapt freely.
