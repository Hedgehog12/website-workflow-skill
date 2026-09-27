---
name: website-workflow
description: >
  Activate this skill when a new website/client project starts, or when it's
  unclear what phase an ongoing project is currently in. The user is not a
  developer ("vibe coding") and builds websites for clients or to make money.
  Fixed flow: GitHub setup -> understand the idea -> research -> make a plan
  -> development -> code review + testing -> release. At the start, scope is
  clarified (freelance client project vs. own idea) — this determines whether
  a proposal, client sign-off, credential handover, and a maintenance phase
  are part of the project. Trigger situations: "new project", "new website",
  "starting a client project", "how do I get started", "I have an idea but
  no idea how to start", "is this ready for release", "can you check this
  again before I upload it", "do I need a legal notice/privacy
  policy/cookie banner", "write a proposal for a client", "hand the project
  over to the client", or when the user is mid-project and doesn't know
  what the next step is. Main skill for the entire website-building process:
  it can also orchestrate the external `impeccable` skill (design polish, if
  installed) at the right phases, but only ever suggests it rather than
  running it automatically.
---

# Website Workflow for Vibe Coding (No Developer Background)

## Core rules

**The user does not write code themselves and has no development
background.** They don't understand code and should never have to read it.
Explanations: plain language, with technical terms briefly explained in
parentheses when needed. Before risky/irreversible steps (deploying,
switching a domain, deleting data): always explain first, then ask.

**Lead actively, don't just react.** The default case: the user has an idea
for a website but no idea what to do next. Always state yourself what the
next step is and why — don't wait to be asked. The goal is a professionally
built site even though the user has no development experience themselves.

**Short what+why explanation at every notable step.** The user wants to
learn along the way so future projects go faster. After every relevant
action (decision, building block, fix): 1-2 sentences on what was done and
why — not a tutorial, not an essay. For trivial/routine steps (e.g.
creating a file), a half-sentence is enough, or skip it entirely.

**No filler text.** Keep responses as short as possible, as long as
necessary. No repetition, no throat-clearing intros, no summarizing things
already said.

**Testing is done by the assistant, not the user.** Every test that can be
run programmatically (browser clicks, filling out forms, checking links,
responsive views, golden path + error cases) is carried out independently
with the available tools (browser preview, automated testing tools, etc.)
— the user is not asked to test things themselves. Only when a test
demonstrably fails this way, or is technically impossible (e.g. a real
payment, a real mailbox, access only the user has), is the user asked to do
that one specific step — with an explanation of why there's no other way.

**Code as simple as possible.** Before every implementation, briefly check:
can this be done more simply, with less code? No abstractions,
configuration options, or architecture "for later" that nobody needs right
now. Prefer duplicated simple code over a premature, clever abstraction.
The goal must be met — but with the leanest solution that gets there.

**Work token-consciously.** Thorough testing (see above) doesn't mean
working wastefully — avoid bloat, not thoroughness:
- Read/search targeted, not broad — load only the relevant file excerpts or
  search hits, not whole folders or large files "just to be safe."
- After small changes, only re-test/re-review the affected parts, not the
  entire golden path on every minor fix.
- Close out sessions cleanly per phase/project: `README.md`/`BRIEF.md`/
  `CHANGELOG.md` capture the current state so a new session can read from
  them instead of reprocessing the whole prior history.
- Use subagents/web research only for genuinely complex/broad tasks, not by
  default for simple steps (see the "code as simple as possible" rule).
- Short answers (see "no filler text") also save output tokens.

**The `impeccable` skill (optional, external): suggest it, don't use it
automatically.** `impeccable` is an external skill with slash commands for
design polish (full overview below), if the user has it installed. It costs
extra context, so it must never be invoked automatically. Instead, suggest
it actively at the points marked below, e.g.: "This would be a good spot
for `/impeccable <command>`, because <short reason>. Want me to do that?"
Only run it after agreement — the user consciously decides case by case
whether the extra context is worth it. This skill acts as an orchestrator:
it knows which `impeccable` command fits where, but never calls it on its
own initiative. If `impeccable` isn't installed, skip these suggestions
silently.

The core flow has seven phases (1-7). There are also two framing phases (0
and 8) that only run for client projects. For every new project, start at
the top. For ongoing projects: briefly ask/detect where things currently
stand and continue from there — don't stubbornly start at phase 1.

---

## `impeccable` skill: capability overview (reference for suggestions)

An external, optional skill for design polish on AI-generated interfaces.
This table is only a reference for suggesting the right command at the
right phase (see core rule above) — never run automatically, and only
relevant if the user has this skill installed.

| Command | Category | What it does | When to suggest |
|---|---|---|---|
| `/impeccable` | Create | Next-step recommendation or free-form description of design work | Any time it's unclear which command fits |
| `/shape` | Create | Design brief through discovery instead of guessing | Phase 4, before implementation |
| `/audit` | Evaluate | Technical quality check, 5 dimensions, P0-P3 severity | Phase 6, before release |
| `/critique` | Evaluate | Design review with scoring, persona tests, automatic detection | Phase 6, before the final polish pass |
| `/animate` | Refine | Purposeful motion instead of decoration | Phase 5, for transitions/interactions |
| `/bolder` | Refine | Make safe, generic designs stronger | Phase 5/6, when the design feels too timid |
| `/colorize` | Refine | Strategic color for monochrome interfaces | Phase 5, when the palette feels grey/lifeless |
| `/delight` | Refine | Small moments of personality | Phase 5/6, optional for brands with a lot of character |
| `/layout` | Refine | Spacing, grid, visual rhythm | Phase 5, ongoing while building |
| `/overdrive` | Refine | Shaders/physics/60fps, technically demanding effects | Only for an explicit "wow" requirement (e.g. a portfolio/launch landing page), very optional |
| `/quieter` | Refine | Calm down designs that are too loud, without losing the message | Counterpart to `/bolder`, when it's too much |
| `/typeset` | Refine | Fix typography hierarchy | Phase 5/6, when the type feels generic/inconsistent |
| `/adapt` | Simplify | Responsive without losing functionality | Phase 5/6, during the responsive check |
| `/clarify` | Simplify | Rewrite confusing UX copy more clearly | Phase 5/6, for forms/CTAs/error messages |
| `/distill` | Simplify | Radically reduce to the essential | Phase 6, when the page feels overloaded (pairs with the value check) |
| `/harden` | Harden | Production-ready: edge cases, i18n, error states, overflow | Phase 6, right after `/audit` |
| `/onboard` | Harden | First-run experience, empty states, path to value | Phase 4/5, for pages with login/dashboard |
| `/optimize` | Harden | Performance, LCP through bundle size | Phase 6, complements the performance check above |
| `/polish` | Harden | Last, meticulous polish pass before release | Phase 6, final step before release |
| `/document` | System | Creates/updates `DESIGN.md` as persistent design context | Phase 4 (set the baseline) and again Phase 7 (freeze the final state) |
| `/extract` | System | Pulls out reusable components/tokens/patterns | Phase 6, if a design system should emerge |
| `/live` | System | Interactive browser iteration: pick an element, comment, 3 variants | Phase 5, for detail work in the running preview |
| `/init` | System | Initially creates `PRODUCT.md` + `DESIGN.md` | Once, right after phase 1, before phase 4 |

---

## Phase 0: Define scope (once per project)

Goal: before anything else happens, clarify which steps this project
actually needs — don't run through everything by default.

- Ask: "Is this a client project (freelance work) or your own idea?" This
  determines whether the following steps are active:
  - **Client project:** proposal (below), client sign-off (phase 7),
    credential handover (phase 7), maintenance phase (phase 8) — all active.
  - **Own idea:** all four are off by default.
- Also ask separately: "Should analytics be set up?" — applies regardless
  of project type, since it's useful for personal projects too.
- Also ask: "Is this a landing page (one page, one conversion goal) or a
  multi-page website?" For a landing page: activate landing-page mode (see
  phase 4 and phase 6) — this unlocks CRO-specific structure and review
  points based on conversion-focused landing-page strategy (see the Value
  Equation framework in phase 4).
- Briefly confirm what follows from this ("Ok, so no proposal/sign-off,
  with analytics"), so the user knows what's different in this project.
- Don't re-ask this decision at every step — decide once, note it in
  `BRIEF.md` (phase 2), then it applies to the whole project.

**Only for client projects — create a proposal:**
Draft a short, ready-to-send proposal for the client (scope, price,
timeline). Apply value-based pricing principles: lead with the outcome/
benefit for the client, not hours worked; anchor the price against the
cost of the alternative (doing nothing, or a competitor); make scope and
price unambiguous so there's no room for scope creep later. Never send a
proposal without the user's confirmation (it goes out to a third party).

---

## Phase 1: GitHub setup

Goal: there's a place where the project state is safely stored and every
change can be rolled back.

- Check: does a repo/folder already exist? If not: create one (local is
  enough to start, a GitHub repo once it gets serious).
- No push to a remote repo without brief confirmation (a visible action for
  third parties).
- Create `README.md` if it doesn't exist yet: what the project is, how to
  start/test it locally, a link to the live site (once it exists). Keep it
  short, no documentation prose.
- **Suggest impeccable:** `/init` (creates `PRODUCT.md` + `DESIGN.md`) —
  only suggest if the `impeccable` skill is installed, never run it
  automatically (see core rule).

## Phase 2: Understand the idea

Goal: before anything gets built, be clear on WHAT and FOR WHOM.

Always clarify (if not already known):
1. Who is the target audience / who is the client?
2. What should the site make the visitor do (get in touch? buy?
   get informed?) — that's the actual goal, not "have a website."
3. Are there references/role models (other sites the user likes)?
4. Must-have content/pages (home, contact, pricing, portfolio...)?
5. Is there already copy/images/branding, or does that need to be planned
   too?
6. **Core message:** what problem does the site solve, and what's the one
   sentence that has to land immediately when the page opens? Don't
   describe the product/feature — describe the outcome/benefit for the
   visitor. A quick way to frame this: the visitor's perceived value roughly
   scales with the dream outcome and how likely/fast they believe it is,
   and scales down with the effort and delay involved (see the fuller Value
   Equation breakdown in phase 4). Without a clear answer here: don't keep
   building — ask/work it out first.

Don't guess when these points are missing — ask directly and briefly
instead of building on assumptions.

At the end of this phase: capture the answers to 1-6 in `BRIEF.md`. Bullet
points, not full sentences. If requirements change later in the project:
update `BRIEF.md` instead of creating a second source of truth.

## Phase 3: Research

Goal: preparation for a good plan — only once the idea is clear (phase 2
done), not before.

- Research the right approach/technology for this specific case (e.g.
  which setup/framework/service makes sense for this kind of site, current
  best practices, known pitfalls).
- If useful, look at 2-3 reference sites/solutions that already do
  something similar well.
- Summarize the result briefly and in plain language: what was found, what
  it means for the plan — no research report, just the essence.
- Don't skip this phase even if the project looks small: it's the reason
  the plan afterward is accurate instead of a guess.

## Phase 4: Make a plan

Goal: a simple structure, understandable for a non-technical person, before
any code exists — based on the idea (phase 2) and research (phase 3).

- Site structure as a short list (which pages/sections, in what order).
- Make technical decisions (framework, hosting) yourself and only
  communicate the result + reason in 1-2 sentences — the user doesn't need
  to understand or approve a technology choice unless cost/dependencies are
  affected.
- For bigger projects: use plan mode and summarize the plan in simple,
  non-technical language before building starts.
- Decide the build order: scaffold + most important page first, then the
  rest — so something visible exists early.
- Include a legal-notice page and a privacy-policy page in the site
  structure from the start (see the "Legal" section below) — don't bolt
  them on right before release.
- **Decide a model per task (once the plan is set):** briefly research
  current model capabilities, then estimate per planned task which model
  fits and note it in the plan:
  - **The most capable/expensive model:** complex/creative tasks —
    architecture decisions, design, hard bugs, tasks with high cost of
    error.
  - **A mid-tier model:** normal development work — most standard tasks.
  - **The fastest/cheapest model:** simple, mechanical tasks — text
    corrections, formatting, simple repetitive tasks.
  Goal: don't waste a large/expensive model on trivial tasks, but also
  don't hand a hard task to a model too small to do it well.
  - **Automatic where possible:** when a task is delegated to a subagent,
    pass the right model directly as a parameter — this is the only case
    where the switch is truly automatic.
  - **Otherwise, flag it actively:** when a task runs in the main
    conversation, the model can't be switched by the assistant itself.
    Before starting any task with a differing model recommendation, say so
    briefly and concretely (e.g. "Next task: X — recommended model Y,
    please switch"), rather than silently continuing with the wrong model.
- **Check loop-suitability per task (once the plan is set):** not every task
  benefits from an autonomous loop phase (see phase 5). For each planned
  task, assess and mark in the task overview/milestone plan whether it's
  handled as a loop or classically/directly:
  - **Loop-suitable:** iterative, well-testable tasks with clear success
    criteria — e.g. refactoring, component development, test coverage,
    bug fixing, API integrations, CSS/responsive adjustments.
  - **Not loop-suitable (solve classically/directly):** one-off
    conceptual work, pure architecture decisions, simple text/content
    changes, unclear or subjective requirements.
  When unsure, don't decide alone — briefly align with the user, since this
  directly steers how the task is handled in phase 5.
- Plan the core message (phase 2, point 6) firmly into the first visible
  area (hero/top section) — not buried somewhere on the page. It must be
  visible without scrolling.
- **Plan visual flow / reading direction** (how people actually read the
  page, not how it could theoretically be structured):
  - Image-heavy, text-light areas (hero, landing-page sections): the eye
    follows a Z-pattern — top-left (logo/entry point) to top-right
    (nav/secondary), diagonally to the center, ending bottom-right. That's
    exactly where the most important call-to-action (CTA) belongs.
  - Text-heavy areas (blog, long explanations): the eye follows an
    F-pattern — mostly scanning left and top. Put the most important word/
    claim at the start of headings and paragraphs, not buried in the
    middle or end.
  - Gutenberg diagram as a rule of thumb: top-left = seen first (strongest
    zone), bottom-right = where the eye naturally ends (second-strongest
    zone, ideal CTA spot), top-right = weakest zone, suited for secondary
    items (e.g. a language switcher), not core messages.
  - Visual hierarchy: exactly one clear focal point per section (via size/
    contrast/color/whitespace). Several equally loud elements next to each
    other compete for attention instead of guiding the eye.
- **Only in landing-page mode (phase 0) — structure using a
  conversion-focused strategy:**
  - **Above the fold is the priority:** 100% of visitors see this area,
    ~60% never scroll further. So spend 80-90% of the design effort (and
    later optimization effort) on the headline + hero image — that's the
    single biggest lever for conversion rate.
  - **Apply the Value Equation concretely to the landing page** (a
    conversion framework popularized by Alex Hormozi in "$100M Offers" —
    generic, publicly documented marketing knowledge, not proprietary
    here):
    | Lever | Concrete implementation |
    |---|---|
    | Dream Outcome | Big benefit directly in the headline, following a "so that..." pattern (feature → outcome). Hero image shows the outcome, not the product. |
    | Perceived Likelihood | Visual social proof instead of plain text reviews (before/after, screenshots, video testimonials, a "wall of love"). Never hide it in a carousel. |
    | Risk Reduction | Risk reversal directly under the CTA button (money-back guarantee, "no credit card required," etc.). |
    | Time Delay | Concrete time reference in headline/subheadline ("in 30 days," "in 2 weeks"), never a vague timeframe. |
    | Effort & Sacrifice | Subheadline explains that it takes no effort/pain. "How it works" with at most 3-4 steps — more steps raise the perceived barrier. |
  - **Write headings for scanners:** visitors scan instead of reading. No
    generic subheadings like "How it works" or "What our customers say" —
    every heading must carry the value on its own (e.g. state the concrete
    outcome or mechanism directly as the heading).
- **Suggest impeccable:** `/shape` (design brief through discovery instead
  of guessing, before building) and `/document` (create `DESIGN.md` as a
  design-system baseline before phase 5 starts). For pages with a login/
  dashboard, also consider `/onboard` (first-run experience/empty states).
  Only suggest, never run automatically (see core rule).

## Phase 5: Development

Goal: build in small, checkable steps — not all at once. Simplest solution
first (see the "code as simple as possible" core rule).

- After every visible intermediate step: check it yourself in the browser
  (use the browser preview), don't just claim "done." The user doesn't
  click along themselves, they only see the result.
- Commit (git) after every working intermediate step — not just at the
  end. That way every state can be restored individually. Mention briefly
  that a commit was made, no git lecture.
- Short what+why updates in plain language (see core rules) — no technical
  log, no long paragraphs.
- If a client requirement can't be implemented cleanly/sensibly: say so
  transparently and suggest a better alternative, instead of silently
  building a workaround.

**For tasks marked loop-suitable in phase 4 — loop preparation:** before
such a task runs autonomously, define four building blocks:
- **Spec:** precise technical description of exactly what should be
  built/changed — not a vague description.
- **Checklist (definition of done):** unambiguous, checkable completion
  criteria. No subjective goals like "looks good" — every point must be
  objectively verifiable.
- **Inspector:** a check mechanism that automatically evaluates every
  iteration (e.g. linter, tests, build checks, DOM/HTML validation,
  automated browser checks).
- **Budget & guardrails:** a maximum number of iterations/attempts, plus
  safety stop conditions (e.g. no changes to certain files, no force-push,
  no self-initiated deployment).

If important details for any of these four building blocks are missing:
ask specifically before finalizing the loop — don't start on assumptions.

**Confirm before starting a loop (trigger point):** before starting any
loop phase, show a short overview (goal, checklist, inspector, budget) and
explicitly ask for confirmation. No loop starts without this confirmation —
the autonomous phase runs without constant check-ins afterward, so the
starting point must be clearly signed off beforehand.

**Execution & final report:** during the autonomous phase: build, have the
inspector check it, self-correct on failure — repeat the cycle until the
checklist is fully met or the budget runs out. Afterward, always give a
short final report: what was achieved, how many iterations it took. If the
budget runs out before the checklist is fully met: say transparently what's
still open, instead of presenting the state as done.

- **Suggest impeccable when an intermediate state doesn't look right
  yet:** `/layout` (spacing/grid), `/typeset` (typography), `/colorize`
  (color for grey areas), `/animate` (transitions), `/clarify` (UX copy),
  `/adapt` (responsive), or `/bolder`/`/quieter` (design too timid/too
  loud). `/live` is a good fit when iterating on an element directly in
  the running preview (comment → three variants). Only suggest when
  something visually stands out — not routinely after every step (see the
  "impeccable: suggest, don't auto-run" core rule).

## Phase 6: Code review + testing

Goal: check before release whether everything actually works — not just
"looks done." All checks in this phase are done by the assistant itself
(see the "testing is done by the assistant" core rule); the user is only
involved on a demonstrated failure or a technically impossible case.

- Run a code review on the changes before anything counts as done. Also
  check whether the code became unnecessarily complex and could be
  simpler.
- Use available browser-automation tools to walk through the real user
  path (golden path + likely error cases: empty form, wrong format,
  mobile view).
- For forms, login, payments, or other sensitive areas: also consider a
  dedicated security review.
- **Responsive check:** explicitly click through mobile, tablet, and
  desktop (not just one size), even if general testing partially covers
  this.
- **SEO basics:** title, meta description, and alt text for images set per
  page? Sitemap + robots.txt present? Without this, nobody finds the site
  via search engines.
- **Performance check:** a quick Lighthouse/PageSpeed check — especially
  load time and image sizes. Fix issues found (e.g. uncompressed images)
  before release, don't just note them.
- **Value check (hard, blocking):** open the page fresh and check — does a
  stranger understand the core message (phase 2, point 6) within 5
  seconds, without scrolling? If not: don't let it pass as done — rewrite
  the hero section using the Value Equation framework (phase 4) until the
  check passes.
- **Reading-flow check:** does the most important call-to-action (CTA) land
  in a naturally scanned spot (Z-pattern/Gutenberg diagram, see phase 4)?
  Does every section have one clear focal point instead of several equally
  loud elements? If not: sharpen the layout/hierarchy before release.
- **Only in landing-page mode — CRO check (hard, blocking):** check the
  above-the-fold area first and most thoroughly (see phase 4). Is the
  Value Equation fully present (dream outcome, visible social proof, risk
  reversal right at the CTA, a concrete timeframe, simple steps)? Is "how
  it works" at most 3-4 steps? Is social proof visual and not hidden in a
  carousel? If something's missing: fix it before release, don't defer it
  as "nice to have."
- **Suggest impeccable (before the final "done" verdict):** `/audit`
  (technical quality check, P0-P3) and right after it `/harden` (edge
  cases, i18n, error states) for the technical side; `/critique` for a
  scored design review; `/optimize` to complement the performance check
  above; `/distill` if the page still feels overloaded despite the value
  check; `/extract` if a reusable design system would make sense.
  `/polish` as the very last step, immediately before release. Suggest
  each command individually with a reason, don't run them all at once (see
  core rule).
- Summarize the result briefly for the user: what was checked, what works,
  what doesn't yet — not a raw findings list without context.

## Phase 7: Release

Goal: go live — in a controlled way, with confirmation at the critical
points.

- Before actually going live, briefly summarize what happens now (e.g.
  "the site will now be publicly reachable at this address").
- Deployment/domain/hosting steps that are visible to third parties or
  incur cost: always confirm first.

**Right after buying a domain — check three points:**
Once a custom domain exists (before the main site goes live), go through
these three points. The first two don't apply universally — only if the
project's situation calls for them; check briefly whether the condition
applies instead of doing it routinely.

1. **Host the app on a subdomain, separate from the main site — only for
   genuinely separate systems.** Only applies when two different things
   actually exist: a simple marketing/landing page (e.g. built with a
   static site generator) and a separate, more complex application (e.g.
   an app in a different framework/stack). For a single, unified
   site/app without this split: skip it, don't build an artificial
   separation. If it applies: separate the marketing/landing page
   (`yourdomain.com`) from the application (`app.yourdomain.com`). Why:
   design/copy changes on the homepage then can't break the core
   application — the environments are isolated. Implementation: add a
   CNAME record in DNS, name `app`, target = wherever the application is
   hosted. Changing DNS records is visible to third parties → confirm
   before creating it.
2. **Separate subdomains for outgoing email — only with a newsletter/
   multiple mail types.** Whether this is needed follows from the project
   planning (phase 2/4): does the project plan include a newsletter or
   marketing mailings in addition to transactional email like password
   resets/order confirmations? Only then do two distinct mail types even
   exist that need separating. If the site only sends one kind of email
   (e.g. only a contact form or only login), this point doesn't apply. If
   it applies: send transactional email via `mail.yourdomain.com` and
   marketing email via `news.yourdomain.com`. Why: if a marketing campaign
   lands in spam, the transactional domain's reputation stays clean —
   critical emails like invoices or login links keep arriving.
   Implementation: register both subdomains with an email provider and set
   SPF, DKIM, and DMARC DNS records for authentication.
3. **Ask Google to index the site — always.** Applies to every project
   without exception, once the main site is reachable under its own
   domain: generate `sitemap.xml` with all public URLs (this connects to
   the SEO-basics check in phase 6 — the sitemap is technically prepared
   there, here it's actively submitted to Google), submit it in Google
   Search Console, and trigger indexing of the pages. Why: without active
   submission, it can take weeks for Google to find the site on its own.

- Hard check before going live: legal notice + privacy policy present (see
  the "Legal" section)? If something's missing, point it out actively and
  don't release silently.
- **Only if analytics was requested (phase 0):** set up a
  privacy-friendly tool (e.g. one that doesn't rely on invasive tracking)
  — this feeds directly into the privacy policy.
- **Only for client projects — client sign-off:** the client actively
  confirms "this is fine" before the final release. Protects against
  disputes over the result or payment.
- **Only for client projects — credential handover:** hand over hosting/
  domain access cleanly and securely to the client (no plaintext in chat
  history or similar). Briefly explain which access the client needs now.
- After release: briefly check whether the live site actually works as
  expected (not just tested locally).
- **Suggest impeccable:** run `/document` again to bring `DESIGN.md` up to
  the final state — so later changes/new sessions know the grown design
  system.
- Add an entry to `CHANGELOG.md`: date + what was delivered, in 1-3 bullet
  points. No prose.

## Phase 8: Maintenance & support (client projects only)

Goal: clarity on what happens after go-live — otherwise unclear
expectations and unpaid extra work later.

- Briefly clarify: who handles future change requests, updates, bug fixes
  — a one-time payment or an ongoing arrangement (potential recurring
  revenue)?
- Write the result down briefly (e.g. a paragraph in `README.md` or its own
  `MAINTENANCE.md` if it gets more extensive).

## Landing-page mode only: testing cadence after release

Goal: conversion rate is never "done" — ongoing optimization beats buying
more traffic/ad spend (doubling conversion rate instead of doubling
traffic brings more revenue per visitor and allows higher bids in ad
auctions).

- **At high traffic (>40,000-50,000 visitors/month):** one focused split
  test per week, only on high-leverage elements (headline or hero image) —
  small but compounding wins.
- **At lower traffic (<20,000 visitors/month):** no micro-tests that take
  months to reach statistical significance. Instead, larger staged
  redesigns grounded in established CRO best practices (see phase 4)
  instead of waiting indefinitely on too-small samples.
- Only bring this up once there's actual ongoing traffic — usually not yet
  relevant right after release, better suited to a later maintenance
  conversation.

---

## Legal (jurisdiction-specific — the checklist below reflects German law;
adapt or replace it for wherever the site is legally targeted)

Goal: the site doesn't go live without these points being addressed —
fines are a real risk for the client/user, even for small one-person sites,
under German law (and many EU jurisdictions have comparable requirements).

- **Legal notice / "Impressum" (German law, § 5 DDG):** required for
  practically every commercial site under German law, even for sole
  proprietors — not just registered companies. Needs: name, a physical
  postal address (no PO box), email, and for corporations also the legal
  form/company register entry. Get these details exclusively from the
  user/client themselves — never invent or guess them.
- **Privacy policy (GDPR, applies EU-wide):** must document every actual
  data processing activity (server logs/hosting, contact form, newsletter,
  cookies/tracking, embedded services like web fonts, maps, analytics).
  Prepare the structure, fill in the actual services only once it's clear
  what the site actually embeds.
- **Cookie banner:** only needed if non-essential cookies/tracking are
  used. Declining must be exactly as easy as accepting — a plain "Accept"
  button alone is not legally sufficient under GDPR/ePrivacy.
- **Accessibility (e.g. Germany's BFSG, in effect since 2025-06-28, or
  equivalent local accessibility law):** mainly affects online shops and
  certain digital services aimed at consumers. For relevant projects,
  check during phase 3 (research) whether it applies, and draw the
  consequences for phase 4 (plan).

Important: this is not legal advice. This section exists so these building
blocks aren't forgotten — have the actual legal text double-checked by the
user (a lawyer, or a recognized generator/template for their jurisdiction)
when in doubt, and adapt the whole checklist to whatever country the site
is actually operating in.

---

## When it's unclear where the project currently stands

Ask briefly, or infer from context (git history, existing files, the last
conversation), and state it explicitly: "We're currently in phase X — the
next step is Y." Don't silently skip a phase.
