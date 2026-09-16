# References

This is the consolidated source list for every external citation used across `chapters/`. It
extends — rather than replaces — this book's existing inline-citation convention (see
`STYLE-GUIDE.md` §9.2 on the `OFFICIAL REFERENCE` evidence class): a citation appears in place,
directly after the claim it supports, in the form `(Organization, "Title," URL, retrieved DATE)`,
and every unique source used anywhere in the book is listed once below with full metadata.

Every URL below was fetched and read directly (not pattern-guessed) before being cited, as part of
a 2026-09-16 citation-enrichment pass. Two categories of fix were made in that pass:

1. **Link format.** This book's original 46 Microsoft Learn citations were bare, unlinked domain
   strings (`learn.microsoft.com/...`, no `http(s)://` scheme, no markdown link syntax). Every one
   is now a clickable markdown link, and every URL was re-fetched on 2026-09-16 to confirm it
   still resolves and still supports the specific claim it's attached to. One citation
   (Part 4 §2.1) pointed at a generic documentation-set root (`learn.microsoft.com/azure/sentinel/`)
   rather than the specific page it meant to cite; it now points at the actual page
   (`create-analytics-rules`) that documents the run-frequency and lookback figures the claim
   depends on.
2. **New citations.** A small number of new citations were added only where a claim is a
   cross-platform security concept rather than a Sentinel-specific feature, and only where a real,
   independently verifiable standards-body source directly supports the specific sentence it's
   attached to (see Part 4 §2.1 and Part 11 §1 below) — MITRE ATT&CK for the vendor-neutral
   technique taxonomy Sentinel's rule wizard maps into, and NIST for User and Entity Behavior
   Analytics (UEBA) as a named security-capability category that predates and exists outside
   Sentinel's own implementation of it.

No citation in this list was constructed by pattern-guessing a URL. Every one was fetched and read
before being added.

## Microsoft Learn / Microsoft Sentinel and Azure Monitor documentation

- Microsoft Learn, "Log Analytics workspace overview," *Azure Monitor documentation*: <https://learn.microsoft.com/azure/azure-monitor/logs/log-analytics-workspace-overview> — cited in Part 2.
- Microsoft Learn, "Design a Log Analytics Workspace Architecture," *Azure Monitor documentation*: <https://learn.microsoft.com/azure/azure-monitor/logs/workspace-design> — cited in Part 2.
- Microsoft Learn, "Log Analytics integration with Power BI," *Azure Monitor documentation*: <https://learn.microsoft.com/azure/azure-monitor/logs/log-powerbi> — cited in Part 8.
- Microsoft Learn, "Azure Workbooks overview," *Azure Monitor documentation*: <https://learn.microsoft.com/azure/azure-monitor/visualize/workbooks-overview> — cited in Part 8.
- Microsoft Learn, "Onboard to Microsoft Sentinel" (quickstart), *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/quickstart-onboard> — cited in Part 2.
- Microsoft Learn, "Connect Microsoft Sentinel to the Microsoft Defender portal," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-onboard> — cited in Part 2.
- Microsoft Learn, "Microsoft Sentinel in the Microsoft Defender portal," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal> — cited in Parts 2 and 16.
- Microsoft Learn, "Transition Your Microsoft Sentinel Environment to the Defender Portal," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/move-to-defender> — cited in Parts 13 and 16.
- Microsoft Learn, "Migrate Microsoft Sentinel incident creation rules to alert grouping in Microsoft Defender," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/migrate-sentinel-incident-creation-rules-alert-grouping> — cited in Part 16.
- Microsoft Learn, "Roles and permissions in the Microsoft Sentinel platform," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/roles> — cited in Part 8.
- Microsoft Learn, "Log retention tiers in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/log-plans> — cited in Parts 3 and 17.
- Microsoft Learn, "Plan costs and understand pricing and billing - Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/billing> — cited in Part 17.
- Microsoft Learn, "Reduce costs for Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/billing-reduce-costs> — cited in Part 17.
- Microsoft Learn, "Create scheduled analytics rules in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/create-analytics-rules> — cited in Parts 4 and 18.
- Microsoft Learn, "Map Data Fields to Microsoft Sentinel Entities," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/map-data-fields-to-entities> — cited in Part 6.
- Microsoft Learn, "Handle Ingestion Delay in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/ingestion-delay> — cited in Part 18.
- Microsoft Learn, "Monitor the health and audit the integrity of your Microsoft Sentinel analytics rules," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/monitor-analytics-rule-integrity> — cited in Part 18.
- Microsoft Learn, "Troubleshooting analytics rules in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/troubleshoot-analytics-rules> — cited in Part 18.
- Microsoft Learn, "Turn on auditing and health monitoring in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/enable-monitoring> — cited in Part 18.
- Microsoft Learn, "Auditing and health monitoring in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/health-audit> — cited in Parts 16 and 18.
- Microsoft Learn, "Automation in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/automation/automation> — cited in Part 16.
- Microsoft Learn, "Automate threat response in Microsoft Sentinel with automation rules," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/automate-incident-handling-with-automation-rules> — cited in Part 13.
- Microsoft Learn, "Use Watchlists to Correlate and Enrich Event Data in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/watchlists> — cited in Part 10.
- Microsoft Learn, "Advanced threat detection with User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/identify-threats-with-entity-behavior-analytics> — cited in Part 11.
- Microsoft Learn, "Microsoft Sentinel Content and Solutions Overview," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/sentinel-solutions> — cited in Part 7.
- Microsoft Learn, "Discover and deploy Microsoft Sentinel out-of-the-box content from Content hub," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/sentinel-solutions-deploy> — cited in Part 7.
- Microsoft Learn, "Deploy Custom Content from your Repository," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/ci-cd> — cited in Part 7.
- Microsoft Learn, "Manage custom content with repository connections," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/ci-cd-custom-content> — cited in Part 7.
- Microsoft Learn, "Use the Microsoft Sentinel Overview dashboard to view incidents, data, and analytics," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/get-visibility> — cited in Part 8.
- Microsoft Learn, "Visualize your Data by using Workbooks in Microsoft Sentinel," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/azure/sentinel/monitor-your-data> — cited in Parts 8 and 16.
- Microsoft Learn, "Microsoft.SecurityInsights/alertRules — Bicep, ARM template & Terraform AzAPI reference," *Azure Resource Manager template reference*: <https://learn.microsoft.com/azure/templates/microsoft.securityinsights/alertrules> — cited in Part 7.
- Microsoft Learn, "Microsoft Sentinel data lake overview," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-lake-overview> — cited in Part 12.
- Microsoft Learn, "What is Microsoft Sentinel's support for MCP?," *Microsoft Sentinel documentation*: <https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-overview> — cited in Part 12.

## Microsoft Learn / Microsoft Security Copilot documentation

- Microsoft Learn, "What is Microsoft Security Copilot?," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/microsoft-security-copilot> — cited in Part 12.
- Microsoft Learn, "Manage security compute unit usage in Security Copilot," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/manage-usage> — cited in Part 12.
- Microsoft Learn, "Privacy and data security in Microsoft Security Copilot," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/privacy-data-security> — cited in Part 12.
- Microsoft Learn, "Microsoft Security Copilot Security Compute Units and capacity," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/security-compute-units-capacity> — cited in Part 12.
- Microsoft Learn, "Microsoft Security Copilot agents overview," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/agents-overview> — cited in Part 12.
- Microsoft Learn, "Security Copilot Agent Development Overview," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/developer/custom-agent-overview> — cited in Part 12.
- Microsoft Learn, "Security Copilot Model Context Protocol," *Security Copilot documentation*: <https://learn.microsoft.com/en-us/copilot/security/developer/mcp-overview> — cited in Part 12.

## Standards bodies and vendor-neutral frameworks

- MITRE, "MITRE ATT&CK®" (knowledge base of adversary tactics and techniques): <https://attack.mitre.org/> — cited in Part 4, to establish that the tactic/technique taxonomy Sentinel's analytics-rule wizard maps into is MITRE's own vendor-neutral framework, not a Microsoft-specific one.
- National Institute of Standards and Technology (NIST), *Guide to a Secure Enterprise Network Landscape*, NIST Special Publication 800-215, November 2022: <https://csrc.nist.gov/pubs/sp/800/215/final> — cited in Part 11, for User and Entity Behavior Analytics (UEBA) as a named security-capability category that NIST documents independently of Microsoft Sentinel's own implementation of it ("Tracking of threats, such as account hijacking and other malicious activities, some of which can detect anomalies in users' cloud access behavior (through robust User and Entity Behavior Analytics (UEBA) functionality) and stop insider threats and advanced cyberattacks," §3.1, "Cloud Access Security Broker (CASB)").
- Model Context Protocol (MCP) project, "Model Context Protocol": <https://modelcontextprotocol.io/> — cited in Part 12, as the origin of the open, vendor-neutral protocol Microsoft Sentinel's and Security Copilot's MCP servers implement.

## Retrieval note

All Microsoft Learn URLs above were re-fetched and their content confirmed current as of
2026-09-16. Microsoft Learn pages are periodically renamed or restructured; if a link above 404s,
search [learn.microsoft.com](https://learn.microsoft.com) for the page title given rather than
assuming the underlying fact is no longer documented.
