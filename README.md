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
- Builds a production baseline (access control, reset-link expiry, input validation, CORS, rate
  limiting, custom error pages, database indexes, logging/alerts, rollback) *during* development
  when each trigger appears — the first form, login, table, or endpoint — scaled to what the
  project actually needs. The testing phase only verifies it; nothing is left for a last-minute
  pre-deployment checklist.
- Asks which market(s) the site is for (where the business is based, where its customers are),
  then researches that market's actual legal requirements (business disclosure, privacy law,
  cookie consent, accessibility) instead of assuming any one country's rules by default.

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

- **Legal & compliance:** market-agnostic by design — phase 0 asks which country/countries the
  site is for, and phase 3 researches that market's actual requirements at build time rather than
  the skill hardcoding one country's rules. If you only ever build for one market, you can trim
  phase 0's question and phase 3's research step down to that market directly.
- **Language:** written in English. If your workflow with clients happens in another language,
  feel free to translate — the phase structure and rules translate directly.

## Disclaimer

The legal guidance in this skill is not legal advice, for any jurisdiction — it exists so the
category of requirement (business disclosure, privacy policy, cookie consent, accessibility, etc.)
isn't forgotten. Always have the actual text/mechanism checked by a lawyer or a
jurisdiction-appropriate generator/template for the market in question.

## License

MIT — see [LICENSE](LICENSE).
