# Microsoft Sentinel Operations

**Workspace Architecture, Analytics Rules, Automation, and Cost Governance — From Query to Platform**

📄 **[Download the full PDF](./Microsoft_Sentinel_Operations.pdf)** — 205 pages, ~79,000 words across 18 parts.

Part of the **NESHBOY SOC Professional Library**, alongside [SIGNAL TO ACTION: The Complete SOC Playbook Handbook](https://github.com/neshboy/soc-playbook-handbook), [The Detection Engineering Handbook V2](https://github.com/neshboy/detection-engineering-handbook), and [The SOC Manager's Operating Handbook](https://github.com/neshboy/soc-manager-handbook). Companion volume to *The Detection Engineering Handbook* (DEH) — cross-references throughout use `DEH Part NN` to point back to that book's chapters.

*Microsoft Sentinel Operations* is a platform-operations handbook, not a query-language primer. DEH Part 25 already teaches the Kusto Query Language (KQL) dialect Sentinel and Defender share, and DEH Part 23 already frames the Sigma-vs-native-query tradeoff that produces a Sentinel scheduled rule in the first place — this book assumes both and starts where DEH Part 25 stops: once a KQL query exists, what does it take to run it as a durable, monitored, cost-accounted piece of a production SOC platform — the workspace it lives in, the rule type that hosts it, the incident it feeds, the automation that responds to it, the tier it's billed under, and the portal (there are, as of this writing, two, with one being retired) an analyst uses to see the result. It covers Log Analytics workspace architecture and the Azure-portal/Defender-portal split, data ingestion and table tiering, the full analytics-rule taxonomy (scheduled, NRT, Fusion, Anomaly, ML Behavior Analytics, Custom Detections), entity mapping and the incident model, the detection-content lifecycle (Content Hub, solutions, detection-as-code), workbooks, hunting, watchlists, UEBA, AI-assisted operations (Security Copilot and agentic tooling), automation rules and playbooks, Defender XDR signal convergence, the unified-platform migration, and workspace cost/retention models.

## Reading the book

- **[Microsoft_Sentinel_Operations.pdf](./Microsoft_Sentinel_Operations.pdf)** — the assembled, print-ready book. Start here.
- **[BOOK-INDEX.md](./BOOK-INDEX.md)** — the full part table with per-unit scope, recurring features, and cross-references to DEH, plus a "Key structural decisions and provenance" section recording why the book is 18 parts and not more.
- **[STYLE-GUIDE.md](./STYLE-GUIDE.md)** — the voice, formatting, and figure-evidence-classification contract every part follows: six content tags (`[CONCEPT]`, `[ANALYST]`, `[SENTINEL ENGINEER]`, `[THREAT HUNTER]`, `[ENGINEERING]`, `[SOC MANAGEMENT]`) and nine recurring callouts (DEH's eight — Detection Autopsy, Hunter's Note, Engineering Reality, Blind Spot, False Positive Trap, Detection Test, SOC Management View, What Would Change My Mind — plus this book's own ninth, PRODUCT VERSION NOTE, for platform facts that carry a vendor-set expiration date).

## What's synthetic vs. real — the honesty constraint

This book's author has no real Microsoft Sentinel tenant, Log Analytics workspace, or Defender portal license. Unlike DEH, which draws real captured evidence from an operated home lab, every claim in this book is sourced from Microsoft's own public documentation or presented as a conceptual/architectural illustration — never as a captured screenshot or a validated-in-production result. Of DEH's four evidence classes, this book's initial release uses only two: `OFFICIAL REFERENCE` (Microsoft Learn diagrams, screenshots, and documented behavior, cited with a retrieval date) and `CONCEPTUAL` (architecture/data-flow sketches original to this book, with no claim of being captured from a real system). `CONTROLLED LAB EXAMPLE` and `REAL LAB EXAMPLE` — evidence captured from a lab the author built or a real pre-existing environment — are defined in `STYLE-GUIDE.md` for series consistency and for the day a real tenant exists, but neither tag is used anywhere in this release; `STYLE-GUIDE.md` §9.4 treats either one appearing in a draft as a rejection, not a judgment call. Every fast-moving platform fact (a feature's preview/GA state, a pricing figure, a rule type's availability, a published retirement date) carries a dated **PRODUCT VERSION NOTE** naming the Microsoft Learn source it was checked against, so a reader can re-verify it rather than trust the book indefinitely.

Diagrams are original Mermaid flowcharts, rendered to SVG and committed alongside their Markdown source. This book contains no fabricated screenshots of the Sentinel or Defender UI.

## How it was built

- `build/render_mermaid.py` — renders every embedded ` ```mermaid ` source block under `chapters/` and `appendices/` to SVG via `@mermaid-js/mermaid-cli` and inserts the image reference back into the chapter.
- `build/build_book.js` — parses `BOOK-INDEX.md`'s Part Table, assembles all 18 chapter files into one HTML document (stripping YAML front matter, resolving image paths, colorizing the six content tags), and prints it to PDF via headless Chrome.
- `build/add_watermark.py` — applies the diagonal `neshboy` watermark to every page.

## Rebuilding it yourself

```
cd build
npm install
python render_mermaid.py
node build_book.js
"C:\Program Files\Google\Chrome\Application\chrome.exe" --headless=new --disable-gpu --no-sandbox --no-pdf-header-footer ^
  --print-to-pdf="..\_build\Microsoft_Sentinel_Operations.pdf" "..\_build\book.html"
python add_watermark.py
```

## Repository layout

- `chapters/` — the 18 parts, Markdown source of record. `appendices/` is reserved for the 3 appendix bundles named in `BOOK-INDEX.md`'s Appendix Table (Table/Connector/Rule-Type Quick Reference, Cost and Retention Decision Matrix, Cross-Reference Map to DEH); none are drafted yet, so this release's build intentionally covers only the Part Table.
- `assets/diagrams/` — rendered Mermaid SVGs.
- `build/` — the build/render/watermark tooling above.
- `BOOK-INDEX.md`, `STYLE-GUIDE.md` — cross-cutting project documentation.
