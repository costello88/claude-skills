# Claude Skills

De persoonlijke verzameling Claude-skills en -plugins van Cristoffe Jensch, op één plek.

**Inhoud:** 13 losse skills en 78 plugins (samen 396 skills).

## Indeling

- `skills/` — losse skills, elk in een eigen map met een `SKILL.md`
- `plugins/` — plugins; elke plugin heeft een map `skills/` en soms ook agents, commands en scripts
- `.claude-plugin/marketplace.json` — maakt van deze repo een plugin-marketplace, zodat je de plugins in Claude Code met één commando installeert

## Installatiehandleiding

Er zijn drie manieren, afhankelijk van waar je Claude gebruikt:

| Waar | Wat installeer je | Methode |
|---|---|---|
| Claude Code | Plugins | [A. Via de marketplace](#a-plugins-installeren-in-claude-code-via-de-marketplace) |
| Claude Code | Losse skills | [B. Kopiëren naar je skills-map](#b-losse-skills-installeren-in-claude-code) |
| claude.ai (web, desktop, mobiel) | Losse skills of één skill uit een plugin | [C. Uploaden als ZIP](#c-skills-uploaden-in-claudeai) |

### Voorbereiding

1. **Zorg dat je toegang hebt tot deze repo.** Hij is privé, dus je computer moet bij GitHub zijn ingelogd. Controleer dat met:
   ```bash
   git ls-remote https://github.com/costello88/claude-skills
   ```
   Zie je een lijst met regels (geen foutmelding)? Dan is het goed. Krijg je een fout, log dan in met `gh auth login` (GitHub CLI) of stel een SSH-sleutel in.
2. **Installeer Claude Code** (alleen nodig voor methode A en B) en controleer de versie:
   ```bash
   claude --version
   ```

### A. Plugins installeren in Claude Code via de marketplace

1. **Voeg de marketplace toe** (eenmalig). Typ in je terminal:
   ```bash
   claude plugin marketplace add costello88/claude-skills
   ```
   Je ziet: `Successfully added marketplace: costello88-skills`.
2. **Bekijk welke plugins er zijn.** Start Claude Code met `claude` en typ `/plugin`. Kies de marketplace **costello88-skills** om alle 78 plugins te zien.
3. **Installeer een plugin.** Gebruik de naam uit de lijst hieronder, bijvoorbeeld:
   ```bash
   claude plugin install linkedin-skills@costello88-skills
   ```
   Je ziet: `Successfully installed plugin: linkedin-skills@costello88-skills`.
4. **Herstart of herlaad.** Start een nieuwe sessie, of typ `/reload-plugins` in een lopende sessie.
5. **Controleer of het werkt:**
   ```bash
   claude plugin list
   ```
   De plugin staat erin met `Status: ✔ enabled`. Skills van een plugin roep je aan met de pluginnaam ervoor, bijvoorbeeld `/linkedin-skills:linkedin-post-writer`.
6. **Updates ophalen** nadat de repo is bijgewerkt:
   ```bash
   claude plugin marketplace update costello88-skills
   ```

Verwijderen kan met `claude plugin uninstall <naam>@costello88-skills`.

### B. Losse skills installeren in Claude Code

1. **Clone de repo:**
   ```bash
   git clone https://github.com/costello88/claude-skills.git
   cd claude-skills
   ```
2. **Kies het bereik:**
   - Voor al je projecten: `~/.claude/skills/`
   - Alleen voor één project: `.claude/skills/` in de map van dat project
3. **Kopieer de skills.** Alle losse skills tegelijk (macOS/Linux):
   ```bash
   mkdir -p ~/.claude/skills
   cp -R skills/* ~/.claude/skills/
   ```
   Of één skill, bijvoorbeeld:
   ```bash
   cp -R skills/animate ~/.claude/skills/
   ```
   Op Windows (PowerShell):
   ```powershell
   New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills"
   Copy-Item -Recurse skills\* "$env:USERPROFILE\.claude\skills\"
   ```
4. **Start Claude Code opnieuw.** De skills worden vanzelf gebruikt als je vraag erbij past, of je roept ze aan met `/<skillnaam>`, bijvoorbeeld `/animate`.

### C. Skills uploaden in claude.ai

claude.ai kent geen plugins, alleen losse skills. Je uploadt elke skill apart als ZIP.

1. **Zet code-uitvoering aan.** Ga in claude.ai naar **Settings → Capabilities** en zet *code execution and file creation* aan. Skills werken niet zonder.
2. **Maak een ZIP van de skillmap.** De ZIP moet de map zelf bevatten, en de mapnaam moet gelijk zijn aan de naam van de skill:
   ```bash
   cd skills
   zip -r animate.zip animate
   ```
   Een skill uit een plugin werkt hetzelfde, bijvoorbeeld:
   ```bash
   cd plugins/linkedin-skills/skills
   zip -r linkedin-post-writer.zip linkedin-post-writer
   ```
   Op Windows: klik met rechts op de map → **Comprimeren naar ZIP-bestand**.
3. **Upload.** Scroll in **Settings → Capabilities** naar **Skills** en klik op **Upload skill**. Kies je ZIP.
4. **Zet de skill aan.** De skill verschijnt in je lijst; zet de schakelaar aan.

Let op: skills die afhankelijk zijn van agents, hooks of MCP-servers van hun plugin werken in claude.ai mogelijk niet volledig. Gebruik die via Claude Code (methode A).

### Problemen oplossen

| Melding | Oplossing |
|---|---|
| `Repository not found` of `Authentication failed` bij het toevoegen | Je bent niet ingelogd bij GitHub. Voer `gh auth login` uit en probeer opnieuw. |
| `Plugin "…" not found in marketplace` | Gebruik exact de naam uit de tabel hieronder. Let op: *self-improving-agent* heet `si`. |
| Skill verschijnt niet in Claude Code | Start een nieuwe sessie of typ `/reload-plugins`. Controleer dat de map een `SKILL.md` bevat. |
| Upload in claude.ai mislukt | Controleer dat de ZIP de map bevat (niet los de bestanden) en dat de mapnaam gelijk is aan de skillnaam. |

## Licenties

Plugins van derden houden hun eigen licentie (zie de `LICENSE` of `README` in elke plugin). Deze repo is een persoonlijke back-up: controleer de licentie voordat je een plugin opnieuw publiceert.

## Overzicht van alle skills

De beschrijvingen staan in het Engels, net als de skills zelf: Claude gebruikt die tekst om te bepalen wanneer een skill van toepassing is.

### Losse skills (13)

| Skill | Wat het doet |
|---|---|
| [animate](skills/animate) | Build an animation from scratch, making the decisions in the order that determines whether it feels right — should it animate at all, what purpose, which tool,… |
| [animation-vocabulary](skills/animation-vocabulary) | Reverse-lookup glossary that turns a vague description of a web animation or motion effect into its exact term ("the bouncy thing when a popover opens" → Pop… |
| [apple-design](skills/apple-design) | Cross-platform UI/UX design reviewer grounded in Apple Human Interface Guidelines principles. Use this skill to audit, review, critique, or improve any UI/UX… |
| [brainstorming](skills/brainstorming) | You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent,… |
| [dispatching-parallel-agents](skills/dispatching-parallel-agents) | Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies |
| [executing-plans](skills/executing-plans) | Use when you have a written implementation plan to execute in a separate session with review checkpoints |
| [improve-animations](skills/improve-animations) | Survey a codebase's animation and motion code as a senior motion advisor, then produce a prioritized audit and self-contained implementation plans for other… |
| [pick-ui-library](skills/pick-ui-library) | Pick the right library for a given frontend task from a curated, opinionated list — numbers, OTP inputs, charts, command menus, virtualization, drag and drop,… |
| [prototype](skills/prototype) | Build multiple genuinely different versions of a UI piece you describe, rendered behind a visual picker so you can flip through them live and promote the one… |
| [receiving-code-review](skills/receiving-code-review) | Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical… |
| [review-animations](skills/review-animations) | Reviews animation and motion code against a high craft bar derived from Emil Kowalski's design engineering philosophy. Default to flagging; approval is earned. |
| [subagent-driven-development](skills/subagent-driven-development) | Use when executing implementation plans with independent tasks in the current session |
| [writing-plans](skills/writing-plans) | Use when you have a spec or requirements for a multi-step task, before touching code |

### Plugins (78)

Installeren: `claude plugin install <installatienaam>@costello88-skills`

<details><summary><b>a11y-audit</b> — installatienaam <code>a11y-audit</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [a11y-audit](plugins/a11y-audit/skills/a11y-audit) | Accessibility audit skill for scanning, fixing, and verifying WCAG 2.2 Level A and AA compliance across React, Next.js, Vue, Angular, Svelte, and plain HTML… |

</details>

<details><summary><b>agenthub</b> — installatienaam <code>agenthub</code>, 8 skills</summary>

| Skill | Wat het doet |
|---|---|
| [agenthub](plugins/agenthub/skills/agenthub) | Multi-agent collaboration plugin that spawns N parallel subagents competing on the same task via git worktree isolation. Agents work independently, results are… |
| [board](plugins/agenthub/skills/board) | Read, write, and browse the AgentHub message board for agent coordination. |
| [eval](plugins/agenthub/skills/eval) | Evaluate and rank agent results by metric or LLM judge for an AgentHub session. |
| [init](plugins/agenthub/skills/init) | Create a new AgentHub collaboration session with task, agent count, and evaluation criteria. |
| [merge](plugins/agenthub/skills/merge) | Merge the winning agent's branch into base, archive losers, and clean up worktrees. |
| [run](plugins/agenthub/skills/run) | One-shot lifecycle command that chains init → baseline → spawn → eval → merge in a single invocation. |
| [spawn](plugins/agenthub/skills/spawn) | Launch N parallel subagents in isolated git worktrees to compete on the session task. |
| [status](plugins/agenthub/skills/status) | Show DAG state, agent progress, and branch status for an AgentHub session. |

</details>

<details><summary><b>agile-product-owner</b> — installatienaam <code>agile-product-owner</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [agile-product-owner](plugins/agile-product-owner/skills/agile-product-owner) | Agile product ownership for backlog management and sprint execution. Covers user story writing, acceptance criteria, sprint planning, and velocity tracking.… |

</details>

<details><summary><b>apple-hig-expert</b> — installatienaam <code>apple-hig-expert</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [apple-hig-expert](plugins/apple-hig-expert/skills/apple-hig-expert) | Expert guidance on Apple Human Interface Guidelines (HIG). Covers iOS, macOS, and visionOS with 2026 Liquid Glass aesthetics and accessibility-first design. |

</details>

<details><summary><b>autoresearch-agent</b> — installatienaam <code>autoresearch-agent</code>, 6 skills</summary>

| Skill | Wat het doet |
|---|---|
| [autoresearch-agent](plugins/autoresearch-agent/skills/autoresearch-agent) | Autonomous experiment loop that optimizes any file by a measurable metric. Inspired by Karpathy's autoresearch. The agent edits a target file, runs a fixed… |
| [loop](plugins/autoresearch-agent/skills/loop) | Start an autonomous experiment loop with user-selected interval (10min, 1h, daily, weekly, monthly). Uses CronCreate for scheduling. |
| [resume](plugins/autoresearch-agent/skills/resume) | Resume a paused experiment. Checkout the experiment branch, read results history, continue iterating. |
| [run](plugins/autoresearch-agent/skills/run) | Run a single experiment iteration. Edit the target file, evaluate, keep or discard. |
| [setup](plugins/autoresearch-agent/skills/setup) | Set up a new autoresearch experiment interactively. Collects domain, target file, eval command, metric, direction, and evaluator. |
| [status](plugins/autoresearch-agent/skills/status) | Show experiment dashboard with results, active loops, and progress. |

</details>

<details><summary><b>brag</b> — installatienaam <code>brag</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [brag](plugins/brag/skills/brag) | Turn the current project website into a short, polished, shareable launch video using Hyperframes. Use when someone says "/brag", "let's brag about this",… |

</details>

<details><summary><b>business-growth-skills</b> — installatienaam <code>business-growth-skills</code>, 5 skills</summary>

| Skill | Wat het doet |
|---|---|
| [business-growth-skills](plugins/business-growth-skills/skills/business-growth-skills) | 4 business growth agent skills and plugins for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw. Customer success (health scoring, churn), sales engineer… |
| [contract-and-proposal-writer](plugins/business-growth-skills/skills/contract-and-proposal-writer) | Contract & Proposal Writer |
| [customer-success-manager](plugins/business-growth-skills/skills/customer-success-manager) | Monitors customer health, predicts churn risk, and identifies expansion opportunities using weighted scoring models for SaaS customer success. Use when… |
| [revenue-operations](plugins/business-growth-skills/skills/revenue-operations) | Analyzes sales pipeline health, revenue forecasting accuracy, and go-to-market efficiency metrics for SaaS revenue optimization. Use when analyzing sales… |
| [sales-engineer](plugins/business-growth-skills/skills/sales-engineer) | Analyzes RFP/RFI responses for coverage gaps, builds competitive feature comparison matrices, and plans proof-of-concept (POC) engagements for pre-sales… |

</details>

<details><summary><b>c-level-agents</b> — installatienaam <code>c-level-agents</code>, 20 skills</summary>

| Skill | Wat het doet |
|---|---|
| [boardroom](plugins/c-level-agents/skills/boardroom) | /cs:boardroom <brief> — 6-phase multi-role deliberation across the C-suite with Phase 2 isolation, critic pre-screen, and synthesis. Outputs a board memo. |
| [brief](plugins/c-level-agents/skills/brief) | /cs:brief <topic> — Generate a one-page strategy brief from an office-hours intake. First step in the strategic sprint pipeline. |
| [c-level-agents](plugins/c-level-agents/skills/c-level-agents) | Founder-mode executive team. 8 cs-* C-suite agents (CFO, CMO, CRO, CPO, COO, CHRO, CISO, Chief of Staff) and 17 /cs:* slash commands for forcing-question… |
| [caio-review](plugins/c-level-agents/skills/caio-review) | /cs:caio-review <plan> — Eval-demanding Chief AI Officer interrogation of any plan that involves AI: model selection, risk classification, cost economics, or… |
| [cdo-review](plugins/c-level-agents/skills/cdo-review) | /cs:cdo-review <plan> — Decision-driven Chief Data Officer interrogation of any plan that touches training data, data architecture, data productization, or… |
| [cfo-review](plugins/c-level-agents/skills/cfo-review) | /cs:cfo-review <plan> — Numerate-skeptic interrogation of any plan that touches money. Unit economics, runway, dilution, capital allocation. |
| [ciso-review](plugins/c-level-agents/skills/ciso-review) | /cs:ciso-review <plan> — Risk-paranoid interrogation of any plan that touches data, compliance, or production access. |
| [cmo-review](plugins/c-level-agents/skills/cmo-review) | /cs:cmo-review <plan> — Narrative-first interrogation of positioning, ICP, message house, and channel mix. |
| [cpo-review](plugins/c-level-agents/skills/cpo-review) | /cs:cpo-review <plan> — JTBD-driven interrogation of product roadmap, PMF signal, and portfolio focus. |
| [cro-review](plugins/c-level-agents/skills/cro-review) | /cs:cro-review <plan> — Pipeline-paranoid interrogation of revenue, win rate, NRR, and ramp time. |
| [cross-eval](plugins/c-level-agents/skills/cross-eval) | /cs:cross-eval <memo> — Multi-model consensus on a board memo or strategy brief. Claude + Codex + Gemini cross-review with graceful degradation. |
| [cto-review](plugins/c-level-agents/skills/cto-review) | /cs:cto-review <plan> — Architecture and scaling interrogation. Tech debt, scaling cliffs, team scaling, build-vs-buy. |
| [decide](plugins/c-level-agents/skills/decide) | /cs:decide <memo> — Log a decision to two-layer memory via decision-logger. Approved memo becomes durable; raw transcripts kept for reference. |
| [execute](plugins/c-level-agents/skills/execute) | /cs:execute <decision> — Generate a 90-day execution plan with weekly milestones, DRIs, and check-in cadence from an approved decision. |
| [founder-mode](plugins/c-level-agents/skills/founder-mode) | /cs:founder-mode <question> — Auto-routes any founder question to the right C-role advisor or to /cs:boardroom for multi-role topics. The single-command entry… |
| [freeze](plugins/c-level-agents/skills/freeze) | /cs:freeze <decision> <days> — Lock a strategic decision for a cooldown period to prevent impulse reversal. Mirrors gstack's safety primitives for the business… |
| [gc-review](plugins/c-level-agents/skills/gc-review) | /cs:gc-review <plan> — General Counsel interrogation of contracts, IP, regulatory, term sheets, and employment-law surface. |
| [office-hours](plugins/c-level-agents/skills/office-hours) | /cs:office-hours <topic> — YC-style 6-question founder interrogation before any advice. Forces clarity on problem, customer, distribution, defensibility,… |
| [onboard](plugins/c-level-agents/skills/onboard) | /cs:onboard — Founder interview that populates ~/.claude/company-context.md. The first command to run when starting with c-level-agents. |
| [post-mortem](plugins/c-level-agents/skills/post-mortem) | /cs:post-mortem <decision> — Honest retrospective on an executed decision, scored against original assumptions and dissent. Closes the strategic sprint loop. |

</details>

<details><summary><b>chaos-engineering</b> — installatienaam <code>chaos-engineering</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [chaos-engineering](plugins/chaos-engineering/skills/chaos-engineering) | Use when planning, running, or learning from chaos engineering experiments. Triggers on "chaos experiment", "fault injection", "gameday", "resilience test",… |

</details>

<details><summary><b>chief-ai-officer-advisor</b> — installatienaam <code>chief-ai-officer-advisor</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [chief-ai-officer-advisor](plugins/chief-ai-officer-advisor/skills/chief-ai-officer-advisor) | Chief AI Officer advisory for startups: model build-vs-buy decisions (API vs fine-tune vs in-house), AI risk classification under EU AI Act + US state… |

</details>

<details><summary><b>chief-data-officer-advisor</b> — installatienaam <code>chief-data-officer-advisor</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [chief-data-officer-advisor](plugins/chief-data-officer-advisor/skills/chief-data-officer-advisor) | Chief Data Officer advisory for startups: AI training data rights and consent provenance, data product strategy (warehouse vs lakehouse vs mesh, build-vs-buy),… |

</details>

<details><summary><b>code-to-prd</b> — installatienaam <code>code-to-prd</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [code-to-prd](plugins/code-to-prd/skills/code-to-prd) | Reverse-engineer any codebase into a complete Product Requirements Document (PRD). Analyzes routes, components, state management, API integrations, and user… |

</details>

<details><summary><b>code-tour</b> — installatienaam <code>code-tour</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [code-tour](plugins/code-tour/skills/code-tour) | Use when the user asks to create a CodeTour .tour file — persona-targeted, step-by-step walkthroughs that link to real files and line numbers. Trigger for:… |

</details>

<details><summary><b>codebase-mapper</b> — installatienaam <code>codebase-mapper</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [map-codebase](plugins/codebase-mapper/skills/map-codebase) | Create a self-maintaining codebase map in .claude/.codebase-info/. Use to map, document, analyze, or onboard a codebase, including a new project. |
| [update-codebase-map](plugins/codebase-mapper/skills/update-codebase-map) | Refresh an existing .claude/.codebase-info/ map after code changes. Use for stale codebase or architecture docs; use map-codebase to create one. |

</details>

<details><summary><b>data-quality-auditor</b> — installatienaam <code>data-quality-auditor</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [data-quality-auditor](plugins/data-quality-auditor/skills/data-quality-auditor) | Audit datasets for completeness, consistency, accuracy, and validity. Profile data distributions, detect anomalies and outliers, surface structural issues, and… |

</details>

<details><summary><b>demo-video</b> — installatienaam <code>demo-video</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [demo-video](plugins/demo-video/skills/demo-video) | Use when the user asks to create a demo video, product walkthrough, feature showcase, animated presentation, marketing video, or GIF from screenshots or scene… |

</details>

<details><summary><b>design</b> — installatienaam <code>design</code>, 7 skills</summary>

| Skill | Wat het doet |
|---|---|
| [accessibility-review](plugins/design/skills/accessibility-review) | Run a WCAG 2.1 AA accessibility audit on a design or page. Trigger with "audit accessibility", "check a11y", "is this accessible?", or when reviewing a design… |
| [design-critique](plugins/design/skills/design-critique) | Get structured design feedback on usability, hierarchy, and consistency. Trigger with "review this design", "critique this mockup", "what do you think of this… |
| [design-handoff](plugins/design/skills/design-handoff) | Generate developer handoff specs from a design. Use when a design is ready for engineering and needs a spec sheet covering layout, design tokens, component… |
| [design-system](plugins/design/skills/design-system) | Audit, document, or extend your design system. Use when checking for naming inconsistencies or hardcoded values across components, writing documentation for a… |
| [research-synthesis](plugins/design/skills/research-synthesis) | Synthesize user research into themes, insights, and recommendations. Use when you have interview transcripts, survey results, usability test notes, support… |
| [user-research](plugins/design/skills/user-research) | Plan, conduct, and synthesize user research. Trigger with "user research plan", "interview guide", "usability test", "survey design", "research questions", or… |
| [ux-copy](plugins/design/skills/ux-copy) | Write or review UX copy — microcopy, error messages, empty states, CTAs. Trigger with "write copy for", "what should this button say?", "review this error… |

</details>

<details><summary><b>docker-development</b> — installatienaam <code>docker-development</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [docker-development](plugins/docker-development/skills/docker-development) | Docker and container development agent skill and plugin for Dockerfile optimization, docker-compose orchestration, multi-stage builds, and container security… |

</details>

<details><summary><b>engineering</b> — installatienaam <code>engineering</code>, 10 skills</summary>

| Skill | Wat het doet |
|---|---|
| [architecture](plugins/engineering/skills/architecture) | Create or evaluate an architecture decision record (ADR). Use when choosing between technologies (e.g., Kafka vs SQS), documenting a design decision with… |
| [code-review](plugins/engineering/skills/code-review) | Review code changes for security, performance, and correctness. Trigger with a PR URL or diff, "review this before I merge", "is this code safe?", or when… |
| [debug](plugins/engineering/skills/debug) | Structured debugging session — reproduce, isolate, diagnose, and fix. Trigger with an error message or stack trace, "this works in staging but not prod",… |
| [deploy-checklist](plugins/engineering/skills/deploy-checklist) | Pre-deployment verification checklist. Use when about to ship a release, deploying a change with database migrations or feature flags, verifying CI status and… |
| [documentation](plugins/engineering/skills/documentation) | Write and maintain technical documentation. Trigger with "write docs for", "document this", "create a README", "write a runbook", "onboarding guide", or when… |
| [incident-response](plugins/engineering/skills/incident-response) | Run an incident response workflow — triage, communicate, and write postmortem. Trigger with "we have an incident", "production is down", an alert that needs… |
| [standup](plugins/engineering/skills/standup) | Generate a standup update from recent activity. Use when preparing for daily standup, summarizing yesterday's commits and PRs and ticket moves, formatting work… |
| [system-design](plugins/engineering/skills/system-design) | Design systems, services, and architectures. Trigger with "design a system for", "how should we architect", "system design for", "what's the right architecture… |
| [tech-debt](plugins/engineering/skills/tech-debt) | Identify, categorize, and prioritize technical debt. Trigger with "tech debt", "technical debt audit", "what should we refactor", "code health", or when the… |
| [testing-strategy](plugins/engineering/skills/testing-strategy) | Design test strategies and test plans. Trigger with "how should we test", "test strategy for", "write tests for", "test plan", "what tests do we need", or when… |

</details>

<details><summary><b>exa</b> — installatienaam <code>exa</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [exa-agent](plugins/exa/skills/exa-agent) | Use Exa Agent for multi-step web research, list-building, enrichment, structured output, run continuation, and coverage validation. Exa Agent can access… |
| [search](plugins/exa/skills/search) | Deep research powered by Exa. Use for lead generation, literature reviews, deep dives, competitive analysis, or any query where one search falls short,… |

</details>

<details><summary><b>executive-mentor</b> — installatienaam <code>executive-mentor</code>, 6 skills</summary>

| Skill | Wat het doet |
|---|---|
| [board-prep](plugins/executive-mentor/skills/board-prep) | /em -board-prep — Board Meeting Preparation |
| [challenge](plugins/executive-mentor/skills/challenge) | /em -challenge — Pre-Mortem Plan Analysis |
| [executive-mentor](plugins/executive-mentor/skills/executive-mentor) | Adversarial thinking partner for founders and executives. Stress-tests plans, prepares for brutal board meetings, dissects decisions with no good options, and… |
| [hard-call](plugins/executive-mentor/skills/hard-call) | /em -hard-call — Framework for Decisions With No Good Options |
| [postmortem](plugins/executive-mentor/skills/postmortem) | /em -postmortem — Honest Analysis of What Went Wrong |
| [stress-test](plugins/executive-mentor/skills/stress-test) | /em -stress-test — Business Assumption Stress Testing |

</details>

<details><summary><b>feature-flags-architect</b> — installatienaam <code>feature-flags-architect</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [feature-flags-architect](plugins/feature-flags-architect/skills/feature-flags-architect) | Use when adding, retiring, or auditing feature flags. Triggers on "add a flag", "ship behind a flag", "rollout plan", "kill switch", "stale flags", "flag… |

</details>

<details><summary><b>general-counsel-advisor</b> — installatienaam <code>general-counsel-advisor</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [general-counsel-advisor](plugins/general-counsel-advisor/skills/general-counsel-advisor) | General Counsel advisory for startups: contract review (MSA, SaaS, NDA, DPA, employment), IP strategy, term sheet decoding, and regulatory landscape mapping.… |

</details>

<details><summary><b>google-workspace-cli</b> — installatienaam <code>google-workspace-cli</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [google-workspace-cli](plugins/google-workspace-cli/skills/google-workspace-cli) | Google Workspace administration via the gws CLI. Install, authenticate, and automate Gmail, Drive, Sheets, Calendar, Docs, Chat, and Tasks. Run security… |

</details>

<details><summary><b>helm-chart-builder</b> — installatienaam <code>helm-chart-builder</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [helm-chart-builder](plugins/helm-chart-builder/skills/helm-chart-builder) | Helm chart development agent skill and plugin for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw — chart scaffolding, values design, template patterns,… |

</details>

<details><summary><b>karpathy-coder</b> — installatienaam <code>karpathy-coder</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [karpathy-coder](plugins/karpathy-coder/skills/karpathy-coder) | Use when writing, reviewing, or committing code to enforce Karpathy's 4 coding principles — surface assumptions before coding, keep it simple, make surgical… |

</details>

<details><summary><b>kubernetes-operator</b> — installatienaam <code>kubernetes-operator</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [kubernetes-operator](plugins/kubernetes-operator/skills/kubernetes-operator) | Use when building a Kubernetes Operator — custom controllers that reconcile CRD state. Triggers on "build an operator", "CRD design", "reconcile loop",… |

</details>

<details><summary><b>linkedin-skills</b> — installatienaam <code>linkedin-skills</code>, 13 skills</summary>

| Skill | Wat het doet |
|---|---|
| [linkedin-marketing](plugins/linkedin-skills) | Plan, draft, audit, and publish LinkedIn posts and comments. Use when the user wants to write a viral LinkedIn post, draft a comment or reply on any LinkedIn… |
| [linkedin-comment-drafter](plugins/linkedin-skills/skills/linkedin-comment-drafter) | Draft a LinkedIn comment on someone else's post from its URL, or reshare (repost) it to your feed with optional commentary. Use when the user pastes a post URL… |
| [linkedin-content-planner](plugins/linkedin-skills/skills/linkedin-content-planner) | Generate a 7-day LinkedIn content plan from a theme, audience, and pillars. Produces per-day post pillar, format, hook type, CTA, posting time, daily comment… |
| [linkedin-employee-advocacy](plugins/linkedin-skills/skills/linkedin-employee-advocacy) | Stand up and run a LinkedIn employee advocacy program for a marketing or sales team. Covers 14-day launch playbook, brand-guideline governance, per-post time… |
| [linkedin-engager-analytics](plugins/linkedin-skills/skills/linkedin-engager-analytics) | Pull the people who liked or commented on any LinkedIn post and segment them by ICP fit (peer / aspirational / prospect / other). Produces an engager roster,… |
| [linkedin-hook-extractor](plugins/linkedin-skills/skills/linkedin-hook-extractor) | Reverse-engineer the hook formula from a viral LinkedIn post URL. Returns which of the 20 canonical 2026 formulas it uses (anaphora, R.I.P., year-pivot,… |
| [linkedin-humanizer](plugins/linkedin-skills/skills/linkedin-humanizer) | Remove AI tells from LinkedIn posts/comments: 2026 vocabulary density, reveal bridges, staccato fragments, stacked triads, performed sincerity. Tiered rewriter… |
| [linkedin-interviewer](plugins/linkedin-skills/skills/linkedin-interviewer) | Interview the user for the raw material their posts are made of. Builds a lasting Story Bank of roles, numbers, turning points, scars and positions, or runs a… |
| [linkedin-post-writer](plugins/linkedin-skills/skills/linkedin-post-writer) | Draft a new LinkedIn post from scratch using one of 20 2026 hook formulas (anaphora, R.I.P., time-anchor, curiosity-gap, contrarian, controlled A/B,… |
| [linkedin-profile-optimizer](plugins/linkedin-skills/skills/linkedin-profile-optimizer) | Audit and rewrite a LinkedIn profile end-to-end for 2026: headline, About 7-step, Featured, banner, photo, Experience metrics, Skills, custom URL,… |
| [linkedin-reply-handler](plugins/linkedin-skills/skills/linkedin-reply-handler) | Draft a reply to one LinkedIn comment from its URL, or sweep a whole thread from just the post URL and draft a reply to every comment worth answering, in one… |
| [linkedin-repurposer](plugins/linkedin-skills/skills/linkedin-repurposer) | Repurpose existing content into a native LinkedIn post. Take a tweet, thread, YouTube video, blog, or newsletter and rebuild it for LinkedIn: re-hook before… |
| [linkedin-thread-monitor](plugins/linkedin-skills/skills/linkedin-thread-monitor) | Track which of your LinkedIn comments earned author replies. Flags the 6-24h warm-reply window where thread momentum peaks, classifies threads as… |

</details>

<details><summary><b>live-rules</b> — installatienaam <code>live-rules</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [add-rule](plugins/live-rules/skills/add-rule) | Create or edit a live-rules instruction in the project's atomic rule set. Use to add a rule, coding guideline, guardrail, convention, or automatic reminder. |
| [manage-rules](plugins/live-rules/skills/manage-rules) | Inspect, audit, enable, or disable project live-rules. Use to list rules, check active instructions, explain an injected rule, or recover an atomic manifest. |

</details>

<details><summary><b>llm-wiki</b> — installatienaam <code>llm-wiki</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [llm-wiki](plugins/llm-wiki/skills/llm-wiki) | Use when building or maintaining a persistent personal knowledge base (second brain) in Obsidian where an LLM incrementally ingests sources, updates… |

</details>

<details><summary><b>marketing</b> — installatienaam <code>marketing</code>, 8 skills</summary>

| Skill | Wat het doet |
|---|---|
| [brand-review](plugins/marketing/skills/brand-review) | Review content against your brand voice, style guide, and messaging pillars, flagging deviations by severity with specific before/after fixes. Use when… |
| [campaign-plan](plugins/marketing/skills/campaign-plan) | Generate a full campaign brief with objectives, audience, messaging, channel strategy, content calendar, and success metrics. Use when planning a product… |
| [competitive-brief](plugins/marketing/skills/competitive-brief) | Research competitors and generate a positioning and messaging comparison with content gaps, opportunities, and threats. Use when building sales battlecards,… |
| [content-creation](plugins/marketing/skills/content-creation) | Draft marketing content across channels — blog posts, social media, email newsletters, landing pages, press releases, and case studies. Use when writing any… |
| [draft-content](plugins/marketing/skills/draft-content) | Draft blog posts, social media, email newsletters, landing pages, press releases, and case studies with channel-specific formatting and SEO recommendations.… |
| [email-sequence](plugins/marketing/skills/email-sequence) | Design and draft multi-email sequences with full copy, timing, branching logic, exit conditions, and performance benchmarks. Use when building onboarding, lead… |
| [performance-report](plugins/marketing/skills/performance-report) | Build a marketing performance report with key metrics, trend analysis, wins and misses, and prioritized optimization recommendations. Use when wrapping a… |
| [seo-audit](plugins/marketing/skills/seo-audit) | Run a comprehensive SEO audit — keyword research, on-page analysis, content gaps, technical checks, and competitor comparison. Use when assessing a site's SEO… |

</details>

<details><summary><b>pdf-viewer</b> — installatienaam <code>pdf-viewer</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [view-pdf](plugins/pdf-viewer/skills/view-pdf) | Interactive PDF viewer. Use when the user wants to open, show, or view a PDF and collaborate on it visually — annotate, highlight, stamp, fill form fields,… |

</details>

<details><summary><b>pm-skills</b> — installatienaam <code>pm-skills</code>, 9 skills</summary>

| Skill | Wat het doet |
|---|---|
| [atlassian-admin](plugins/pm-skills/skills/atlassian-admin) | Atlassian Administrator for managing and organizing Atlassian products (Jira, Confluence, Bitbucket, Trello), users, permissions, security, integrations,… |
| [atlassian-templates](plugins/pm-skills/skills/atlassian-templates) | Atlassian Template and Files Creator/Modifier expert for creating, modifying, and managing Jira and Confluence templates, blueprints, custom layouts, reusable… |
| [confluence-expert](plugins/pm-skills/skills/confluence-expert) | Atlassian Confluence expert for creating and managing spaces, knowledge bases, and documentation. Configures space permissions and hierarchies, creates page… |
| [jira-expert](plugins/pm-skills/skills/jira-expert) | Atlassian Jira expert for creating and managing projects, planning, product discovery, JQL queries, workflows, custom fields, automation, reporting, and all… |
| [meeting-analyzer](plugins/pm-skills/skills/meeting-analyzer) | Analyzes meeting transcripts and recordings to surface behavioral patterns, communication anti-patterns, and actionable coaching feedback. Use this skill… |
| [pm-skills](plugins/pm-skills/skills/pm-skills) | 6 project management agent skills and plugins for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw. Senior PM, scrum master, Jira expert (JQL), Confluence… |
| [scrum-master](plugins/pm-skills/skills/scrum-master) | Advanced Scrum Master skill for data-driven agile team analysis and coaching. Use when the user asks about sprint planning, velocity tracking, retrospectives,… |
| [senior-pm](plugins/pm-skills/skills/senior-pm) | Senior Project Manager for enterprise software, SaaS, and digital transformation projects. Specializes in portfolio management, quantitative risk analysis,… |
| [team-communications](plugins/pm-skills/skills/team-communications) | Write internal company communications — 3P updates (Progress/Plans/Problems), company-wide newsletters, FAQ roundups, incident reports, leadership updates,… |

</details>

<details><summary><b>product-management</b> — installatienaam <code>product-management</code>, 8 skills</summary>

| Skill | Wat het doet |
|---|---|
| [competitive-brief](plugins/product-management/skills/competitive-brief) | Create a competitive analysis brief for one or more competitors or a feature area. Use when informing product strategy or feature prioritization, building… |
| [metrics-review](plugins/product-management/skills/metrics-review) | Review and analyze product metrics with trend analysis and actionable insights. Use when running a weekly, monthly, or quarterly metrics review, investigating… |
| [product-brainstorming](plugins/product-management/skills/product-brainstorming) | Brainstorm product ideas, explore problem spaces, and challenge assumptions as a thinking partner. Use when exploring a new opportunity, generating solutions… |
| [roadmap-update](plugins/product-management/skills/roadmap-update) | Update, create, or reprioritize your product roadmap. Use when adding a new initiative and deciding what moves to make room, shifting priorities after new… |
| [sprint-planning](plugins/product-management/skills/sprint-planning) | Plan a sprint — scope work, estimate capacity, set goals, and draft a sprint plan. Use when kicking off a new sprint, sizing a backlog against team… |
| [stakeholder-update](plugins/product-management/skills/stakeholder-update) | Generate a stakeholder update tailored to audience and cadence. Use when writing a weekly or monthly status for leadership, announcing a launch, escalating a… |
| [synthesize-research](plugins/product-management/skills/synthesize-research) | Synthesize user research from interviews, surveys, and feedback into structured insights. Use when you have a pile of interview notes, survey responses, or… |
| [write-spec](plugins/product-management/skills/write-spec) | Write a feature spec or PRD from a problem statement or feature idea. Use when turning a vague idea or user request into a structured document, scoping a… |

</details>

<details><summary><b>pw</b> — installatienaam <code>pw</code>, 10 skills</summary>

| Skill | Wat het doet |
|---|---|
| [browserstack](plugins/pw/skills/browserstack) | Run tests on BrowserStack. Use when user mentions "browserstack", "cross-browser", "cloud testing", "browser matrix", "test on safari", "test on firefox", or… |
| [coverage](plugins/pw/skills/coverage) | Analyze test coverage gaps. Use when user says "test coverage", "what's not tested", "coverage gaps", "missing tests", "coverage report", or "what needs… |
| [fix](plugins/pw/skills/fix) | Fix failing or flaky Playwright tests. Use when user says "fix test", "flaky test", "test failing", "debug test", "test broken", "test passes sometimes", or… |
| [generate](plugins/pw/skills/generate) | Generate Playwright tests. Use when user says "write tests", "generate tests", "add tests for", "test this component", "e2e test", "create test for", "test… |
| [init](plugins/pw/skills/init) | Set up Playwright in a project. Use when user says "set up playwright", "add e2e tests", "configure playwright", "testing setup", "init playwright", or "add… |
| [migrate](plugins/pw/skills/migrate) | Migrate from Cypress or Selenium to Playwright. Use when user mentions "cypress", "selenium", "migrate tests", "convert tests", "switch to playwright", "move… |
| [playwright-pro](plugins/pw/skills/pw) | Production-grade Playwright testing toolkit. Use when the user mentions Playwright tests, end-to-end testing, browser automation, fixing flaky tests, test… |
| [report](plugins/pw/skills/report) | Generate test report. Use when user says "test report", "results summary", "test status", "show results", "test dashboard", or "how did tests go". |
| [review](plugins/pw/skills/review) | Review Playwright tests for quality. Use when user says "review tests", "check test quality", "audit tests", "improve tests", "test code review", or… |
| [testrail](plugins/pw/skills/testrail) | Sync tests with TestRail. Use when user mentions "testrail", "test management", "test cases", "test run", "sync test cases", "push results to testrail", or… |

</details>

<details><summary><b>ra-qm-skills</b> — installatienaam <code>ra-qm-skills</code>, 14 skills</summary>

| Skill | Wat het doet |
|---|---|
| [capa-officer](plugins/ra-qm-skills/skills/capa-officer) | CAPA system management for medical device QMS. Covers root cause analysis, corrective action planning, effectiveness verification, and CAPA metrics. Use for… |
| [fda-consultant-specialist](plugins/ra-qm-skills/skills/fda-consultant-specialist) | FDA regulatory consultant for medical device companies. Provides 510(k)/PMA/De Novo pathway guidance, QSR (21 CFR 820) compliance, HIPAA assessments, and… |
| [gdpr-dsgvo-expert](plugins/ra-qm-skills/skills/gdpr-dsgvo-expert) | GDPR and German DSGVO compliance automation. Scans codebases for privacy risks, generates DPIA documentation, tracks data subject rights requests. Use for GDPR… |
| [information-security-manager-iso27001](plugins/ra-qm-skills/skills/information-security-manager-iso27001) | ISO 27001 ISMS implementation and cybersecurity governance for HealthTech and MedTech companies. Use for ISMS design, security risk assessment, control… |
| [isms-audit-expert](plugins/ra-qm-skills/skills/isms-audit-expert) | Information Security Management System (ISMS) audit expert for ISO 27001 compliance verification, security control assessment, and certification support. Use… |
| [mdr-745-specialist](plugins/ra-qm-skills/skills/mdr-745-specialist) | EU MDR 2017/745 compliance specialist for medical device classification, technical documentation, clinical evidence, and post-market surveillance. Covers Annex… |
| [qms-audit-expert](plugins/ra-qm-skills/skills/qms-audit-expert) | ISO 13485 internal audit expertise for medical device QMS. Covers audit planning, execution, nonconformity classification, and CAPA verification. Use for… |
| [quality-documentation-manager](plugins/ra-qm-skills/skills/quality-documentation-manager) | Document control system management for medical device QMS. Covers document numbering, version control, change management, and 21 CFR Part 11 compliance. Use… |
| [quality-manager-qmr](plugins/ra-qm-skills/skills/quality-manager-qmr) | Senior Quality Manager Responsible Person (QMR) for HealthTech and MedTech companies. Provides quality system governance, management review leadership,… |
| [quality-manager-qms-iso13485](plugins/ra-qm-skills/skills/quality-manager-qms-iso13485) | ISO 13485 Quality Management System implementation and maintenance for medical device organizations. Provides QMS design, documentation control, internal… |
| [ra-qm-skills](plugins/ra-qm-skills/skills/ra-qm-skills) | 12 regulatory & QM agent skills and plugins for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw. ISO 13485 QMS, MDR 2017/745, FDA 510(k)/PMA, ISO 27001 ISMS,… |
| [regulatory-affairs-head](plugins/ra-qm-skills/skills/regulatory-affairs-head) | Senior Regulatory Affairs Manager for HealthTech and MedTech companies. Prepares FDA 510(k), De Novo, and PMA submission packages; analyzes regulatory pathways… |
| [risk-management-specialist](plugins/ra-qm-skills/skills/risk-management-specialist) | Medical device risk management specialist implementing ISO 14971 throughout product lifecycle. Provides risk analysis, risk evaluation, risk control, and… |
| [soc2-compliance](plugins/ra-qm-skills/skills/soc2-compliance) | Use when the user asks to prepare for SOC 2 audits, map Trust Service Criteria, build control matrices, collect audit evidence, perform gap analysis, or assess… |

</details>

<details><summary><b>research-summarizer</b> — installatienaam <code>research-summarizer</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [research-summarizer](plugins/research-summarizer/skills/research-summarizer) | Structured research summarization agent skill for non-dev users. Handles academic papers, web articles, reports, and documentation. Extracts key findings,… |

</details>

<details><summary><b>ruflo-adr</b> — installatienaam <code>ruflo-adr</code>, 5 skills</summary>

| Skill | Wat het doet |
|---|---|
| [adr-create](plugins/ruflo-adr/skills/adr-create) | Create a new Architecture Decision Record with sequential numbering and AgentDB registration |
| [adr-index](plugins/ruflo-adr/skills/adr-index) | Build or rebuild the ADR index + dependency graph by running scripts/import.mjs (handles v3-style and plugin-style ADR formats; one Bash call vs hundreds of… |
| [adr-reindex](plugins/ruflo-adr/skills/adr-reindex) | Reconcile the ADR index against a DELETED ADR file or relation line by dropping and rebuilding adr-patterns + adr-edges from scratch (scripts/reindex.mjs). Use… |
| [adr-review](plugins/ruflo-adr/skills/adr-review) | Review code changes against accepted ADRs for compliance violations |
| [adr-verify](plugins/ruflo-adr/skills/adr-verify) | Read back adr-patterns + adr-edges namespaces, surface dangling refs / supersede cycles / status mismatches; exit 1 on cycles |

</details>

<details><summary><b>ruflo-agent</b> — installatienaam <code>ruflo-agent</code>, 4 skills</summary>

| Skill | Wat het doet |
|---|---|
| [managed-agent](plugins/ruflo-agent/skills/managed-agent) | Run an Anthropic Claude Managed Agent — a cloud agent harness (container + filesystem + tools), the cloud counterpart of the local wasm-agent runtime |
| [nested-subagents](plugins/ruflo-agent/skills/nested-subagents) | Spawn nested sub-agents (agents that spawn sub-agents, up to depth=5) via Claude Code's native Task tool — for context-managed deep delegation |
| [wasm-agent](plugins/ruflo-agent/skills/wasm-agent) | Create and manage sandboxed WASM agents for isolated code execution |
| [wasm-gallery](plugins/ruflo-agent/skills/wasm-gallery) | Browse, publish, and install WASM agents from the community gallery |

</details>

<details><summary><b>ruflo-agentdb</b> — installatienaam <code>ruflo-agentdb</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [agentdb-query](plugins/ruflo-agentdb/skills/agentdb-query) | Query AgentDB through the controller bridge -- semantic routing, hierarchical recall, causal graphs, context synthesis, pattern store/search |
| [vector-search](plugins/ruflo-agentdb/skills/vector-search) | Vector search via embeddings_* (large-scale HNSW) and ruvllm_hnsw_* (WASM router for ≤11 hot patterns), with RaBitQ 1-bit quantization for 32× memory reduction |

</details>

<details><summary><b>ruflo-aidefence</b> — installatienaam <code>ruflo-aidefence</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [pii-detect](plugins/ruflo-aidefence/skills/pii-detect) | Detect and flag personally identifiable information (PII) in text, code, and configurations. Use before committing code, writing logs, storing data, or sending… |
| [safety-scan](plugins/ruflo-aidefence/skills/safety-scan) | Scan inputs for prompt injection, unsafe content, and adversarial attacks using AIDefence. Use when processing untrusted input (user submissions, API payloads,… |

</details>

<details><summary><b>ruflo-arena</b> — installatienaam <code>ruflo-arena</code>, 0 skills</summary>

| Skill | Wat het doet |
|---|---|

</details>

<details><summary><b>ruflo-autopilot</b> — installatienaam <code>ruflo-autopilot</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [autopilot-loop](plugins/ruflo-autopilot/skills/autopilot-loop) | Run an autonomous /loop iteration -- check progress, work on next task, schedule next wake |
| [autopilot-predict](plugins/ruflo-autopilot/skills/autopilot-predict) | Use learned patterns and current state to predict the optimal next action |

</details>

<details><summary><b>ruflo-browser</b> — installatienaam <code>ruflo-browser</code>, 10 skills</summary>

| Skill | Wat het doet |
|---|---|
| [browser-auth-flow](plugins/ruflo-browser/skills/browser-auth-flow) | Probe a site's authentication flow for redirect leaks, missing CSRF, weak session cookies, and OAuth misconfiguration; produces an auth findings.md |
| [browser-extract](plugins/ruflo-browser/skills/browser-extract) | Extract structured data via stored browser-templates or one-shot DOM queries, with mandatory AIDefence PII + prompt-injection gates before content reaches the… |
| [browser-form-fill](plugins/ruflo-browser/skills/browser-form-fill) | Fill a web form by mapping field-name → value, with optional template lookup from browser-templates for known forms |
| [browser-intent](plugins/ruflo-browser/skills/browser-intent) | Execute a natural-language browser intent via page-agent (browser_act) when the target is easier to describe than to select — degrades gracefully when… |
| [browser-login](plugins/ruflo-browser/skills/browser-login) | Drive an authentication flow once, sanitize cookies through AIDefence, and vault a reusable cookie handle in browser-cookies for future sessions |
| [browser-record](plugins/ruflo-browser/skills/browser-record) | Open a named, traced browser session into an RVF cognitive container with a ruvector trajectory recording every action |
| [browser-replay](plugins/ruflo-browser/skills/browser-replay) | Replay a recorded session trajectory against the same URL or a mutated variant; uses browser-selectors embedding similarity to recover from DOM drift |
| [browser-scrape](plugins/ruflo-browser/skills/browser-scrape) | DEPRECATED in v0.2.0 -- use browser-extract instead; this is a thin shim for backward compatibility, removed in v0.3.0 |
| [browser-screenshot-diff](plugins/ruflo-browser/skills/browser-screenshot-diff) | Visual + DOM diff between two recorded sessions at matching trajectory step ids; used for visual regression and replay verification |
| [browser-test](plugins/ruflo-browser/skills/browser-test) | UI test recipe -- composes browser-record (capture) + browser-replay (verify) so every test produces a replayable RVF artifact, not an ephemeral run |

</details>

<details><summary><b>ruflo-core</b> — installatienaam <code>ruflo-core</code>, 4 skills</summary>

| Skill | Wat het doet |
|---|---|
| [discover-plugins](plugins/ruflo-core/skills/discover-plugins) | Discover and recommend ruflo plugins based on your workflow, installed MCP tools, and current task |
| [init-project](plugins/ruflo-core/skills/init-project) | Initialize a new Ruflo project with MCP tools, hooks, and agent configuration. Use when setting up Ruflo in a fresh repo, or when the user says "init ruflo",… |
| [ruflo-doctor](plugins/ruflo-core/skills/ruflo-doctor) | Run health checks on the Ruflo installation and fix common issues |
| [witness](plugins/ruflo-core/skills/witness) | Sign, verify, and track fix-marker regressions over time using a deterministic Ed25519 witness manifest. Works in any project — clone the toolkit, run init,… |

</details>

<details><summary><b>ruflo-cost-tracker</b> — installatienaam <code>ruflo-cost-tracker</code>, 20 skills</summary>

| Skill | Wat het doet |
|---|---|
| [cost-anomaly](plugins/ruflo-cost-tracker/skills/cost-anomaly) | MAD-based outlier detection on session spend. Robust to the very outliers it hunts (unlike mean+sigma). Surfaces specific anomalous sessions with modified-z… |
| [cost-benchmark](plugins/ruflo-cost-tracker/skills/cost-benchmark) | Run the corpus benchmark — booster locally, optional Gemini/Sonnet/Opus baselines — and persist a verifiable measured-vs-claimed table |
| [cost-booster-edit](plugins/ruflo-cost-tracker/skills/cost-booster-edit) | Apply a simple code transform via agent-booster's WASM engine — sub-millisecond, deterministic, $0 (no LLM call). Companion to cost-booster-route. |
| [cost-booster-route](plugins/ruflo-cost-tracker/skills/cost-booster-route) | Route tasks through hooks_route, partition by Agent Booster availability, and report Tier 1 bypass utilization with $0 cost |
| [cost-budget-check](plugins/ruflo-cost-tracker/skills/cost-budget-check) | Read accumulated cost-tracking spend + budget config, compute utilization, emit 50/75/90/100% alert ladder |
| [cost-burn](plugins/ruflo-cost-tracker/skills/cost-burn) | Burn-rate trend over time with optional drift-alert exit code. Bins session spend into buckets, surfaces window-over-window delta, and can exit 1 when latest… |
| [cost-compact-context](plugins/ruflo-cost-tracker/skills/cost-compact-context) | Wrap getTokenOptimizer().getCompactContext() to retrieve compacted ReasoningBank context for cost-analysis queries; report bridge-reported tokensSaved |
| [cost-conversation](plugins/ruflo-cost-tracker/skills/cost-conversation) | Per-conversation cost view — list every session in cost-tracking with started-at, message count, top model, and total cost |
| [cost-counterfactual](plugins/ruflo-cost-tracker/skills/cost-counterfactual) | Multi-baseline counterfactual cost analysis. Compares actual session spend to hypothetical always-haiku / always-sonnet / always-opus routing baselines.… |
| [cost-diff](plugins/ruflo-cost-tracker/skills/cost-diff) | Snapshot delta between two cost-summary JSON outputs. PR-level cost regression detection — answers "what changed between these two specific snapshots?". Pairs… |
| [cost-export](plugins/ruflo-cost-tracker/skills/cost-export) | Export cost-tracking telemetry in Prometheus textfile or webhook JSON formats — for external observability (Grafana, Datadog, custom dashboards) |
| [cost-federation](plugins/ruflo-cost-tracker/skills/cost-federation) | Consumer-side wiring for ADR-097 Phase 3 federation_spend events — per-peer rolling windows + suspension-threshold check |
| [cost-health](plugins/ruflo-cost-tracker/skills/cost-health) | Composite CI gate — runs cost-budget-check + cost-burn + cost-anomaly + cost-projection in parallel and surfaces a single combined health status with max exit… |
| [cost-optimize](plugins/ruflo-cost-tracker/skills/cost-optimize) | Analyze token usage patterns and recommend cost optimizations with estimated savings |
| [cost-projection](plugins/ruflo-cost-tracker/skills/cost-projection) | Forward-looking spend extrapolation. Computes a USD-per-day rate from the recent measurement window, projects to 7d/30d/90d/365d horizons, and surfaces "days… |
| [cost-report](plugins/ruflo-cost-tracker/skills/cost-report) | Generate a cost report showing token usage and USD costs by agent and model |
| [cost-session](plugins/ruflo-cost-tracker/skills/cost-session) | Per-message cost breakdown within a single session. The drill-down companion to cost-anomaly — when an outlier session is flagged, this surfaces the specific… |
| [cost-summary](plugins/ruflo-cost-tracker/skills/cost-summary) | Single-shot programmatic dump of all cost data — total spend, per-tier, top session, budget status, federation aggregate. JSON or markdown. |
| [cost-track](plugins/ruflo-cost-tracker/skills/cost-track) | Auto-capture per-session token usage from the Claude Code session jsonl and persist to the cost-tracking namespace |
| [cost-trend](plugins/ruflo-cost-tracker/skills/cost-trend) | Read every docs/benchmarks/runs/*.json and surface drift in win rate, latency, escalation rate, and LLM-baseline cost over time |

</details>

<details><summary><b>ruflo-daa</b> — installatienaam <code>ruflo-daa</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [cognitive-pattern](plugins/ruflo-daa/skills/cognitive-pattern) | Define and manage cognitive patterns for agent reasoning and decision-making |
| [daa-agent](plugins/ruflo-daa/skills/daa-agent) | Create and adapt Dynamic Agentic Architecture agents that learn and evolve |

</details>

<details><summary><b>ruflo-ddd</b> — installatienaam <code>ruflo-ddd</code>, 3 skills</summary>

| Skill | Wat het doet |
|---|---|
| [ddd-aggregate](plugins/ruflo-ddd/skills/ddd-aggregate) | Scaffold an aggregate root with entity, value objects, repository interface, domain events, and test stubs. Use when adding a new aggregate to an existing… |
| [ddd-context](plugins/ruflo-ddd/skills/ddd-context) | Create and manage a DDD bounded context with standard directory structure. Use when starting a new subdomain, splitting a monolith into bounded contexts, or… |
| [ddd-validate](plugins/ruflo-ddd/skills/ddd-validate) | Validate domain boundaries -- detect cross-context import violations and aggregate invariant issues. Use when auditing a DDD codebase for leaks between bounded… |

</details>

<details><summary><b>ruflo-docs</b> — installatienaam <code>ruflo-docs</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [api-docs](plugins/ruflo-docs/skills/api-docs) | Generate API documentation from source code with JSDoc and OpenAPI support |
| [doc-gen](plugins/ruflo-docs/skills/doc-gen) | Generate and maintain documentation with drift detection. Use when the user asks to write/update/refresh docs, detect doc drift against code, or schedule… |

</details>

<details><summary><b>ruflo-federation</b> — installatienaam <code>ruflo-federation</code>, 3 skills</summary>

| Skill | Wat het doet |
|---|---|
| [federation-audit](plugins/ruflo-federation/skills/federation-audit) | Query federation audit logs with compliance filtering |
| [federation-init](plugins/ruflo-federation/skills/federation-init) | Initialize federation on this node — generate keypair and configure peers |
| [federation-status](plugins/ruflo-federation/skills/federation-status) | Show federation health — peers, sessions, trust levels, and message metrics. Use when the user asks "is federation healthy?", "show peers", "federation… |

</details>

<details><summary><b>ruflo-goals</b> — installatienaam <code>ruflo-goals</code>, 5 skills</summary>

| Skill | Wat het doet |
|---|---|
| [deep-research](plugins/ruflo-goals/skills/deep-research) | Orchestrate multi-phase deep research with web search, memory retrieval, pattern matching, and synthesis into structured findings |
| [dossier-collect](plugins/ruflo-goals/skills/dossier-collect) | Build a graph-structured dossier on a seed entity via parallel fan-out + recursive expansion across web, memory, knowledge-graph, codebase, ADR index, and git… |
| [goal-plan](plugins/ruflo-goals/skills/goal-plan) | Create and execute Goal-Oriented Action Plans (GOAP) with precondition analysis, cost optimization, and adaptive replanning |
| [horizon-track](plugins/ruflo-goals/skills/horizon-track) | Track long-horizon objectives across multiple sessions with milestone checkpoints, progress persistence, and drift detection |
| [research-synthesize](plugins/ruflo-goals/skills/research-synthesize) | Synthesize research findings from memory into structured reports with evidence grading, contradiction resolution, and actionable recommendations |

</details>

<details><summary><b>ruflo-graph-intelligence</b> — installatienaam <code>ruflo-graph-intelligence</code>, 0 skills</summary>

| Skill | Wat het doet |
|---|---|

</details>

<details><summary><b>ruflo-intelligence</b> — installatienaam <code>ruflo-intelligence</code>, 3 skills</summary>

| Skill | Wat het doet |
|---|---|
| [intelligence-route](plugins/ruflo-intelligence/skills/intelligence-route) | Route tasks via the 3-tier model selector and learned patterns; emits a routing rationale via hooks_explain |
| [intelligence-transfer](plugins/ruflo-intelligence/skills/intelligence-transfer) | Publish or fetch learned patterns across projects via IPFS (Pinata) -- the cross-project pattern transfer that hooks_transfer enables |
| [neural-train](plugins/ruflo-intelligence/skills/neural-train) | Train SONA + MicroLoRA neural patterns from successful task completions; runs the DISTILL + CONSOLIDATE phases of the 4-step pipeline |

</details>

<details><summary><b>ruflo-iot-cognitum</b> — installatienaam <code>ruflo-iot-cognitum</code>, 5 skills</summary>

| Skill | Wat het doet |
|---|---|
| [iot-anomalies](plugins/ruflo-iot-cognitum/skills/iot-anomalies) | Detect and classify telemetry anomalies on Cognitum Seed devices. Use when investigating a device that's reporting odd metrics, before approving a firmware… |
| [iot-firmware](plugins/ruflo-iot-cognitum/skills/iot-firmware) | Orchestrate firmware rollouts with canary deployment and anomaly-gated advancement |
| [iot-fleet](plugins/ruflo-iot-cognitum/skills/iot-fleet) | Create and manage Cognitum Seed device fleets with firmware policies |
| [iot-register](plugins/ruflo-iot-cognitum/skills/iot-register) | Register a Cognitum Seed device by endpoint and establish agent bridge |
| [iot-witness-verify](plugins/ruflo-iot-cognitum/skills/iot-witness-verify) | Verify witness chain integrity and detect provenance gaps |

</details>

<details><summary><b>ruflo-jujutsu</b> — installatienaam <code>ruflo-jujutsu</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [diff-analyze](plugins/ruflo-jujutsu/skills/diff-analyze) | Analyze git diffs for risk scoring, reviewer recommendations, and change classification. Use when preparing a PR, reviewing a large or cross-module change, or… |
| [git-workflow](plugins/ruflo-jujutsu/skills/git-workflow) | Advanced git workflows with branch management, conflict resolution, and PR lifecycle |

</details>

<details><summary><b>ruflo-knowledge-graph</b> — installatienaam <code>ruflo-knowledge-graph</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [kg-extract](plugins/ruflo-knowledge-graph/skills/kg-extract) | Extract entities and relations from source files to build a knowledge graph |
| [kg-traverse](plugins/ruflo-knowledge-graph/skills/kg-traverse) | Pathfinder traversal of the knowledge graph starting from a seed entity |

</details>

<details><summary><b>ruflo-loop-workers</b> — installatienaam <code>ruflo-loop-workers</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [cron-schedule](plugins/ruflo-loop-workers/skills/cron-schedule) | Schedule persistent background workers via CronCreate |
| [loop-worker](plugins/ruflo-loop-workers/skills/loop-worker) | Run Ruflo background workers using Claude Code native /loop scheduling |

</details>

<details><summary><b>ruflo-market-data</b> — installatienaam <code>ruflo-market-data</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [market-ingest](plugins/ruflo-market-data/skills/market-ingest) | Ingest and normalize market data into OHLCV vectors with HNSW indexing |
| [market-pattern](plugins/ruflo-market-data/skills/market-pattern) | Detect and classify candlestick patterns from ingested OHLCV data |

</details>

<details><summary><b>ruflo-metaharness</b> — installatienaam <code>ruflo-metaharness</code>, 13 skills</summary>

| Skill | Wat het doet |
|---|---|
| [harness-bench](plugins/ruflo-metaharness/skills/harness-bench) | Manage `@metaharness/darwin` bench suites — `bench create <repo>` scaffolds a JSON suite from a repo's test corpus; `bench verify <suite.json>` checks suite… |
| [harness-drift-from-history](plugins/ruflo-metaharness/skills/harness-drift-from-history) | One-command drift detection. Composes audit-list + oia-audit + audit-trend into a single primitive — finds the most recent audit in `metaharness-audit`… |
| [harness-evolve](plugins/ruflo-metaharness/skills/harness-evolve) | Run `@metaharness/darwin evolve <repo>` to mutate a harness's seven policy surfaces… |
| [harness-genome](plugins/ruflo-metaharness/skills/harness-genome) | 7-section repo readiness report from `metaharness genome <path>`. Returns repo_type / agent_topology / risk_score / mcp_surface / test_confidence /… |
| [harness-gepa](plugins/ruflo-metaharness/skills/harness-gepa) | Inspect and audit GEPA genomes via the `@metaharness/darwin/gepa` library entry (darwin 0.8.0) — load/validate a genome (default: the shipped cand-6… |
| [harness-learn](plugins/ruflo-metaharness/skills/harness-learn) | Run a GEPA learning cycle via `metaharness learn` (upstream ADR-235, metaharness@0.3.0) — optimizes a harness genome against a SWE-bench-style slice manifest.… |
| [harness-mcp-scan](plugins/ruflo-metaharness/skills/harness-mcp-scan) | Static security scan of a harness's declared MCP surface via `harness mcp-scan <path>`. Reads `.mcp/servers.json` + `.harness/claims.json`. Pure-read, no… |
| [harness-mint](plugins/ruflo-metaharness/skills/harness-mint) | Scaffold a custom AI agent harness via `metaharness new <name> --template <id> --host <id>`. Defaults to DRY-RUN (no writes) unless --confirm is passed.… |
| [harness-oia-audit](plugins/ruflo-metaharness/skills/harness-oia-audit) | Composite Phase-2 audit worker (ADR-150). Bundles harness oia-manifest + threat-model + mcp-scan into one timestamped audit record stored in the… |
| [harness-score](plugins/ruflo-metaharness/skills/harness-score) | 5-dimension harness readiness scorecard from `metaharness score <path>`. Returns harnessFit / compileConfidence / taskCoverage / toolSafety / memoryUsefulness… |
| [harness-security-bench](plugins/ruflo-metaharness/skills/harness-security-bench) | Run `@metaharness/darwin security bench` (upstream "Darwin Shield" / ADR-155) — evolves a champion security-detection harness against a 10-vuln / 9-decoy… |
| [harness-similarity](plugins/ruflo-metaharness/skills/harness-similarity) | ADR-152 — weighted similarity between two harness fingerprints (genome + score JSON). Returns overall score in [0,1] plus per-component breakdown (cosine over… |
| [harness-threat-model](plugins/ruflo-metaharness/skills/harness-threat-model) | Enterprise-review-grade threat model from `harness threat-model <path>`. Categorizes MCP-surface threats; emits `worst: 'clean''low''medium''high'` +… |

</details>

<details><summary><b>ruflo-migrations</b> — installatienaam <code>ruflo-migrations</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [migrate-create](plugins/ruflo-migrations/skills/migrate-create) | Create a new sequentially numbered database migration with up/down SQL files |
| [migrate-validate](plugins/ruflo-migrations/skills/migrate-validate) | Validate pending migrations for foreign key consistency, rollback safety, and best practices |

</details>

<details><summary><b>ruflo-neural-trader</b> — installatienaam <code>ruflo-neural-trader</code>, 9 skills</summary>

| Skill | Wat het doet |
|---|---|
| [trader-backtest](plugins/ruflo-neural-trader/skills/trader-backtest) | Run a historical backtest using npx neural-trader with Rust/NAPI engine (8-19x faster) and walk-forward validation; Ed25519-sign the result for paper→live… |
| [trader-cloud-backtest](plugins/ruflo-neural-trader/skills/trader-cloud-backtest) | Run a heavy neural-trader job (long walk-forward, big Monte-Carlo, parameter sweep, model training) on the Anthropic Managed Agent cloud runtime instead of… |
| [trader-explain](plugins/ruflo-neural-trader/skills/trader-explain) | Regulator-grade feature attribution for any LSTM/Transformer signal — single-entry PageRank ranks the top-K features that drove the prediction (ADR-126 Phase… |
| [trader-portfolio-cg](plugins/ruflo-neural-trader/skills/trader-portfolio-cg) | Mean-variance portfolio optimization via Conjugate Gradient — 40-60× faster than the legacy Neumann path (ADR-126 Phase 3, ADR-123 Wedge 8) |
| [trader-portfolio](plugins/ruflo-neural-trader/skills/trader-portfolio) | Optimize portfolio allocation using npx neural-trader mean-variance engine with risk constraints and rebalancing plan |
| [trader-regime](plugins/ruflo-neural-trader/skills/trader-regime) | Detect current market regime using npx neural-trader — bull/bear/ranging/volatile classification with recommended strategy. Use when the user asks about market… |
| [trader-risk](plugins/ruflo-neural-trader/skills/trader-risk) | Assess portfolio risk using npx neural-trader — VaR, CVaR, Sharpe, position sizing, circuit breaker status |
| [trader-signal](plugins/ruflo-neural-trader/skills/trader-signal) | Generate trading signals using npx neural-trader anomaly detection engine with Z-score scoring and neural prediction |
| [trader-train](plugins/ruflo-neural-trader/skills/trader-train) | Train neural models (LSTM, Transformer, N-BEATS) on market data using npx neural-trader with confidence intervals |

</details>

<details><summary><b>ruflo-observability</b> — installatienaam <code>ruflo-observability</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [observe-metrics](plugins/ruflo-observability/skills/observe-metrics) | Aggregate and display system metrics with anomaly detection for a time period |
| [observe-trace](plugins/ruflo-observability/skills/observe-trace) | Trace agent execution by collecting spans and building a trace tree for a task |

</details>

<details><summary><b>ruflo-plugin-creator</b> — installatienaam <code>ruflo-plugin-creator</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [create-plugin](plugins/ruflo-plugin-creator/skills/create-plugin) | Scaffold a new Claude Code plugin with proper directory structure, plugin.json, skills, commands, and agents |
| [validate-plugin](plugins/ruflo-plugin-creator/skills/validate-plugin) | Validate a Claude Code plugin structure, frontmatter, and MCP tool references |

</details>

<details><summary><b>ruflo-rag-memory</b> — installatienaam <code>ruflo-rag-memory</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [memory-bridge](plugins/ruflo-rag-memory/skills/memory-bridge) | Bridge Claude Code auto-memory into AgentDB with ONNX embeddings, deduplicate, and enable unified cross-project search |
| [memory-search](plugins/ruflo-rag-memory/skills/memory-search) | SOTA semantic search — hybrid (sparse+dense), Graph RAG multi-hop, MMR diversity reranking, recency weighting |

</details>

<details><summary><b>ruflo-ruvector</b> — installatienaam <code>ruflo-ruvector</code>, 4 skills</summary>

| Skill | Wat het doet |
|---|---|
| [vector-cluster](plugins/ruflo-ruvector/skills/vector-cluster) | Cluster code by graph community detection via npx ruvector@0.2.25 hooks graph-cluster (spectral / Louvain) |
| [vector-embed](plugins/ruflo-ruvector/skills/vector-embed) | Generate embeddings via npx ruvector@0.2.25 embed text (ONNX all-MiniLM-L6-v2, 384-dim), normalize, and store in HNSW index |
| [vector-hyperbolic](plugins/ruflo-ruvector/skills/vector-hyperbolic) | Embed hierarchical data via npx ruvector@0.2.25 embed text and project into the Poincare ball in user code (no --model poincare flag in 0.2.25) |
| [vector-setup](plugins/ruflo-ruvector/skills/vector-setup) | First-run setup for ruvector@0.2.25 — installs ONNX/Brain/SONA add-ons, registers the MCP server, and verifies the install via `doctor` |

</details>

<details><summary><b>ruflo-ruvllm</b> — installatienaam <code>ruflo-ruvllm</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [chat-format](plugins/ruflo-ruvllm/skills/chat-format) | Format prompts for different LLM providers with chat templates and HNSW-powered context retrieval |
| [llm-config](plugins/ruflo-ruvllm/skills/llm-config) | Configure RuVLLM local inference with model selection, MicroLoRA fine-tuning, and SONA adaptation |

</details>

<details><summary><b>ruflo-rvf</b> — installatienaam <code>ruflo-rvf</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [rvf-manage](plugins/ruflo-rvf/skills/rvf-manage) | Manage RVF (Ruflo Vector Format) files for portable agent memory and cross-platform transfer |
| [session-persist](plugins/ruflo-rvf/skills/session-persist) | Persist and restore agent sessions across conversations with state snapshots |

</details>

<details><summary><b>ruflo-security-audit</b> — installatienaam <code>ruflo-security-audit</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [dependency-check](plugins/ruflo-security-audit/skills/dependency-check) | Scan project dependencies for known vulnerabilities and CVEs. Use when auditing third-party packages, before releases, after `npm install`/lockfile changes, or… |
| [security-scan](plugins/ruflo-security-audit/skills/security-scan) | Run full security scans on the codebase using Ruflo security tools. Use when reviewing PRs for security regressions, auditing auth/input-handling code, before… |

</details>

<details><summary><b>ruflo-sparc</b> — installatienaam <code>ruflo-sparc</code>, 3 skills</summary>

| Skill | Wat het doet |
|---|---|
| [sparc-implement](plugins/ruflo-sparc/skills/sparc-implement) | Run the SPARC Pseudocode and Architecture phases (2 and 3) — write algorithm pseudocode, design module boundaries and API contracts, then implement |
| [sparc-refine](plugins/ruflo-sparc/skills/sparc-refine) | Run the SPARC Refinement and Completion phases — review code, improve test coverage, validate against specification, and generate documentation |
| [sparc-spec](plugins/ruflo-sparc/skills/sparc-spec) | Run the SPARC Specification phase — gather requirements, define acceptance criteria, identify constraints, and store the spec in memory |

</details>

<details><summary><b>ruflo-swarm</b> — installatienaam <code>ruflo-swarm</code>, 2 skills</summary>

| Skill | Wat het doet |
|---|---|
| [monitor-stream](plugins/ruflo-swarm/skills/monitor-stream) | Stream live swarm events using the Monitor tool for real-time observability |
| [swarm-init](plugins/ruflo-swarm/skills/swarm-init) | Initialize a multi-agent swarm with anti-drift configuration. Use when starting a complex multi-file task that needs 3+ coordinated agents (feature… |

</details>

<details><summary><b>ruflo-testgen</b> — installatienaam <code>ruflo-testgen</code>, 3 skills</summary>

| Skill | Wat het doet |
|---|---|
| [tdd-repair](plugins/ruflo-testgen/skills/tdd-repair) | Test-Driven Repair — given a failing test, spawn a bounded headless `claude -p` (Read/Edit/Bash only) that makes the test pass without modifying it. Modeled on… |
| [tdd-workflow](plugins/ruflo-testgen/skills/tdd-workflow) | TDD London School workflow -- mock-first, outside-in test development |
| [test-gaps](plugins/ruflo-testgen/skills/test-gaps) | Detect missing test coverage and generate test suggestions. Use when the user asks about coverage gaps, untested code, or what tests to write next; also after… |

</details>

<details><summary><b>ruflo-workflows</b> — installatienaam <code>ruflo-workflows</code>, 5 skills</summary>

| Skill | Wat het doet |
|---|---|
| [gaia-architecture-comparison](plugins/ruflo-workflows/skills/gaia-architecture-comparison) | Side-by-side comparison of ruflo vs HAL vs other GAIA harnesses — capability gaps, design decisions, and improvement roadmap |
| [gaia-debugging](plugins/ruflo-workflows/skills/gaia-debugging) | Diagnose why a GAIA question failed — extract trace, classify failure mode, and propose a fix. Use when a GAIA benchmark run reports a failed/incorrect task_id… |
| [gaia-submission](plugins/ruflo-workflows/skills/gaia-submission) | Walk through a complete GAIA benchmark→submit flow — from key resolution through HAL-compatible package generation |
| [workflow-create](plugins/ruflo-workflows/skills/workflow-create) | Author a workflow — either an MCP workflow template (persisted, lifecycle) or a native .claude/workflows/*.js orchestration script (agent/parallel/pipeline… |
| [workflow-run](plugins/ruflo-workflows/skills/workflow-run) | Run a workflow — drive an MCP workflow lifecycle (execute/pause/resume/cancel) or invoke + resume a native .claude/workflows/*.js orchestration via the… |

</details>

<details><summary><b>self-improving-agent</b> — installatienaam <code>si</code>, 6 skills</summary>

| Skill | Wat het doet |
|---|---|
| [extract](plugins/self-improving-agent/skills/extract) | Turn a proven pattern or debugging solution into a standalone reusable skill with SKILL.md, reference docs, and examples. |
| [promote](plugins/self-improving-agent/skills/promote) | Graduate a proven pattern from auto-memory (MEMORY.md) to CLAUDE.md or .claude/rules/ for permanent enforcement. |
| [remember](plugins/self-improving-agent/skills/remember) | Explicitly save important knowledge to auto-memory with timestamp and context. Use when a discovery is too important to rely on auto-capture. |
| [review](plugins/self-improving-agent/skills/review) | Analyze auto-memory for promotion candidates, stale entries, consolidation opportunities, and health metrics. |
| [self-improving-agent](plugins/self-improving-agent/skills/self-improving-agent) | Curate Claude Code's auto-memory into durable project knowledge. Analyze MEMORY.md for patterns, promote proven learnings to CLAUDE.md and .claude/rules/,… |
| [status](plugins/self-improving-agent/skills/status) | Memory health dashboard showing line counts, topic files, capacity, stale entries, and recommendations. |

</details>

<details><summary><b>slo-architect</b> — installatienaam <code>slo-architect</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [slo-architect](plugins/slo-architect/skills/slo-architect) | Use when defining, reviewing, or operating SLOs/SLIs/error budgets. Triggers on "define an SLO", "what should our SLO be", "error budget", "burn rate", "SLI",… |

</details>

<details><summary><b>small-business</b> — installatienaam <code>small-business</code>, 44 skills</summary>

| Skill | Wat het doet |
|---|---|
| [ad-manager](plugins/small-business/skills/ad-manager) | The ads consultant that becomes an ads agent. Reads paid-ad performance natively through the TikTok Ads connector, or via a build-connector Zapier connection… |
| [ap-processor](plugins/small-business/skills/ap-processor) | Works the bill pile end to end: reads bills and vendor statements out of the AP inbox or from uploaded PDFs and phone photos, pulls out vendor, amount, due… |
| [brand-style](plugins/small-business/skills/brand-style) | Sets and updates the owner's brand look and output preferences, which every page and document the plugin produces then follows automatically. Captures the… |
| [build-agent](plugins/small-business/skills/build-agent) | Turns a task the owner keeps doing by hand into a named, reusable skill they can trigger by name or put on a schedule. Watches them do it once or listens to… |
| [build-connector](plugins/small-business/skills/build-connector) | Gets Claude talking to a tool nobody built an official connector for. Works out what the system is, checks the Claude connector directory for an existing… |
| [business-pulse](plugins/small-business/skills/business-pulse) | Produces a one-page cross-functional business snapshot for SMB owners — cash position (the ledger: MYOB, NetSuite, QuickBooks, Xero, or Zoho Books), sales… |
| [call-list](plugins/small-business/skills/call-list) | Builds today's call list. Runs lead-triage to rank the top-5 leads most worth calling, supplies talking points from email history, blocks time on the calendar,… |
| [canva-creator](plugins/small-business/skills/canva-creator) | Takes an approved content brief and executes a campaign end-to-end: builds the posting calendar, generates Canva designs for social posts, drafts caption and… |
| [cash-flow-snapshot](plugins/small-business/skills/cash-flow-snapshot) | Reads AR/AP, historical cash timing, and known fixed costs from the ledger (MYOB, NetSuite, QuickBooks, Xero, or Zoho Books) or from PayPal, Square, or Stripe… |
| [close-month](plugins/small-business/skills/close-month) | Closes the books and turns them into a decision as a three-link chain — month-end-prep reconciles the ledger against every connected payment processor and… |
| [content-strategy](plugins/small-business/skills/content-strategy) | Analyzes sales data from PayPal and QuickBooks to find top performers and slow movers, layers in seasonality, and produces a prioritized 30-day content brief:… |
| [contract-review](plugins/small-business/skills/contract-review) | Lightweight NDA, MSA, and vendor contract review for SMBs without legal on staff. Reads contracts from local files, mail attachments (Gmail or M365), a… |
| [crm-autopilot](plugins/small-business/skills/crm-autopilot) | Keeps the CRM current without the owner ever opening it. Creates and updates contacts and deals from email, calendar, and call transcripts; logs activity… |
| [grant-rfp-writer](plugins/small-business/skills/grant-rfp-writer) | Finds grant and solicitation opportunities the organization actually qualifies for, runs a hard go/no-go before anyone starts writing, drafts the application… |
| [grow-pipeline](plugins/small-business/skills/grow-pipeline) | Fills the funnel end to end without the owner babysitting it — reads the market and the competition for context, builds a ranked list of named prospects with a… |
| [growth-pulse](plugins/small-business/skills/growth-pulse) | Answers one question for an SMB owner — is the growth engine actually working? Pulls sales trend by channel, funnel conversion, campaign return, best and worst… |
| [hiring-screener](plugins/small-business/skills/hiring-screener) | Takes a pile of applications and turns it into a ranked shortlist, scored only against the job's stated rubric, with drafted replies to every candidate,… |
| [inbox-manager](plugins/small-business/skills/inbox-manager) | Turns a full inbox into a short, ranked list of what actually needs the owner. Reads the mail, sorts it into needs-you, drafted-and-waiting, and handled,… |
| [inventory-planner](plugins/small-business/skills/inventory-planner) | Works out what to reorder and when, from what is actually selling: pulls sales history and stock on hand from Shopify, Square, NetSuite, or an uploaded CSV,… |
| [invoice-chase](plugins/small-business/skills/invoice-chase) | Drafts overdue-invoice reminder emails from the ledger (MYOB, NetSuite, QuickBooks, Xero, or Zoho Books) plus PayPal, Stripe, and Airwallex data, matched to… |
| [job-post-builder](plugins/small-business/skills/job-post-builder) | Builds end-to-end hiring packets — job post, structured interview guide with scoring rubric, and offer letter template — from a hiring brief. Triggers on:… |
| [lead-finder](plugins/small-business/skills/lead-finder) | Builds a ranked list of prospects worth contacting. Works out the owner's ideal customer profile from the customers they already have, finds look-alike… |
| [lead-triage](plugins/small-business/skills/lead-triage) | Scores inbound HubSpot leads by engagement signals, company fit, and urgency markers, ranks the ones worth a call today with talking points, drafts the… |
| [marketing-monday](plugins/small-business/skills/marketing-monday) | Delivers the weekly growth briefing as one merged read — whether the growth engine is working, what customers are saying in public and private, what… |
| [monday-brief](plugins/small-business/skills/monday-brief) | Runs the owner's Monday morning briefing as a two-link chain — business-pulse for the cross-connector snapshot of cash, sales, and pipeline, and report-builder… |
| [month-end-prep](plugins/small-business/skills/month-end-prep) | Reconciles the accounting ledger (MYOB, NetSuite, QuickBooks, Xero, or Zoho Books) against PayPal, Shopify, Square, and Stripe settlements, flags transactions… |
| [outreach-composer](plugins/small-business/skills/outreach-composer) | Writes prospect outreach and follow-up sequences that sound like the owner wrote them, not like an AI did. Learns a voice profile from the owner's own sent… |
| [pay-the-bills](plugins/small-business/skills/pay-the-bills) | Works the bill pile from the AP inbox all the way to a staged payment run — reads and codes every bill, then checks the cash position before a dollar is… |
| [payroll-prep](plugins/small-business/skills/payroll-prep) | Gets payroll ready to run without anyone getting shorted: pulls timesheets from Gusto, QuickBooks Payroll, or an uploaded spreadsheet, totals regular,… |
| [plan-payroll](plugins/small-business/skills/plan-payroll) | Runs the payroll-confidence chain end to end — forecasts cash across the payroll window with cash-flow-snapshot, ranks and drafts overdue-invoice reminders… |
| [proposal-builder](plugins/small-business/skills/proposal-builder) | Turns whatever came out of a discovery conversation — a call transcript, a voice memo, jobsite photos, an RFP document, a set of drawings, or scrappy notes —… |
| [reactivate](plugins/small-business/skills/reactivate) | Wins back customers who have quietly stopped buying — finds the ones whose gap has stretched past their own normal rhythm or who are showing churn signals,… |
| [report-builder](plugins/small-business/skills/report-builder) | Turns a plain-English description of a recurring report into a real, repeatable report — defines the metrics, pulls them from whatever data sources are… |
| [report-pack](plugins/small-business/skills/report-pack) | Delivers the owner's custom recurring report pack on a set cadence — runs the saved report definition from report-builder, wraps it in a business-pulse… |
| [restock](plugins/small-business/skills/restock) | Turns what is actually selling into a reorder decision and gets it all the way into the books — computes sales velocity and conservative stockout dates per… |
| [review-reputation](plugins/small-business/skills/review-reputation) | Watches what customers are saying in public and in private, then does something about it. Aggregates Google, Yelp, and Facebook reviews alongside disputes,… |
| [seo-ai-visibility](plugins/small-business/skills/seo-ai-visibility) | Audits and fixes both halves of being found — classic search and AI answers. Search side: rankings, site structure, page speed, titles and descriptions, and… |
| [smb-onboard](plugins/small-business/skills/smb-onboard) | Claude as the trainer. Walks an SMB owner through connecting their first two tools, runs one recipe to prove immediate value, interviews them about their… |
| [smb-router](plugins/small-business/skills/smb-router) | The front door to the Small Business plugin. Listens to what the owner needs right now — vague or specific — and routes them to the best skill or slash command… |
| [social-content-engine](plugins/small-business/skills/social-content-engine) | Runs the owner's content operation as a standing thing rather than a one-off: keeps a rolling posting calendar, learns the owner's voice, generates on-brand… |
| [speed-to-lead](plugins/small-business/skills/speed-to-lead) | Makes sure no inbound lead goes unanswered. Watches web forms, the shared inbox, and the CRM for new inquiries, qualifies each one against the owner's… |
| [tax-prep](plugins/small-business/skills/tax-prep) | Prepares tax materials as a two-link chain — month-end-prep confirms the books are closed and reconciled first, then tax-season-organizer calculates the… |
| [tax-season-organizer](plugins/small-business/skills/tax-season-organizer) | Prepares tax-season materials for the owner's accountant, not tax advice. US federal tax; a non-US business gets its closed-books packet instead. Two modes:… |
| [ticket-deflector](plugins/small-business/skills/ticket-deflector) | Reads a forwarded customer email or ticket, pulls order and refund status from a payments connector (PayPal, Square, or Stripe) or Shopify, account history… |

</details>

<details><summary><b>statistical-analyst</b> — installatienaam <code>statistical-analyst</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [statistical-analyst](plugins/statistical-analyst/skills/statistical-analyst) | Run hypothesis tests, analyze A/B experiment results, calculate sample sizes, and interpret statistical significance with effect sizes. Use when you need to… |

</details>

<details><summary><b>terraform-patterns</b> — installatienaam <code>terraform-patterns</code>, 1 skill</summary>

| Skill | Wat het doet |
|---|---|
| [terraform-patterns](plugins/terraform-patterns/skills/terraform-patterns) | Terraform infrastructure-as-code agent skill and plugin for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw. Covers module design patterns, state management… |

</details>

<details><summary><b>wix</b> — installatienaam <code>wix</code>, 46 skills</summary>

| Skill | Wat het doet |
|---|---|
| [wix-app](plugins/wix/skills/wix-app) | Build and review Wix CLI app extensions — dashboard pages, modals, plugins, menu plugins, custom element widgets, Editor React components, site plugins,… |
| [wix-auth](plugins/wix/skills/wix-auth) | Authenticate with Wix to obtain an access token for calling Wix APIs. Use when an agent needs a valid Wix access token and has none, or when the stored token… |
| [wix-base44-connector](plugins/wix/skills/wix-base44-connector) | Build on and manage the connected Wix site from a Base44 app: discover and call any Wix API (endpoints, request/response shapes, fields), gather site context,… |
| [wix-design-system](plugins/wix/skills/wix-design-system) | Wix Design System component reference. Use when building UI with @wix/design-system, choosing components, checking props and examples, or writing tests with… |
| [wix-docs](plugins/wix/skills/wix-docs) | Look up the Wix API/SDK documentation to confirm an exact endpoint, HTTP method, request/response shape, field, enum, or error before writing Wix code — never… |
| [wix-headless-fast](plugins/wix/skills/wix-headless-fast) | Build a Wix Headless site fast by wiring SHIPPED, verified @wix/sdk code instead of authoring the integration from recipes. Each Wix business vertical ships a… |
| [wix-headless](plugins/wix/skills/wix-headless) | Connect Wix business services (Stores, Bookings, CMS, Blog, Events, Forms, and more) to a Wix Headless frontend — infer the needed capabilities, install the… |
| [wix-manage](plugins/wix/skills/wix-manage) | REST recipes to configure and manage a Wix site's business solutions — stores, bookings, payments, CMS, and more. Open the matching recipe for the exact… |
| [replatform](plugins/wix/skills/wix-replatform) | Routes RePlatform source-to-Wix migrations to the next workflow step by inspecting migration project artifacts. Use when starting, continuing, or recovering a… |
| [rp-discovery](plugins/wix/skills/wix-replatform/resources/rp-discovery) | Discovers and documents the source platform schema (entities, fields, relationships) for a migration project. Use when capturing source structure before… |
| [rp-execute-import](plugins/wix/skills/wix-replatform/resources/rp-execute-import) | Runs the generated extract/import pipeline and records execution results. Use when setup and codegen are complete and the user has approved the execution plan. |
| [rp-execute-setup](plugins/wix/skills/wix-replatform/resources/rp-execute-setup) | Verifies and provisions Wix-side setup required before import. Use after codegen when machine-readable setup artifacts must be validated or executed against… |
| [rp-import-codegen](plugins/wix/skills/wix-replatform/resources/rp-import-codegen) | Generates migration readers, transforms, setup plans, and thin Wix write specs from schema and mapping artifacts. Use when producing runnable extract/import… |
| [rp-mapper](plugins/wix/skills/wix-replatform/resources/rp-mapper) | Maps discovered source entities and fields to Wix targets and documents lossiness. Use when creating machine-readable mapping artifacts and review markdown… |
| [rp-setup-discovery](plugins/wix/skills/wix-replatform/resources/rp-setup-discovery) | Derives Wix environment prerequisites (apps, collections, schemas) from an approved mapping plan. Use after mapping review and before import code generation. |
| [rp-source-csv](plugins/wix/skills/wix-replatform/resources/rp-source-csv) | CSV file source adapter: parse core, vendor fingerprinting (Shopify, WooCommerce, Magento, BigCommerce), layout inference, file-set handling, and read contract… |
| [rp-source-wordpress](plugins/wix/skills/wix-replatform/resources/rp-source-wordpress) | WordPress and WooCommerce source adapter: REST capture, auth, pagination, and read contract for codegen. Use when the source platform is WordPress or… |
| [rp-target-wix](plugins/wix/skills/wix-replatform/resources/rp-target-wix) | Wix target adapter with verified write primitives, shared execution runtimes, and contract tests. Use when vendoring Wix writers, validating API shapes, or Wix… |
| [rp-telemetry](plugins/wix/skills/wix-replatform/resources/rp-telemetry) | Always-active telemetry companion for RePlatform migration runs. Records what happened during a run — halts, errors, fidelity losses, API gaps, skill coverage… |
| [wix-vibe-headless](plugins/wix/skills/wix-vibe-headless) | Client-only, dependency-free REST scaffolds for connecting an already-built front end (a vibe-coded app, an HTML/JSX/Vite project, a design-tool export) to a… |
| [wix-headless-replatform](plugins/wix/wix-headless-replatform) | Clone, rebuild, migrate, or reverse-engineer a public website home page into a Wix Headless frontend while preserving source identity, SEO, interactions, and… |
| [rp-facelift](plugins/wix/wix-headless-replatform/resources/rp-facelift) | Apply an explicitly requested, identity-preserving UI/UX refinement after clone acceptance. |
| [rp-project-context](plugins/wix/wix-headless-replatform/resources/rp-project-context) | Resolve headless mode, scope, Wix project validity, and browser execution readiness. |
| [rp-qa-gap-loop](plugins/wix/wix-headless-replatform/resources/rp-qa-gap-loop) | Verify the running clone, perform auditable visual comparison and gap fixes, and finalize frontend completion. |
| [rp-source-evidence](plugins/wix/wix-headless-replatform/resources/rp-source-evidence) | Produce fresh browser-derived source evidence and implementation contracts for a headless clone. |
| [rp-ui-implementation](plugins/wix/wix-headless-replatform/resources/rp-ui-implementation) | Implement a Wix Headless clone from generated source evidence. |
| [wix-replatform](plugins/wix/wix-replatform) | Routes RePlatform source-to-Wix migrations to the next required workflow module by inspecting authoritative migration artifacts. Use when starting, resuming,… |
| [rp-destination](plugins/wix/wix-replatform/resources/rp-destination) | Resolves, adopts, or creates the one Wix Managed Headless destination for a migration. |
| [rp-discovery](plugins/wix/wix-replatform/resources/rp-discovery) | Discovers and documents the source platform schema (entities, fields, relationships) for a migration project. Use when capturing source structure before… |
| [rp-execute-import](plugins/wix/wix-replatform/resources/rp-execute-import) | Runs the generated extract/import pipeline and records execution results. Use when setup and codegen are complete and the user has approved the execution plan. |
| [rp-execute-setup](plugins/wix/wix-replatform/resources/rp-execute-setup) | Verifies and provisions Wix-side setup required before import. Use after codegen when machine-readable setup artifacts must be validated or executed against… |
| [rp-execution-policy](plugins/wix/wix-replatform/resources/rp-execution-policy) | Applies cross-stage execution safety policy and writes the aggregate migration completion artifact after all delivery-specific terminal evidence validates. |
| [rp-import-codegen](plugins/wix/wix-replatform/resources/rp-import-codegen) | Generates migration readers, transforms, setup plans, and thin Wix write specs from schema and mapping artifacts. Use when producing runnable extract/import… |
| [rp-mapper](plugins/wix/wix-replatform/resources/rp-mapper) | Maps discovered source entities and fields to Wix targets and documents lossiness. Use when creating machine-readable mapping artifacts and review markdown… |
| [rp-preflight](plugins/wix/wix-replatform/resources/rp-preflight) | Validates the selected source and destination configuration before discovery. |
| [rp-project-intake](plugins/wix/wix-replatform/resources/rp-project-intake) | Resolves the active migration project and the minimum intake decisions needed to route it. |
| [rp-quick-runtime](plugins/wix/wix-replatform/resources/rp-quick-runtime) | Shared deterministic target-limit recovery and final-report runtime every rp-quick-<platform> quick-mode adapter uses before a Wix Stores write. |
| [rp-quick-shopify](plugins/wix/wix-replatform/resources/rp-quick-shopify) | Runs the bounded deterministic public Shopify catalog quick-import adapter after a qualifying source probe. |
| [rp-quick-woocommerce](plugins/wix/wix-replatform/resources/rp-quick-woocommerce) | Runs the bounded deterministic public WooCommerce quick-import adapter after a qualifying source probe. |
| [rp-setup-discovery](plugins/wix/wix-replatform/resources/rp-setup-discovery) | Derives Wix environment prerequisites (apps, collections, schemas) from an approved mapping plan. Use after mapping review and before import code generation. |
| [rp-source-csv](plugins/wix/wix-replatform/resources/rp-source-csv) | CSV file source adapter: parse core, vendor fingerprinting (Shopify, WooCommerce, Magento, BigCommerce), layout inference, file-set handling, and read contract… |
| [rp-source-inputs](plugins/wix/wix-replatform/resources/rp-source-inputs) | Collects and validates source URLs, exports, acquisition modes, and credentials without exposing secrets. |
| [rp-source-wordpress](plugins/wix/wix-replatform/resources/rp-source-wordpress) | WordPress and WooCommerce source adapter: REST capture, auth, pagination, and read contract for codegen. Use when the source platform is WordPress or… |
| [rp-target-wix](plugins/wix/wix-replatform/resources/rp-target-wix) | Wix target adapter with verified write primitives, shared execution runtimes, and contract tests. Use when vendoring Wix writers, validating API shapes, or Wix… |
| [rp-telemetry](plugins/wix/wix-replatform/resources/rp-telemetry) | Always-active telemetry companion for RePlatform migration runs. Records what happened during a run — halts, errors, fidelity losses, API gaps, skill coverage… |
| [rp-website-continuation](plugins/wix/wix-replatform/resources/rp-website-continuation) | Continues a website-mode migration from the validated backend handoff through frontend build, post-build gap analysis/fixing, release, and a durable frontend… |

</details>

