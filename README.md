# Converted Financial Services Plugins for Microsoft Copilot Cowork

Reference plugins and skills for the financial services workflows for use as templates to customize.

This fork preserves the original Claude implementations and adds converted Microsoft 365 Copilot Cowork packages. The original source remains available as a [Claude Cowork](https://claude.com/product/cowork) plugin or through the [Claude Managed Agents API](https://docs.claude.com/en/api/managed-agents); the converted source and upload-ready MOS3 packages provide a parallel path for Microsoft 365 Copilot Cowork.

> [!IMPORTANT]
> Nothing in this repository constitutes investment, legal, tax, or accounting advice. These agents draft analyst work product — models, memos, research notes, reconciliations — for review by a qualified professional. They do not make investment recommendations, execute transactions, bind risk, post to a ledger, or approve onboarding; every output is staged for human sign-off. You are responsible for verifying outputs and for compliance with the laws and regulations that apply to your firm.

## Evolution to Microsoft 365 Copilot Cowork

The upstream repository was authored for Claude plugins and Claude Managed Agents. This fork evolves that work into a dual-platform repository by converting each plugin into the Microsoft Copilot Cowork MOS3 package format while retaining the original Claude assets for comparison and continued upstream synchronization.

The conversion adds:

- MOS3 `manifest.json` files with valid app versions, deterministic app IDs, support metadata, and Microsoft 365 Copilot Cowork skill references.
- Expanded, reviewable package sources under [`src-copilot-cowork/`](./src-copilot-cowork).
- Upload-ready ZIP packages under [`dist-copilot-cowork/`](./dist-copilot-cowork).
- Original finance-themed package icons sized at 192×192 and 96 DPI.
- Cowork-compatible skill frontmatter and folder/name alignment.
- A maximum of 10 remote MCP connectors per app. The converted `financial-analysis` package retains the 10 finance and market-data connectors and omits the Box and Egnyte document-storage connectors to satisfy the MOS3 schema limit.

The converted packages use `Cowork Conversion` as the developer name and placeholder `contoso.com` website, privacy, terms, and fallback support values. Replace those placeholders with production publisher information before external distribution.

> [!WARNING]
> Fifteen source `SKILL.md` files exceed the current 20,000-character Cowork ingestion limit. They are intentionally preserved without summarization in this conversion, so packages containing those skills may require further editing before publication.

### Converted package layout

| Category | Expanded MOS3 source |
|---|---|
| Agent plugins | `src-copilot-cowork/agent-plugins/<plugin>/` |
| Vertical plugins | `src-copilot-cowork/vertical-plugins/<plugin>/` |
| Partner-built plugins | `src-copilot-cowork/partner-built/<plugin>/` |
| Microsoft 365 install tooling | `src-copilot-cowork/claude-for-msft-365-install/` |
| Upload-ready packages | `dist-copilot-cowork/*-mos3-<version>.zip` |

What's in the repo:

- **[Agents](#agents)** — named, end-to-end workflow agents (Pitch Agent, Market Researcher, GL Reconciler, …). Each ships as a Cowork plugin **and** as a [Claude Managed Agent template](./managed-agent-cookbooks) you deploy via `/v1/agents`.
- **[Vertical plugins](#vertical-plugins)** — the underlying skills, slash commands, and data connectors, bundled by FSI vertical. Install these on their own if you just want `/comps`, `/dcf`, `/earnings` and the connectors without a full agent.
- **[Microsoft 365 Copilot Cowork packages](#microsoft-365-copilot-cowork)** — converted MOS3 source packages and upload-ready ZIPs.


## Getting Started

### Cowork

In Cowork, open **Settings → Plugins → Add plugin** and either:

- **Paste this repo URL** — `https://github.com/davideldersveld/financial-services-mos3-conversion` — then pick the agents and verticals you want from the marketplace list, or
- **Upload a zip** — zip any directory under `plugins/` (e.g. `plugins/agent-plugins/pitch-agent/`) and drop it in.


### Microsoft Copilot Cowork

The converted packages are ready for review and upload from [`dist-copilot-cowork/`](./dist-copilot-cowork):

1. Select the ZIP you want.
2. Upload it through the Microsoft Copilot Cowork plugin publishing experience.
3. Configure each MCP connector's credential reference if needed (M365 admins must publish connectors).
4. Validate the package against your tenant's current schema and policies before publishing.

To inspect or customize a package first, edit its matching directory under [`src-copilot-cowork/`](./src-copilot-cowork), increment the manifest version, and rebuild the ZIP with the contents of that package directory at the archive root.


## Making It Yours

These are reference templates — they get better when you tune them to how your firm works.

- **Swap connectors** — point `.mcp.json` at your data providers and internal systems.
- **Add firm context** — drop your terminology, processes, and formatting standards into skill files.
- **Bring your templates** — `/ppt-template` teaches Claude your branded PowerPoint layouts.
- **Adjust agent scope** — edit `agents/<slug>.md` to match how your team actually runs the workflow.
- **Add your own** — copy the structure for workflows we haven't covered.

## Skill & Command Reference

<details>
<summary><b>financial-analysis</b> — core modeling, Excel, deck QC</summary>

| Skill | Command | Description |
|---|---|---|
| comps-analysis | `/comps` | Comparable company analysis with trading multiples |
| dcf-model | `/dcf` | DCF valuation with WACC and sensitivity analysis |
| lbo-model | `/lbo` | Leveraged buyout model |
| 3-statement-model | `/3-statement-model` | Populate 3-statement financial model templates |
| audit-xls | `/debug-model` | Excel model audit — formula tracing, hardcode detection, balance checks |
| clean-data-xls | — | Normalize and clean tabular data in Excel |
| deck-refresh | — | Re-link and refresh embedded charts/tables across a deck |
| competitive-analysis | `/competitive-analysis` | Competitive landscape and market positioning |
| ib-check-deck | — | QC presentations for errors and consistency |
| pptx-author | — | Produce a `.pptx` file headlessly (Managed Agent mode) |
| xlsx-author | — | Produce a `.xlsx` file headlessly (Managed Agent mode) |
| ppt-template-creator | `/ppt-template` | Create reusable PPT template skills |
| skill-creator | — | Guide for creating new skills |

</details>

<details>
<summary><b>investment-banking</b> — deal materials and execution</summary>

| Skill | Command | Description |
|---|---|---|
| strip-profile | `/one-pager` | One-page company profiles for pitch books |
| pitch-deck | — | Populate pitch deck templates with data |
| datapack-builder | — | Build data packs from CIMs and filings |
| cim-builder | `/cim` | Draft Confidential Information Memorandums |
| teaser | `/teaser` | Anonymous one-page company teasers |
| buyer-list | `/buyer-list` | Strategic and financial buyer universe |
| merger-model | `/merger-model` | Accretion/dilution M&A analysis |
| process-letter | `/process-letter` | Bid instructions and process correspondence |
| deal-tracker | `/deal-tracker` | Track live deals, milestones, and action items |

</details>

<details>
<summary><b>equity-research</b> — coverage and publishing</summary>

| Skill | Command | Description |
|---|---|---|
| earnings-analysis | `/earnings` | Post-earnings quarterly update reports |
| earnings-preview | `/earnings-preview` | Pre-earnings scenario analysis and key metrics |
| initiating-coverage | `/initiate` | Institutional-quality initiation reports |
| model-update | `/model-update` | Update financial models with new data |
| morning-note | `/morning-note` | Morning meeting notes and trade ideas |
| sector-overview | `/sector` | Industry landscape and thematic reports |
| thesis-tracker | `/thesis` | Maintain and update investment theses |
| catalyst-calendar | `/catalysts` | Track upcoming catalysts across coverage |
| idea-generation | `/screen` | Stock screening and idea sourcing |

</details>

<details>
<summary><b>private-equity</b> — sourcing through portfolio ops</summary>

| Skill | Command | Description |
|---|---|---|
| deal-sourcing | `/source` | Discover companies, check CRM, draft founder outreach |
| deal-screening | `/screen-deal` | Quick pass/fail on inbound CIMs and teasers |
| dd-checklist | `/dd-checklist` | Diligence checklists by workstream |
| dd-meeting-prep | `/dd-prep` | Prep for management presentations and expert calls |
| unit-economics | `/unit-economics` | ARR cohorts, LTV/CAC, net retention, revenue quality |
| returns-analysis | `/returns` | IRR/MOIC sensitivity tables |
| ic-memo | `/ic-memo` | Investment committee memo drafting |
| portfolio-monitoring | `/portfolio` | Track portfolio company KPIs and variances |
| value-creation-plan | `/value-creation` | Post-close 100-day plans and EBITDA bridges |
| ai-readiness | `/ai-readiness` | Assess a portfolio company's AI readiness |

</details>

## License

[Apache License 2.0](./LICENSE)
