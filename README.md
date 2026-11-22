# DecisionNext for Claude

The official [DecisionNext](https://decisionnext.com) plugin for Claude. It
connects Claude to the DecisionNext platform so you can ask about market
outlooks, forecasts, prices, spreads and drivers, build dashboards, and work
through buy, sell and timing decisions, all grounded in your DecisionNext data.

It covers protein, livestock, dairy, crop and oil markets, and it's built for
the buyers and sellers in those markets.

## What's included

| Component | Name | What it does |
| --- | --- | --- |
| MCP connector | `decisionnext` | Gives Claude secure access to DecisionNext market data, forecasts, model accuracy, forecast drivers, documents and dashboards. |
| Skill | `use-decisionnext` | Teaches Claude to answer like DecisionNext: buyer and seller-focused takeaways, correct units and sourcing, and protein, livestock, dairy and grain market knowledge. |
| Skill | `dn-buy-sell-decision` | Turns a forecast into decision support for buy, sell, hold and timing questions: the price outlook, the cost of waiting, risks and options. It lays out the picture and leaves the decision to you. |

## Requirements

- A DecisionNext account.
- MCP access enabled for your DecisionNext instance. An administrator turns
  this on per user under **Manage MCP Access** in the DecisionNext Admin app.
- Claude (claude.ai, Claude Desktop or Claude Code).

## Installation

### Claude Code

```text
/plugin marketplace add DecisionNext/DecisionNext
/plugin install decisionnext@decisionnext
```

### Claude Team and Enterprise

An organization admin can add this repository
(`https://github.com/DecisionNext/DecisionNext`) as a plugin marketplace in the
organization's Claude settings, then make the `decisionnext` plugin available to
members or install it automatically for everyone.

## Signing in

The first time Claude uses DecisionNext, it asks you to **Sign in to
DecisionNext**. Use your existing DecisionNext credentials (username and
password with MFA, or Google Workspace SSO) and grant consent once. You don't
need an API token or any manual configuration.

Signing in doesn't grant access to any data by itself. Claude can only see the
DecisionNext instances an administrator has enabled for you. If Claude reports
that no instances are available, ask your DecisionNext administrator to enable
MCP access for your instance.

If you have access to more than one instance, Claude asks which one to use
unless you name it. If you have only one, Claude uses it automatically.

## Example prompts

- "What's the outlook for choice ribeye over the next eight weeks?"
- "How accurate has the forecast for 50% lean trim been at four weeks out?"
- "What's driving the pork belly forecast?"
- "I need to buy 20 loads of briskets over the next six weeks. Help me plan
  the timing."
- "Build me a dashboard comparing boneless skinless breast and wing prices."

## Repository layout

```text
.
├── .claude-plugin/
│   └── marketplace.json      # Marketplace catalog listing the plugin
└── plugin/
    ├── .claude-plugin/
    │   ├── plugin.json       # Plugin manifest (name, version, author)
    │   └── icon.png
    ├── .mcp.json             # DecisionNext MCP server connection
    ├── skills/
    │   ├── use-decisionnext/
    │   │   └── SKILL.md
    │   └── dn-buy-sell-decision/
    │       └── SKILL.md
    └── LICENSE
```

## Support

For help with the plugin, your DecisionNext access or your forecasts, contact
your DecisionNext customer success specialist or email
[support@decisionnext.com](mailto:support@decisionnext.com).

## License

Copyright © 2026 DecisionNext, Inc. All rights reserved. See
[`plugin/LICENSE`](plugin/LICENSE).
