# website-workflow

A [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that turns Claude into an
end-to-end project lead for building websites when *you* are not a developer ("vibe coding").
It drives a fixed flow — GitHub setup, understanding the idea, research, planning, development,
testing, and release — so you always know what's next, without needing to read or write code
yourself.

## Who this is for

Freelancers and non-developers who build websites (for clients or for their own ideas) with
Claude doing the implementation. The skill assumes you can describe what you want, but not that
you can debug HTML/CSS or read a diff.

## What it does

- Asks scope questions up front (client project vs. own idea, landing page vs. multi-page site)
  and adjusts the workflow accordingly (proposal, client sign-off, credential handover, and a
  maintenance phase only apply to client projects).
- Walks through 7 phases: GitHub setup → understand the idea → research → plan → development →
  code review & testing → release, plus an optional maintenance phase for client work.
- Bakes in a conversion-copy framework (the Value Equation) for landing pages, plus visual-flow
  guidance (Z-pattern, F-pattern, Gutenberg diagram) for page layout.
- Treats testing as the assistant's job: it drives the browser itself rather than asking you to
  click through the site.
- Includes a legal checklist reflecting German requirements (Impressum, GDPR, cookie banner,
  accessibility) — explicitly flagged as jurisdiction-specific, adapt it for your own country.

## Installing

Copy this skill into your Claude Code skills directory:

```bash
git clone https://github.com/<your-username>/website-workflow-skill.git ~/.claude/skills/website-workflow
```

Or, if you keep skills per-project, place `SKILL.md` in `.claude/skills/website-workflow/` inside
your repository.

## Optional companion skills

This skill suggests (never auto-runs) an external design-polish skill called `impeccable` at
several points in the workflow if you happen to have it installed — it's not required, and the
workflow degrades gracefully without it (those suggestions are simply skipped). Everything else
in this skill is self-contained.

For code review and security review steps in phase 6, it references Claude Code's own built-in
`code-review` and `security-review` skills.

## Customizing

- **Legal section:** written for Germany/EU. If you're building for a different jurisdiction,
  replace the checklist with your local requirements before relying on it.
- **Language:** written in English. If your workflow with clients happens in another language,
  feel free to translate — the phase structure and rules translate directly.

## Disclaimer

The legal checklist in this skill is not legal advice — it exists so the topic isn't forgotten,
not to replace a lawyer or a jurisdiction-appropriate generator/template.

## License

MIT — see [LICENSE](LICENSE).
