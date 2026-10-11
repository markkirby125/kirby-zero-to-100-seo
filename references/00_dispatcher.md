# Kirby Zero to 100 SEO: Launch Playbook

This skill is a standalone engine for launching a brand-new site from zero authority to an established entity, based on Charles Floate's Ep 1136 "Zero to 100" methodology. It scaffolds a non-indexed staging workspace and generates a velocity-matched off-site playbook.

## Limitations (When NOT to use)
*   **Do not use** for established sites. For ongoing link acquisition, use [kirby-off-page-seo](../../kirby-off-page-seo/SKILL.md).
*   **Do not use** for deployment staging or EMDs. Use [kirby-seo-deployment](../../kirby-seo-deployment/SKILL.md).
*   **Do not use** if the site is already indexed. This methodology relies on a specific "Day 1" forced-index spike.

## Stage 1: Interactive Intake

Prompt the user for the following 4 pieces of information (if not running in `-y` or non-interactive mode. If non-interactive, use best-guess defaults from context):
1. **Brand Name & Core Offering** (Used to slugify the path: apply NFKC normalization, then strictly match regex `^[a-z0-9]([a-z0-9-]{0,63})$`. Reject empty or traversal paths like `../`).
2. **Target Audience & Core Competitors**
3. **Launch Scale Target** (e.g., 10-page MVP vs. 1,000-page programmatic build)
4. **Target Location or Target Domain**

**Idempotency & Rerun Policy:** If the target workspace directory (always use absolute paths to avoid bare `./` traversal risks) already exists, pause and ask the user whether to `resume` (skip existing files), `clobber` (overwrite), or `abort`. Even in non-interactive mode, `clobber` requires explicit user confirmation to prevent data loss. Default to `resume` if no input is provided.

### 1.1 Primary Association Lock-In (Pre-Launch Gate — decide BEFORE Day 1)

*Source: Charles Floate (LLM Mastery). Net-new doctrine for this skill — no canonical twin.*

* **The Rule:** Anchor the brand to **one primary entity association** during launch (e.g., PressWiz = "link building marketplace", not broad "SEO services") before expanding to secondary services. Core topical pages publish on-site with the Day 1 flip (within the Stage 2 Top 5 cap), but external citations and guest posts focus **exclusively** on reinforcing the single primary association.
* **The 10x Reversal Cost:** Misclassification (e.g., an email management tool absorbed as an "email newsletter" tool) takes a reported ~10x the effort to correct due to model caching and reinforcement weights (directional, single-source).
* **Research Gate (mandatory):** Before scaffolding Stage 2, decide the primary association from competitor-category gaps and the intended revenue core — this is the single highest-leverage launch decision, and the doctrine cuts both ways: locking the *wrong* association is itself the 10x mistake. In non-interactive mode, derive the association from intake context and record it as `ASSUMED` for later human confirmation.
* **Output:** Record the chosen primary association + 2 rejected alternates in `/semantics/semantic_triples.md` so later stages cannot silently drift.

## Stage 2: On-Site Groundwork (Workspace Scaffolding)

Create the `[brand-slug]-launchpad/` directory (using absolute paths). **Before creating any files, explicitly echo the resolved absolute path to the user.** Populate it:

*   **`/architecture/`**
    *   `site_structure.md`: Define the URL taxonomy and navigation tree.
    *   `topical_map.md`: Expand the core offering into a long-tail, high-intent keyword map.

*   **`/semantics/`**
    *   `schema.json`: Write valid JSON-LD markup representing the entity. Use `LocalBusiness` if a location is provided, otherwise `Organization`. Use single-object or `@graph`. **Must substitute all placeholders (no `example.com`).**
    *   `semantic_triples.md`: Define the subject-predicate-object entity relationships.

*   **`/content/`**
    *   *Warning:* Do not blindly generate 1,000 files. Cap generation at the **Top 5 core pages**. Output the remainder of the topical map as `content_manifest.csv` and prompt the user for confirmation before bulk creation.
    *   For the core pages, scaffold `.md` stubs with H1/H2 structures and semantic guidelines.

### 2.1 Comparison-Page Launch Staging (Self-Contained Twin of `kirby-aiseo-skill` Module 2 §2.40)

> **Self-contained duplicate (twin).** The doctrine block below replicates `kirby-aiseo-skill` Module 2 §2.40 verbatim per the duplication policy; update both twins in the same change. The application layer after it is launch-specific and not part of the canonical block.

**Doctrine block (verbatim from canonical):**

* **Listicle Demotion:** Standard "top 10" listicles saw significant demotions in recent core updates due to programmatic AI-spam saturation. Deprecate thin listicle generation as a default format.
* **Comparison Pages ("X vs. Y") are the premier format for shifting LLM consensus** — a single syndicated comparison article can shift a Google AI Overview for its head term. Integrates with §2.6 (mandatory competitor context) and §2.10 (high-intent comparison hubs).
* **The 99%/1% Consensus Rule:** Mirror 99% of established SERP consensus in the comparison to satisfy algorithmic consensus filters, then position the brand as the superior solution within the remaining 1%. Weak 1% differentiation degrades into me-too content — the differentiator must be a checkable fact (price, SLA, accreditation), not adjectives.
* **Caution (defamation exposure):** Comparison claims must be verifiable and current. Attribute disputed claims to their source; avoid asserted superiority on subjective dimensions.

**Application layer — launch staging:**

* *Reference note:* `§2.6` / `§2.10` inside the doctrine block above refer to `kirby-aiseo-skill` Module 2 sections (comparison architecture and high-intent hubs), not to this file's stage numbering.
* **On-site (within the Stage 2 Top 5 cap):** stage **one** flagship comparison page — not one per money page — in honest "X vs. Y" hub format where the brand appears as *one option among competitors* with checkable facts (price, SLA, accreditation). Never self-award: 85% of AI brand citations for commercial and transactional queries originate from third-party domains, and first-party "we win" comparisons are discounted as self-reviews. Reuse a deprecated listicle slot; do not add file count.
* **Off-site (where consensus actually shifts):** the syndicated third-party comparison placement reinforcing the §1.1 primary association belongs to Stage 3.2 velocity-matched links and [kirby-off-page-seo](../../kirby-off-page-seo/SKILL.md) — do not invent outreach here.
* **Guardrail:** Any comparison page that positions the brand as superior requires explicit user confirmation before publishing (defamation caution in the doctrine block; claims must be verifiable and current).

## Stage 3: The "Zero to 100" Off-Site Playbook

The core mechanic is to build the *entire* site in a **non-indexed staging environment**, then flip it live on "Day 1" and force-index via GSC sitemaps alongside a massive trust-signal blast. Generate the playbook and save it explicitly to `[brand-slug]-launchpad/execution_playbook.md` with this strict timing:

### 3.1 Entity Stacking & Forced Indexing (Day 1-3)
*   Provide a checklist for social profiles, citations, reference sites, and directories. These must go live in **1-3 days** to spike the crawl rate on the new site.
*   Mandate forced indexing (via GSC, press releases, or sameAs schema).
*   **Guardrail:** You MUST require explicit user confirmation before executing any "massive trust-signal blast" or "forced indexing" actions.

### 3.2 Velocity-Matched Links (Month 1)
*   Calculate a first-month backlink target based on the Launch Scale Target using this explicit table:
    *   10 pages ➔ 5 links
    *   100 pages ➔ 20 links
    *   1,000 pages ➔ 150 links
*   *Note to user:* Surface the assumption that link velocity strictly scales with page count. Building 100 links to a single homepage on a new site will tank the root domain. Distribute links evenly.
*   Provide strategies for reverse-engineering competitor link overlap.

### 3.3 AI Visibility
*   Detail tactics to trigger brand consensus in ChatGPT, Claude, and AI Overviews.
*   **AIO Parasite Incubation:** While the fresh domain sits out the sandbox and AI Overview quarantine, capture head-query AI Overview citations on parasite platforms and bridge the traffic to the owned domain — full strategy, 5-year longevity maintenance, and handover timing in `./module_1_aio_incubation_longevity.md`.

### 3.4 Fresh-Domain AI Overview Blackout (Condensed Routing Note — *not* a twin; full doctrine: `kirby-aiseo-skill` Module 1 §1.20)
*   Freshly registered domains hit a reported **24–72 hour anti-spam holding period** in Google AI Overviews (first documented on exact-match domains; treat as directional for any fresh domain), then rank normally after 1–2 weeks of indexation. Scoped to Google AI Overviews only — ChatGPT/Claude visibility (§3.3) is not quarantine-gated.
*   **Measurement blackout:** do not judge AI Overview visibility for the launch domain before the end of week 2 post-flip; earlier readings measure the quarantine, not the content. Do not delay the Day 1 flip waiting out the window.

## Stage 4: Advanced Expansion

*   Once the root domain hits 10k monthly organic traffic (the baseline threshold), deploy satellite microsites and parasite SEO for long-tail domination.
*   **Parasite handover:** At the baseline threshold, execute the incubation→ownership reversal from `./module_1_aio_incubation_longevity.md` §1.4 (parasite assets become citations; maintenance budget shifts to the owned domain).
*   **Guardrail:** You MUST require explicit user confirmation before executing any "satellite microsites" or "parasite SEO" tactics to ensure compliance with terms of service and risk tolerance.

## Execution Rules
- **Cross-Skill Routing:** For off-page execution details, see the [kirby-off-page-seo](../../kirby-off-page-seo/SKILL.md) skill. For deployment rules, refer to [kirby-seo-deployment](../../kirby-seo-deployment/SKILL.md). For the canonical doctrine behind §2.1 (comparison pages), §3.4 (fresh-domain quarantine), and entity trinity work, refer to [kirby-aiseo-skill](../../kirby-aiseo-skill/SKILL.md).
- **Hollow Shell Rule:** The full logic lives here in `00_dispatcher.md`. Never alter `../SKILL.md`.
