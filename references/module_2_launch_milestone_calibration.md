# Module 2: Launch Milestone Calibration to Google's Empirical Timing Benchmarks

*Source: Google's official processing-pipeline benchmarks (Gary Illyes, Search Central Live Deep Dive Europe, Barcelona, Oct 2, 2026; analyzed by Edward Sturm, Ep. E1192). Full Matrix, confidence tiers, and forecasting math: `../../kirby-seo-timing-benchmarks/SKILL.md`. This module recalibrates the Zero-to-100 launch calendar (Stages 3–4) so Day 1–3 / Month 1 expectations match measured Google behavior instead of folklore.*

## 2.1 The Calibration Problem

The Zero-to-100 methodology compresses launch expectations into aggressive windows ("force-index on Day 1–3"). A **zero-authority fresh domain** sits at the bottom of Google's scheduler priority ladder: the typical Matrix values apply, and the slow tail — not the typical case — is the realistic planning risk. Calibrating prevents two launch-phase failure modes: (a) declaring the flip failed while Google is still inside its normal windows, and (b) mistaking a quality/authority verdict for a queue delay and burning effort on resubmission spam.

## 2.2 Calibrated Launch Milestone Table

Anchored to the Matrix (tier values in `../../kirby-seo-timing-benchmarks/SKILL.md` Reference 01):

| Milestone | Folklore expectation | Calibrated expectation (fresh domain) | Calendar implication |
|---|---|---|---|
| New URL discovery post-flip (sitemap + GSC request) | Hours | **~20h typical; days-to-weeks on a cold domain** | Day 1–3 "forced indexing" activities are *inputs*, not guarantees; verify discovery at Day 3, not hour 3 |
| Sitemap processing | Immediate | **~24h typical; up to 14 days slow tail** | Do not resubmit inside 14 days; one clean submission at flip |
| End-to-end indexing (post-crawl) | Same-day | **from ~1.5h pipeline latency — but only after discovery+crawl fire** | If crawled but not indexed past 14–21 days, it is a quality gate, not a queue (route: Reference 03 §3.3) |
| Title/snippet correctness in SERPs | Days | **1–2d after recrawl; recrawl itself runs ~30d** — fresh domains have no hot crawl cadence yet | Verify SERP rendering at week 4–6, not day 2 |
| Canonical consolidation (if staging→live URL flips or www variants exist) | Immediate | **1–3 weeks under clean signals; months if conflicting** | Purge all staging-era canonical/link conflicts *before* flip (checklist: `../../kirby-seo-deployment/SKILL.md` Module 20 §20.2) |
| AI Overview visibility (fresh domain) | Immediate | 24–72h quarantine + 1–2 weeks normalization (§3.4 of this skill's dispatcher / `../../kirby-aiseo-skill/SKILL.md` §1.20) | Blackout judgment until end of week 2 (unchanged doctrine) |

## 2.3 Stage 3 Timing Recalibration

- **Day 1–3 (§3.1 Entity Stacking & Forced Indexing):** keep the activity bundle (profiles, citations, sameAs, GSC requests) — these raise scheduler priority and shorten discovery toward the ~20h typical. But write the execution playbook's success criteria as: *discovery confirmed by Day 3, indexing confirmed by Day 7–14*. A URL undiscovered at Day 14 with clean sitemaps crosses the T2 stall boundary → run the triage protocol (`../../kirby-seo-timing-benchmarks/SKILL.md` Reference 03 §3.2) before any escalation.
- **Month 1 (§3.2 Velocity-Matched Links):** the link table stays; note that fresh contextual backlinks are also a **discovery/velocity lever** (Matrix authority bypass inputs), so early links to deep pages — not just the homepage — shorten their discovery windows (lever doctrine: `../../kirby-seo-timing-benchmarks/SKILL.md` Reference 05 L5).
- **Resubmission discipline:** sitemap resubmission and bulk URL Inspection requests do not override scheduler priority or quality verdicts (anti-patterns: Reference 05 §5.4). One clean pass, then instrument and wait.
- **Stall monitoring:** wire the launch workspace to the two-tier stall thresholds (T1 watch / T2 stalled) — instrumentation spec: `../../kirby-seo-telemetry/SKILL.md` Module 12.

## 2.4 Stage 4 Handoff Implication

The 10k-traffic baseline threshold that unlocks satellite/parasite expansion (Stage 4) is effectively an **authority-bypass threshold**: below it, the site lives on typical Matrix timelines; above it, windows compress. Expect the 0→baseline climb to be governed by normal content/authority timelines (multi-month), and do not read Matrix slow-tails on young assets as penalties — they are default scheduler priority until earned otherwise (bypass doctrine: Reference 01 §1.3).

## 2.5 Guardrail

This module calibrates *expectations and verification schedules only*. It does not license delaying the Day 1 flip (the quarantine/blackout doctrine in §3.4 stands), and it does not replace the confirmation gates on trust-signal blasts or forced-indexing actions.
