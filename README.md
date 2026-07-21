# Zone.ee x WordPress Agent Skill

[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-open%20standard-5B21B6)](https://agentskills.io)
[![skills.sh](https://skills.sh/b/KristjanToop/zone-ee-wordpress-agent-skill)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)
[![License: MIT](https://img.shields.io/badge/License-MIT-10B981)](LICENSE)

[![Add to Claude Code](https://img.shields.io/badge/Add%20to-Claude%20Code-D97757)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)
[![Add to Codex](https://img.shields.io/badge/Add%20to-Codex-10A37F)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)
[![Add to Cursor](https://img.shields.io/badge/Add%20to-Cursor-111827)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)
[![Add to GitHub Copilot](https://img.shields.io/badge/Add%20to-GitHub%20Copilot-0969DA)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)
[![Add to Gemini CLI](https://img.shields.io/badge/Add%20to-Gemini%20CLI-4285F4)](https://skills.sh/KristjanToop/zone-ee-wordpress-agent-skill)

A portable, staging-first workflow for safely managing WordPress sites hosted on Zone.ee.

The skill covers access setup, staging, backups, page and template changes, multilingual content, forms, email delivery, SEO, DNS and SSL. It contains no client-specific prompts, site configuration, credentials or operational data.

## Install

The standard `npx skills` installer supports a broad range of compatible coding agents. The universal install starts an interactive agent selector:

```bash
npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global
```

| Agent | Install globally |
| --- | --- |
| Claude Code | `npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global --agent claude-code --yes` |
| Codex | `npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global --agent codex --yes` |
| Cursor | `npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global --agent cursor --yes` |
| GitHub Copilot | `npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global --agent github-copilot --yes` |
| Gemini CLI | `npx skills add KristjanToop/zone-ee-wordpress-agent-skill --skill zone-ee-wordpress-agent --global --agent gemini-cli --yes` |

GitHub READMEs cannot safely run an installation on someone else's computer with one click. The agent buttons open the skill page, and the commands are intentionally explicit about the agent and installation scope.

## Design principles

- The source of truth is a standard `SKILL.md` folder, not a vendor-specific plugin.
- Start with safe access, staging and rollback before changing a site.
- Use the least-privileged access needed for each task.
- Keep production publishing explicit and reversible.
- Keep client context and credentials outside this repository.

## Repository structure

```text
skills/zone-ee-wordpress-agent/
├── SKILL.md
└── references/
    └── site-profile-template.md
```

## Contributing

Contributions are welcome. Keep all proposed additions reusable and vendor-neutral. Do not include client prompts, real URLs, credentials, backups, screenshots with account data, or private operational notes.

## License

[MIT](LICENSE)
