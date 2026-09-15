# Microsoft Sentinel Operations — STYLE-GUIDE.md

**Status:** Adopted before any part is authored or reviewed, per NESHBOY SOC Professional Library convention.
**Applies to:** every part, appendix, and diagram in this book.
**Audience:** every writer and reviewer working on this book.
**Parent convention:** `detection-engineering-handbook/release-v2/STYLE-GUIDE.md` (DEH). This document adapts DEH's contract rather than replacing it — where a section below says "unchanged from DEH," the DEH text is normative and this file exists only to confirm it carries forward. Where this book's subject matter genuinely differs (a SaaS platform with its own portal, pricing, and release cadence, instead of a query language that changes on standards-body time), this document says so explicitly and supplies its own rule.

## Why this document exists, and why it's not just a copy of DEH's

DEH's style guide was written to fix a specific, diagnosed defect: 55 independent single-pass agents with no shared contract, producing five shapes for one callout box. This book has one author lineage and inherits DEH's contract directly, so that specific failure mode isn't the risk here. The risk this book actually carries is different: **DEH governs content about a query language and a detection technique, both of which change slowly and get validated against real telemetry the author has in hand. This book governs content about a commercial SaaS platform whose rule types, portal, and pricing tiers change on a vendor release cycle the author does not control, and it does so with no real tenant to validate anything against.** Every adaptation below traces back to one of those two differences. Nothing here is adapted for its own sake.

**"Must"** means a PR gets rejected if it doesn't comply. **"Should"** means deviate only with a reason recorded in the PR description. **"Avoid"** is a strong default a reviewer can override with justification.

---

## 1. Voice and Tone

**Unchanged from DEH §1** — the core rule, the banned-filler list and its two-test exception (does the phrase carry information, or does it just sound like it does), the worked GOOD/BAD examples, and the sentence/paragraph mechanics all apply exactly as written in DEH `STYLE-GUIDE.md` §1. Re-read that section before writing; it is not reproduced here to avoid two copies drifting apart.

One addition specific to this book's subject matter:

### 1.1 Naming the platform without marketing it

Microsoft's own product pages describe Sentinel/Defender in exactly the register DEH §1.2 bans — "unified," "seamless," "AI-powered," "best-in-class." Quoting a Microsoft Learn page verbatim for a specific, falsifiable technical claim is fine and expected (see §9 below on the `OFFICIAL REFERENCE` evidence class); repeating Microsoft's own marketing adjectives as if this book endorses them is not. If a source page says a feature provides "a seamless, unified experience," extract the falsifiable claim underneath it (what actually happens, what data actually moves, what a user actually sees) and cut the adjective, exactly as DEH §1.2 already instructs for any other source of marketing language.

> BAD: "The Microsoft Defender portal delivers a seamless, unified security operations experience that empowers SOC teams."

> GOOD: "Onboarding a Sentinel workspace to the Defender portal moves Sentinel's own incidents into the same queue Defender XDR already populates from Defender for Endpoint, Defender for Identity, Defender for Cloud Apps, and Defender for Office 365 — one queue, one correlation engine, and (see Part 13) one set of automation-rule behaviors that differ from what the same rule did in the Azure portal."

---

## 2. Heading Level Conventions

**Unchanged from DEH §2** — H1 for part title only, H2 for numbered major sections, H3 for named subsections (a specific rule type, a specific table, a specific feature walkthrough), H4 rare and never nested deeper. `## Why this part exists` remains mandatory, unnumbered, and first. Section titles in sentence case; part titles in title case with an em dash (`# Part 4 — Analytics Rules I: Scheduled and Near-Real-Time (NRT) Rules`).

One addition: when a part gives a named feature its own `###` walkthrough, format the heading as a plain feature name, not a sentence — `### Fusion — advanced multistage attack detection`, not `### The Fusion rule type detects advanced multistage attacks`. This mirrors DEH §2's Event-ID heading rule (`### 4624 — An account was successfully logged on`) applied to a feature name instead of a numeric ID, for the same reason: the heading is a label a reader scans, not a claim they read.

---

## 3. Code Block Conventions

**Base table unchanged from DEH §3** for every language DEH already covers (KQL, YAML/Sigma, bash/PowerShell, JSON/XML/text for raw excerpts, Mermaid). This book adds the platform-deployment languages DEH never needed:

| Language / platform | Fence tag | Notes |
|---|---|---|
| ARM template (analytics rule, workbook, or playbook export) | `` ```json `` | An ARM template is JSON; don't invent an `arm` tag. Every ARM example must state which resource type it's exporting (`Microsoft.SecurityInsights/alertRules`, `.../automationRules`, etc.) in the sentence above the block. |
| Bicep | `` ```bicep `` | |
| Logic Apps workflow definition (a playbook's own JSON) | `` ```json `` | Disambiguate from a generic ARM template in the sentence above the block — "The following is a playbook's Logic Apps workflow definition..." |
| Azure CLI | `` ```azurecli `` | Never bare `bash` for a command that is specifically `az ...` — use `azurecli` so a reader can tell at a glance this isn't portable shell. |
| PowerShell (Az module) | `` ```powershell `` | Same tag and rule as DEH §3 — never `ps1`. |
| KQL (Sentinel/Defender) | `` ```kql `` | **This book rarely shows a full KQL query.** Per `BOOK-INDEX.md`'s structural decision #4, a KQL block in this book either (a) shows only the Sentinel-specific extension DEH Part 25 doesn't cover — a watchlist lookup function, an entity-mapping expression, a data-lake KQL job — or (b) is a short illustrative fragment inside a larger ARM/JSON rule definition. A block showing a full, freestanding detection query belongs in DEH, not here; if a draft accumulates one, that's a signal that content is misplaced, not a green light to duplicate it. |

Additional rules, all unchanged from DEH §3: every fence tagged; every real (non-conceptual) example preceded by a platform/version-targeting sentence and followed by a stated limitation or a pointer to the callout that supplies one; inline code (single backtick) for feature names, table names, and rule-type names used as identifiers mid-sentence (`` `SecurityIncident` ``, `` `SentinelHealth` ``, `` `AnomalyScore` ``); the `CONCEPTUAL SAMPLE — <clause>` label for teaching-only, invented, or unverified-against-a-live-tenant examples, used liberally in this book given §9's honesty constraint.

---

## 4. Notation Conventions: Rule Types, Tables, and Portal Terms

DEH §4 fixes "Event ID 4624 on first use, bare 4624 after" because Windows Event IDs are the recurring vocabulary of that book. This book's recurring vocabulary is different — analytics rule types, table names, and the two-portal split — so it gets its own version of the same discipline instead of reusing DEH's Event ID rule verbatim.

- **Rule types, on first use per chapter:** full name plus, in parentheses, the one distinguishing fact that matters operationally — `Near-real-time (NRT) rules (fixed one-minute evaluation cadence, limited subset of scheduled-rule features)`, `Fusion (Advanced multistage attack detection — single instance, not customizable, unavailable once Defender XDR incident integration is on)`. Bare `NRT` or `Fusion` is fine after that first expansion within the same chapter.
- **Table names:** always inline-coded, always exact case — `` `SecurityIncident` ``, `` `BehaviorAnalytics` ``, `` `Anomalies` `` — never paraphrased ("the incident table") without having named the real table at least once nearby.
- **The two portals:** always "the Azure portal" and "the Microsoft Defender portal" in full on first mention per chapter (never "Azure" or "Defender" alone to mean the portal — both words are also product names and the ambiguity is exactly the kind of confusion Part 2 exists to resolve). "The Defender portal" is an acceptable short form after first mention in a section. Never invent an acronym for either.
- **Feature preview/GA state:** state it explicitly the first time a feature is named in a chapter — "ML Behavior Analytics rules (currently in Preview)," "the UEBA behaviors layer (a separately-enabled, recently introduced capability)" — using whatever state Microsoft's own documentation states as of the last-verified date in the unit's front matter. Never assert GA status without having checked it in the source cited for that claim.

---

## 5. MITRE ATT&CK ID Formatting

**Unchanged from DEH §5** in full — `T1558.003 (Kerberoasting)` on first reference per section, bare ID after, uppercase `T`, no truncated sub-technique suffixes, standalone `**MITRE:**` lines always spelled out regardless of prior mentions, never an invented mapping. This book uses MITRE IDs less often than DEH (most of this book's content is platform mechanics, not technique detection), but every instance follows the same rule with no platform-specific exception.

---

## 6. Callout Boxes — Exact Templates

All nine of this book's callouts — DEH's eight plus this book's own ninth — use DEH's base shape: a blockquote opened with a bold label line, never a heading, never nested, sitting inline in the flow rather than as a separate jump target.

### 6.1–6.8 — DEH's eight callouts, unchanged

**Detection Autopsy, Hunter's Note, Engineering Reality, Blind Spot, False Positive Trap, Detection Test, SOC Management View, What Would Change My Mind** — exact templates as specified in DEH `STYLE-GUIDE.md` §6.1–§6.8. Use them as written. Two usage notes specific to this book:

- **Detection Autopsy** and **Detection Test** apply where this book discusses actual rule or automation logic (Parts 4, 5, 13, 14) — not in a part about, say, workspace architecture or cost tiers, where there's no rule to dissect or test. Forcing one into every part to hit a quota is exactly the over-boxing DEH §6.9 already warns against.
- **False Positive Trap** in this book as often names a *platform-behavior* false positive as a detection-logic one — an automation rule firing on an incident-update batching artifact (Part 13), not just a legitimate user tripping a query's threshold.

Worked example, adapted for this book's subject matter (an NRT-rule Engineering Reality, parallel in structure to DEH's own worked examples):

```
> **Engineering Reality**
> NRT rules run once every minute, fixed — there is no lookback-vs-frequency tuning knob the
> way there is for a scheduled rule (see Part 4, and DEH Part 25 §3 for why that mismatch
> matters at all). What this actually costs you: an NRT rule's query has to be cheap enough to
> finish comfortably inside a one-minute window on every run, forever, and a query that's "slow
> but fine" as an hourly scheduled rule can start missing its own cadence as data volume grows
> — silently degrading to something closer to a scheduled rule's latency while still being
> billed and reasoned about as if it were near-real-time.
```

### 6.9 — PRODUCT VERSION NOTE (new)

The one callout DEH doesn't need and this book can't do without. Names a specific platform fact — a feature's availability, a pricing figure, a rule type's dependency on another feature being on or off, a published deprecation or retirement date — as accurate **as of a stated date**, and tells the reader exactly how to re-check it themselves rather than asking them to trust the book indefinitely.

```
> **PRODUCT VERSION NOTE (as of <date>)**
> The specific, falsifiable platform fact, stated plainly. The Microsoft Learn page (or
> equivalent official source) it's drawn from, named in prose (not just a footnote). One
> sentence on what changes for the reader if this fact is now out of date.
```

Worked example:

```
> **PRODUCT VERSION NOTE (as of 2026-09-15)**
> Microsoft Sentinel in the Azure portal is scheduled for retirement on March 31, 2027; after
> that date, Sentinel is only available in the Microsoft Defender portal, and every workspace
> still in the Azure portal is redirected automatically. Microsoft's own "What's new" and
> overview pages carry this date as of this writing. If you're reading this after that date (or
> your organization has already migrated), treat every Azure-portal-specific screenshot,
> procedure, or menu path in this book as historical context for understanding a migration
> that has already happened to you, not as a live how-to.
```

Rules specific to this callout:

- The date in the label is **mandatory**, not optional — this callout without a date is a lint failure, since "as of this writing" with no anchor is exactly the kind of unfalsifiable claim DEH §1.2 already bans for a different reason.
- Cite the actual source by name in the body (Microsoft Learn page title or URL), not just "Microsoft's documentation" — a reviewer re-verifying this claim needs to know where to look.
- A PRODUCT VERSION NOTE is not a substitute for a **What Would Change My Mind** box — use both where a claim is both fast-moving *and* a judgment call the book is making on top of the fact (see the worked What Would Change My Mind example in §6.10 below, which follows directly from this section's Fusion/Defender-portal fact).
- Every unit whose `depends_on` cites a specific limit, price, or availability rule must carry at least one PRODUCT VERSION NOTE for that claim — this is enforced at review, per `BOOK-INDEX.md`'s Production Model addition requiring a checked-URL-and-date record from the reviewer.

Worked What Would Change My Mind, chained from the PRODUCT VERSION NOTE example in §6.9, showing how the two callouts divide labor (fact vs. judgment):

```
> **What Would Change My Mind**
> This book treats "plan for the Defender portal as the only long-term option" as the correct
> default recommendation for any team still running Sentinel in the Azure portal today (Part
> 16). If Microsoft reversed the retirement decision, extended the date substantially, or
> shipped a durable Azure-portal-parity commitment beyond March 31, 2027, the recommendation
> would need to soften from "migrate now" to "migrate on your own schedule" — a materially
> different program-management message to give a SOC manager planning a multi-quarter project
> around this date.
```

### 6.10 Callout usage density

Same guidance as DEH §6.9, with this book's own typical mix: a part discussing an actively-evolving feature (Parts 5, 11 §UEBA-behaviors-layer, 12, 13, 16, 17) typically carries one PRODUCT VERSION NOTE and, where the fact feeds a judgment call, one paired What Would Change My Mind; a part discussing stable architecture (Parts 2's workspace model, 6's entity-mapping mechanics, 8's workbook mechanics) may carry none. A part stacking a PRODUCT VERSION NOTE onto every paragraph is over-boxed exactly as DEH warns — most platform facts in a given part are stable; only the ones actually on a vendor's active-change list earn the callout.

---

## 7. Content-Level Tags

Format locked to `**[TAG]**`, same rule as DEH §7 — bold, brackets, all caps, start of the paragraph or subsection it governs, never a heading, never doubled on one paragraph.

| Tag | Use for | Do not use for | Relationship to DEH |
|---|---|---|---|
| `[CONCEPT]` | Foundational "what and why" for a platform feature or architectural piece, no assumption the reader acts on it directly. | A specific configuration step, query, or setting — that's a lower tag. | Unchanged from DEH. |
| `[ANALYST]` | Triage/investigation-facing: what an incident in the unified queue means, what an entity graph shows, when to check a watchlist, how to read a workbook panel. | Building or tuning the rule/automation/watchlist itself — that's `[SENTINEL ENGINEER]`. | Same role as DEH's `[ANALYST]`; scope re-centered on the unified incident queue instead of a single alert. |
| `[SENTINEL ENGINEER]` | Rule logic, entity mapping, watchlist curation, automation-rule and playbook configuration, and the design tradeoffs behind them. | Triage guidance for someone who didn't build the rule — that's `[ANALYST]`. Workspace/ingestion/retention plumbing — that's `[ENGINEERING]`. | **Renamed from DEH's `[DETECTION ENGINEER]`.** Deliberately broader: this book's rule-builder role also owns automation and reference data, which DEH's narrower tag never had to cover. |
| `[THREAT HUNTER]` | Hypothesis-driven exploration inside Sentinel/Defender: hunting queries, bookmarks, notebook-based pivots, UEBA-anomaly-led hunts. | A named, deployable detection rule — tag the finished rule `[SENTINEL ENGINEER]` and keep the hunting narrative separate. | Unchanged from DEH. |
| `[ENGINEERING]` | Workspace architecture, connectors, Data Collection Rules, table tiering, retention mechanics, ingestion cost and performance — the platform a rule or dashboard runs on top of. | Rule logic itself. | Unchanged from DEH — DEH's own definition ("the plumbing that has to exist before any detection or hunt can run") already fits this book's ingestion/workspace/tiering content without modification. |
| `[SOC MANAGEMENT]` | Licensing/commitment-tier decisions, staffing for platform operations, the Azure-portal-retirement migration as a program-management problem, risk-acceptance on retention/tuning tradeoffs. | Any paragraph that starts specifying a query or a setting — split it. | Unchanged from DEH. |

Tagging guidance, unchanged from DEH: `[CONCEPT]` is the only tag allowed to open a section before any other tag appears; most `##` sections carry more than one tag across their subsections; the two pairs writers most often confuse are `[SENTINEL ENGINEER]` (the rule/automation/watchlist itself) vs. `[ENGINEERING]` (the platform it runs on), and `[ANALYST]` (working an incident) vs. `[THREAT HUNTER]` (looking without a triggered incident) — when in doubt, ask which column in the table above the content actually falls under.

---

## 8. Table Conventions

**Unchanged from DEH §8** in full: lead-in sentence stating what decision the table supports; header row as short capitalized noun phrases; left-aligned text columns; fragments not full sentences in cells; em dash for "not applicable," never a blank cell; inline code for field/table/rule-type names inside cells; MITRE IDs in their own column following §5's rules; tables built from invented/illustrative data marked `(CONCEPTUAL SAMPLE)` in the caption.

One addition: a table comparing behavior across the Azure portal and the Defender portal (there will be several, given Part 16's scope) must use exactly two columns headed `Azure portal` and `Defender portal`, in that order, with an explicit `(retiring 2027-03-31)` qualifier on the `Azure portal` header the first time such a table appears in a chapter — consistent labeling matters more here than almost anywhere else in the book, since a reader skimming a table out of context is the most likely reader to miss which portal a row describes.

---

## 9. Figures and Evidence Classification — the Honesty Constraint

This section is this book's largest deviation from DEH, because the constraint driving it — no real Sentinel tenant, no real Log Analytics workspace, no captured screenshot from a live system — is the central fact governing what this book is allowed to claim as evidence anywhere in its 18 parts. Get this section wrong and the book's factual credibility fails wholesale, not locally.

### 9.1 The same four evidence classes DEH defines, with this book's actual usage pattern stated up front

| Tag | Meaning (unchanged from DEH) | Used in this book? |
|---|---|---|
| `CONTROLLED LAB EXAMPLE` | Captured in a lab the author built specifically to generate this evidence. | **Not in this book's initial release.** No Sentinel tenant exists to build that lab in. Retained in this table only so the definition is ready the day one exists — see §9.4. |
| `REAL LAB EXAMPLE` | Captured from a real, pre-existing environment observing organic activity. | **Not in this book's initial release**, for the same reason. |
| `OFFICIAL REFERENCE` | Sourced from vendor documentation, reproduced or closely adapted with attribution. | **This book's primary evidence class.** Nearly every screenshot, schema diagram, or table reference in this book, if it exists as a rendered figure at all, is this tag — adapted from a cited Microsoft Learn page. |
| `CONCEPTUAL` | An illustrative diagram with no claim of being captured from a real system. | **This book's other primary evidence class.** Every architecture sketch, data-flow diagram, and portal-comparison illustration that isn't a direct reproduction of an official diagram. |

### 9.2 Caption format — unchanged mechanically from DEH §9.2

```
**Figure N.M — [Short descriptive title].** *[Evidence class tag].* One to two sentences: what
the figure shows and what it's evidence of, or — for CONCEPTUAL diagrams — what it illustrates
rather than proves. If OFFICIAL REFERENCE: full source citation (page title, URL, retrieval
date) — mandatory in this book, not optional, since OFFICIAL REFERENCE carries more of this
book's evidentiary weight than it does in DEH.
```

Worked examples specific to this book:

```
**Figure 5.1 — Analytics rule type decision tree.** *CONCEPTUAL.* Illustrates the decision
sequence an engineer walks through when choosing a rule type (Scheduled vs. NRT vs. Fusion vs.
Anomaly vs. Custom Detection) based on latency need, customizability need, and Defender-portal
onboarding status. This is a structural sketch built from this book's own reading of the
official rule-type documentation cited in Part 5's References list — not a capture of any
Sentinel UI screen, and not a reproduction of an official Microsoft diagram.
```

```
**Figure 17.2 — Analytics tier vs. data lake tier retention and cost shape.** *OFFICIAL
REFERENCE.* Adapted from Microsoft Learn, "Log retention tiers in Microsoft Sentinel"
(learn.microsoft.com/azure/sentinel/log-plans), retrieved 2026-09-15. Reproduces the two-tier
retention model (analytics tier: 90-day default interactive retention, extensible to two years;
data lake tier: cost-effective long-term retention for secondary security data) as documented
at the retrieval date — see the paired PRODUCT VERSION NOTE in Part 17 for why this replaced an
older four-tier model and what to check if this figure looks out of date.
```

### 9.3 Pending placeholder format — unchanged from DEH §9.3, with one added restriction

```
> **[FIGURE PENDING — target evidence class: <OFFICIAL REFERENCE | CONCEPTUAL>]** What the
> figure will show, one sentence. Why it isn't captured/rendered yet, one sentence. What claim
> in the surrounding text it would support.
```

**This book's pending-placeholder target evidence class is restricted to `OFFICIAL REFERENCE` or `CONCEPTUAL` only.** A pending placeholder targeting `CONTROLLED LAB EXAMPLE` or `REAL LAB EXAMPLE` is a lint failure in this book specifically — see §9.4.

### 9.4 The rule that enforces the honesty constraint

**No unit in this book's initial release may use the `CONTROLLED LAB EXAMPLE` or `REAL LAB EXAMPLE` evidence-class tag, and no pending placeholder may target either one.** This is stricter than DEH, where all four classes are live options a reviewer chooses among per figure. Here, the choice is made once, at the book level, by the fact stated in `BOOK-INDEX.md`'s "What this book is" section: there is no tenant to capture evidence from.

If a future contributor stands up a real Sentinel tenant and wants to add a `CONTROLLED LAB EXAMPLE` figure to a later edition, that's a welcome, explicit change to this book's evidence base — but it's a change to be made deliberately, recorded in a revision note at the top of the affected part (front-matter `last_validated` bump plus a one-line note on what became available), not a tag quietly used because it seemed to fit. A reviewer who finds `CONTROLLED LAB EXAMPLE` or `REAL LAB EXAMPLE` anywhere in a draft for this book's initial release should treat it the same way a DEH reviewer treats an invented MITRE mapping in DEH §5: reject it, don't soften it, and ask where the claimed evidence actually came from.

---

## 10. Diagram Rendering Requirement

**Unchanged from DEH §10.** Every Mermaid block gets rendered to a static image (SVG preferred) and committed alongside the source, referenced with a real evidence-class tag per §9.2 — almost always `CONCEPTUAL` in this book, per §9.1's usage pattern, unless the diagram is a literal reproduction of an official Microsoft architecture diagram, in which case it's `OFFICIAL REFERENCE` with full citation. The Mermaid source stays in the file as the editable record. A unit isn't review-complete with an unpaired `mermaid` fence.

---

## 11. Review Checklist

Same enforcement role as DEH §11 — work from this list, not from vibes. Items 1–8 are DEH's checklist, applied to this book's own tags/callouts; items 9–11 are additions specific to this book's evidence constraint and fast-moving subject matter.

1. **Voice:** any banned filler present without being rewritten (DEH §1.2)? Any Microsoft marketing adjective repeated uncritically instead of extracted into a falsifiable claim (§1.1)?
2. **Headings:** correct level nesting, `## Why this part exists` present, no heading used as a bold-line substitute?
3. **Code blocks:** every fence tagged correctly per §3's extended table; every real example framed with a targeting sentence and a stated limitation; no freestanding full detection-query KQL block that belongs in DEH instead?
4. **Notation:** rule types, table names, and portal names expanded on first use per chapter per §4; no bare "Azure" or "Defender" used ambiguously to mean the portal?
5. **MITRE IDs:** per DEH §5, no exceptions.
6. **Callouts:** correct label and structure for all nine types (§6); PRODUCT VERSION NOTE carries a date and a named source every time; density not excessive relative to how fast-moving the part's actual subject matter is (§6.10)?
7. **Tags:** every `##`/`###` subsection carries at least one of the six tags in §7's table, correctly chosen per the "which column does this fall under" test, no paragraph carrying two?
8. **Tables:** lead-in sentence present, no blank cells, portal-comparison tables use the exact `Azure portal` / `Defender portal` header convention with the retirement qualifier on first use per chapter (§8)?
9. **Evidence classes:** does every figure use only `OFFICIAL REFERENCE` or `CONCEPTUAL` (§9.1, §9.4)? Does every `OFFICIAL REFERENCE` figure carry a full citation with a retrieval date? Is there a `CONTROLLED LAB EXAMPLE` or `REAL LAB EXAMPLE` tag anywhere that needs to be rejected outright?
10. **Fact-checking record:** for every unit citing a specific limit, price, availability rule, or date, does the reviewer's sign-off record the source URL and the date it was checked, per `BOOK-INDEX.md`'s Production Model addition?
11. **Depth and currency check:** does this unit's technical depth match sibling units covering comparable scope (DEH §11 item 10, unchanged)? Separately and additionally: is there a claim in this unit that reads as settled architecture but is actually a preview feature, a recently-changed default, or a fact with a published future change date — and if so, does it have a PRODUCT VERSION NOTE?

Match this guide over inventing local precedent. Any deviation a reviewer approves gets recorded as a documented change to this file, exactly as DEH §11 requires of its own guide.
