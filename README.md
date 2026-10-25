# Continua MCP for Claude

<img src="logo.png" alt="Continua AI" width="96" />

[Continua AI](https://askcontinua.com) brings cited investigations, reusable project knowledge, and working deliverables into Claude. Use it for **private credit, factoring, supply chain finance, and enterprise knowledge management**: start with financials, agreements, invoices, correspondence, and other source materials; return with a credit memo, exposure table, or review pack your team can act on.

This Claude Code **plugin** includes the **`/continua:analyze`** skill, connects to the hosted Continua MCP server, and supports **Investigation**, **Project Room**, and **Automation** workflows.

Follows the [Claude Code plugins guide](https://code.claude.com/docs/en/plugins) and [plugin publishing guide](https://code.claude.com/docs/en/plugins/publish).

## Connect Continua after installation

In Claude, open **Settings → Connectors**, find **Continua**, enable it, and choose **Connect** to sign in. In Claude Code, run **`/mcp`**, select the Continua server, and complete authentication. If authorization expires, reconnect there and retry the request.

The plugin uses Streamable HTTP with OAuth:

```text
https://app.askcontinua.com/mcp
```

Before the first task, call **`learn_how_to_use`** with `{}`. It returns the current usage guide without creating an analysis or consuming analysis credits. Investigations and project searches may consume credits; check the account's billing information when needed.

For clients using API keys, follow the [MCP connection guide](https://askcontinua.com/mcp). Keep credentials in your client's secure configuration.

## Plugin layout

```text
continua-mcp/                  # Plugin root
├── .claude-plugin/
│   └── plugin.json            # Manifest only
├── .mcp.json                  # MCP: Streamable HTTP + OAuth
├── logo.png                   # Plugin icon
├── LICENSE                    # MIT license
├── skills/
│   └── analyze/
│       └── SKILL.md           # /continua:analyze
└── README.md
```

| File | Role |
| --- | --- |
| [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json) | Plugin identity (`name`: `continua`), version, and MCP configuration |
| [`.mcp.json`](.mcp.json) | Connection to `https://app.askcontinua.com/mcp` |
| [`logo.png`](logo.png) | Plugin icon |
| [`LICENSE`](LICENSE) | MIT license |
| [`skills/analyze/SKILL.md`](skills/analyze/SKILL.md) | Tool picker and Investigation, Project Room, and Automation workflows |

Only `plugin.json` belongs in `.claude-plugin/`; keep `skills/`, `.mcp.json`, and the logo at the repository root.

Plugin icon: [Continua logo](logo.png). Privacy policy: [Continua privacy policy](https://app.askcontinua.com/privacy-policy).

---

## Local development

From this repository's root:

```bash
claude --plugin-dir .
```

In Claude Code:

1. Enable the plugin if prompted.
2. Run `/mcp`, connect **continua**, and complete sign-in.
3. Run `/reload-plugins` after editing `SKILL.md` or `plugin.json`.
4. Invoke **`/continua:analyze`** (namespace = `plugin.json` → `name`).
5. Read the current usage guide with `learn_how_to_use` and check the connection through `/mcp`.

---

## Validate before submit

From the plugin root:

```bash
claude plugin validate .
```

Resolve any reported issues before submission. See the [manifest reference](https://code.claude.com/docs/en/plugins-reference) for supported fields and paths.

---

## Submit to the community marketplace

Follow the current [plugin publishing and submission guide](https://code.claude.com/docs/en/plugins/publish). The directory submission route is the [developer portal](https://claude.ai/directory/manage):

1. Validate the plugin from the repository root.
2. Submit the GitHub repository through the portal and complete its validation and review steps.
3. After publication, share the install instructions from the published listing.

---

## analyze skill

[`skills/analyze/SKILL.md`](skills/analyze/SKILL.md) teaches Claude when and how to use Continua MCP through three main sections:

- **Investigation:** Review very large source sets with up to **1 billion tokens of working context**, as described in the [Platform overview](https://askcontinua.com/platform). Reconcile financials, agreements, amendments, invoices, and other evidence; surface conflicts and missing support with citations. Produce Word memos, Excel workbooks, PowerPoint presentations, and JSON/CSV outputs. Use Agent mode for project-aware orchestration.
- **Project Room:** Upload related materials once and reuse the same context for reports, follow-ups, and new questions. Share the source set with colleagues and other AI clients through project access settings. Preserve reviewed decisions, definitions, policies, recipes, and expert corrections in an **Enterprise Second Brain**, a shared **LLM wiki** that people and AI can read, refine, and reuse across investigations. Users can also forward requests and case attachments to **query@agent.askcontinua.com** through Continua Inbox.
- **Automation:** Schedule credit memos and supply chain reviews against project sources and connected systems. Follow **Intake → Underwrite → Monitor → Policy**: review changes and exceptions, confirm or correct conclusions, and preserve approved lessons for the next case.

Requires Continua MCP connected; the plugin loads the connection through `.mcp.json`. Financial conclusions and policy changes remain subject to the responsible team's review.

### Industry workflows

| Workflow | Source materials | Decision-ready output |
| --- | --- | --- |
| **Private credit** | Borrower financials, debt schedules, credit agreements, amendments, compliance certificates, prior memos | Cited credit memo, effective covenant and headroom matrix, cash-flow reconciliation, changes since the last review, and open diligence items |
| **Factoring and receivables finance** | Receivables aging, invoices, credit notes, remittances, purchase orders, delivery evidence, customer agreements | Receivables reconciliation, potential eligibility exceptions, dilution and concentration analysis, disputed items, and a borrowing-base review using the supplied facility rules |
| **Supply chain and working capital** | Supplier/customer contracts, orders, invoices, payment records, inventory and delivery reports | Supplier and buyer exposure map, payment and delivery exceptions, contract obligations, working-capital risks, and a prioritized follow-up plan |
| **Enterprise knowledge management** | Approved policies, metric definitions, prior decisions, SOPs, templates, expert reviews | Reusable project knowledge, cited decision history, policy comparisons, proposed lessons for review, and a consistent starting point for the next case |

### Example requests

```text
/continua:analyze Review our private credit project against the current loan
agreement and all amendments. Reconcile reported covenant compliance, identify
changes since the prior review, and produce a cited credit memo plus an Excel
exception register. Apply our approved credit policy and flag missing evidence.
```

Other starting points:

- “Reconcile this factoring pool's invoices, collections, credit notes, and aging. Apply the supplied eligibility rules and show every unresolved exception.”
- “Review supplier exposure and working-capital risks across contracts, orders, invoices, and payment records. Prepare a management deck and action register.”
- “Turn this reviewed case and my corrections into a draft decision record and proposed project knowledge. Show the changes for review before saving an approved policy.”
- “Run a weekly credit review against this Project and compare each result with the prior review.”

---

## Other clients (Cursor, Codex, ChatGPT)

This repository is a **Claude Code plugin**. For other clients, connect the Continua MCP server using the [MCP connection guide](https://askcontinua.com/mcp).

[Continua AI](https://askcontinua.com) · [MCP tools and connection guide](https://askcontinua.com/mcp) · [Platform](https://askcontinua.com/platform) · [Enterprise Second Brain and LLM wiki](https://askcontinua.com/second-brain) · [Privacy policy](https://app.askcontinua.com/privacy-policy)

Solutions & use cases: [All workflows](https://askcontinua.com/resources) · [Finance underwriting](https://askcontinua.com/ai-commercial-finance-underwriting) · [Credit review](https://askcontinua.com/ai-commercial-credit-review) · [Multi-document processing](https://askcontinua.com/solutions/multi-document-processing) · [Knowledge graph](https://askcontinua.com/solutions/knowledge-graph).
