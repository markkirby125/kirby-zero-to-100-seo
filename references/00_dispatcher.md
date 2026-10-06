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

## Stage 4: Advanced Expansion

*   Once the root domain hits 10k monthly organic traffic (the baseline threshold), deploy satellite microsites and parasite SEO for long-tail domination.
*   **Guardrail:** You MUST require explicit user confirmation before executing any "satellite microsites" or "parasite SEO" tactics to ensure compliance with terms of service and risk tolerance.

## Execution Rules
- **Cross-Skill Routing:** For off-page execution details, see the [kirby-off-page-seo](../../kirby-off-page-seo/SKILL.md) skill. For deployment rules, refer to [kirby-seo-deployment](../../kirby-seo-deployment/SKILL.md).
- **Hollow Shell Rule:** The full logic lives here in `00_dispatcher.md`. Never alter `../SKILL.md`.
