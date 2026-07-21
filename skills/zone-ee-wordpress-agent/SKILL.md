---
name: zone-ee-wordpress-agent
description: Safely manage WordPress websites hosted on Zone.ee, including access setup, staging, content and theme updates, multilingual pages, forms, email delivery, DNS/SSL checks, backups, and SEO launch checks. Use when work involves editing, publishing, troubleshooting, migrating, localizing, or auditing a Zone.ee-hosted WordPress site.
license: MIT
compatibility: Requires an authorized WordPress or Zone.ee access method. A WordPress application password is suitable for REST content work; hosting access is needed only for infrastructure tasks.
metadata:
  repository: https://github.com/KristjanToop/zone-ee-wordpress-agent-skill
  version: "1.0.0"
---

# Zone.ee x WordPress Agent Skill

Use this skill to make site changes safely and leave a clear handoff. Default to staging; production changes require the site owner's explicit approval in the current request.

## Canonical repository

This skill is maintained in the public repository [KristjanToop/zone-ee-wordpress-agent-skill](https://github.com/KristjanToop/zone-ee-wordpress-agent-skill). It follows the open Agent Skills format and may be used by any compatible agent. Use the repository for installation, updates, issues and contributions. Never add client prompts, site credentials, customer data, backups or private operational notes to the repository.

## First-time setup

Before making the first change for a site, establish the working setup. Do not proceed to edits until the available access, environment, and recovery path are clear.

1. **Map the site.** Record the production URL, staging URL or path, WordPress admin URL, and the name of the active theme, page builder, and language/form/SEO plugins.
2. **Create a dedicated WordPress user.** Ask the owner to create a separate administrator account for the authorized agent, using an email address they control. Use this account only for the work requested. Do not use or request the owner's personal administrator password.
3. **Use an application password for REST work.** In that dedicated WordPress user's profile, create an application password with a neutral label such as `Site agent`. Share it only through the active task and never commit, display, or repeat it. Confirm access with a harmless read request before making changes.
4. **Set up hosting access only if needed.** For site content and settings, WordPress access is normally enough. If DNS, SSL, files, backups, database, or mail settings are in scope, have the owner grant the narrowest suitable Zone.ee or SFTP/SSH access. Start with read-only inspection.
5. **Create or identify staging.** Prefer a staging site that mirrors production and has a clear URL such as `/staging/` or `staging.example.com`. Keep it blocked from indexing and do not treat it as permission to edit production.
6. **Confirm rollback.** Identify who can restore a backup and where the latest restorable copy lives. Before the first production release, confirm there is a current backup and a way to revert the precise change.
7. **Agree the release rule.** Make changes and checks on staging first. Only publish to the production URL after the owner explicitly approves the exact scope in the current request.

If any setup element is unavailable, explain the smallest next action the owner must take. Never ask them to paste credentials into a repository, screenshot, or permanent document.

## Start with the site profile

Ask for or inspect only the details needed for the request. For a reusable handoff, copy the non-secret fields from [references/site-profile-template.md](references/site-profile-template.md). Never put passwords, app passwords, API keys, database credentials, or recovery codes in a skill, repository, page, or chat recap.

Identify:

- the production and staging URLs;
- the allowed access method: WordPress admin, WordPress REST application password, SFTP/SSH, or Zone.ee control panel;
- who owns DNS, email sending, and backups;
- whether the site uses an FSE template, page builder, or classic theme;
- multilingual plugin and language URL structure.

## Choose the safe control surface

Use the least-privileged method that can complete the task.

- Use WordPress REST for repeatable, content-only updates when an application password is available.
- Use WordPress admin for plugin settings, Yoast fields, WPForms, language-plugin settings, and other settings not safely exposed by REST.
- Use Zone.ee only for hosting, domains, DNS, SSL, mail, databases, and server access.
- Use SFTP/SSH only when the change genuinely requires files or server configuration.

Do not expose credentials in terminal output, templates, code, commits, screenshots, or final responses. Do not test with a real visitor's data.

## Change workflow

1. Confirm the target URL and environment. Treat `/staging/`, a staging subdomain, or an explicitly marked test install as staging; do not infer that a live-looking URL is safe to edit.
2. Inspect the relevant page, template, plugin settings, and current public output before changing anything.
3. Make the smallest change that satisfies the request. Preserve unrelated user changes in a dirty workspace.
4. For layout work, check desktop and mobile. For multilingual work, check every language and language switcher.
5. Publish to staging, then verify the public rendered result, not only the editor state.
6. Before production, confirm the exact scope with the user, take or confirm a recoverable backup, publish, and re-check the public URL.

For direct production work, announce the exact target and the change immediately before writing. Never mass-delete posts, media, users, databases, or files without specific authorization and a validated target.

## WordPress specifics

### Themes and templates

Determine whether content is in the page body, an FSE template, a reusable block/pattern, or a page-builder record. Update the actual source of rendered content; otherwise an apparently saved change may not appear publicly.

Keep a local, timestamped copy of a complex custom HTML/CSS template before replacing it. Use narrowly scoped CSS overrides and verify that they do not break the other language or mobile layout.

### Multilingual pages

Keep translations paired in the active language plugin. Validate all of the following:

- the translated page is linked to its counterpart;
- language links lead to clean, intended URLs;
- `<html lang>`, `hreflang`, canonical URLs, title tags, and meta descriptions match the page language;
- translated navigation and form labels are complete.

For Estonian copy, use an available Estonian language checker or MCP for spelling and unusual compound checks. Preserve user-approved English product names and terms where localization would damage the brand.

### Forms and email

Prefer an installed form plugin such as WPForms over custom mail code.

- Include name, reply email, and message at minimum.
- Set the notification recipient explicitly and use the submitter's address as Reply-To where the plugin supports it.
- Add a clear confirmation message and basic spam protection available in the installed plugin.
- Verify form placement and mobile layout.
- Confirm delivery through the configured mail transport. If WordPress sends unreliably, configure or request an approved SMTP/transactional-email service; do not claim delivery works merely because the form saved.
- Sending a real test message is an external side effect. Confirm the recipient and test before sending it.

### SEO and launch checks

Audit public rendered HTML and server responses, not just editor fields.

- One descriptive H1 per page, with the primary term naturally included.
- Unique title and meta description for every indexable language page.
- Correct canonical and reciprocal `hreflang` links.
- Staging should normally be `noindex`; production pages intended for search must not be.
- `robots.txt` must permit crawling and point to an accessible sitemap.
- Verify the production sitemap resolves successfully and contains indexable canonical URLs.
- Use real alt text for meaningful images and avoid duplicate page titles.

Do not turn on indexing for staging or production without explicit authorization.

## Zone.ee checks

For DNS, SSL, and hosting work:

- inspect the existing records before changing them;
- use the smallest DNS change possible and record the prior value;
- do not remove MX, SPF, DKIM, DMARC, or nameserver records unless the user explicitly identifies them as the target;
- verify HTTPS, certificate coverage, and redirect behaviour after domain changes;
- distinguish website mail delivery from mailbox hosting and transactional SMTP.

## Handoff

Report the environment changed, the user-visible outcome, and verification performed. Mention any remaining dependency, especially email delivery, cache propagation, DNS propagation, or production indexing. Do not include secrets in the handoff.
