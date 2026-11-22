# DecisionNext

Connect Claude to [DecisionNext](https://decisionnext.com) for market outlooks,
forecasts, forecast accuracy, price drivers, dashboards, and buy, sell and timing
decisions, all grounded in your DecisionNext data.

## Contents

- **DecisionNext connector (MCP):** secure access to your DecisionNext market
  data, forecasts, documents and dashboards.
- **`use-decisionnext` skill:** answers in DecisionNext's voice with
  buyer and seller-focused takeaways, correct units and sourcing, and protein,
  livestock, dairy and grain market knowledge.
- **`dn-buy-sell-decision` skill:** turns a forecast into decision support for
  buy, sell, hold and timing questions. It lays out the price outlook, the cost
  of waiting, risks and options, and leaves the decision to you.

## Install

In Claude Code:

```text
/plugin marketplace add DecisionNext/plugin
/plugin install decisionnext@decisionnext
```

On Claude Team and Enterprise plans, your organization admin can make the
plugin available to members or install it for everyone.

## Sign in

The first time Claude uses DecisionNext, it asks you to **Sign in to
DecisionNext**. Use your existing DecisionNext credentials (username and
password with MFA, or Google Workspace SSO) and grant consent once. You don't
need an API token or any manual configuration.

Signing in doesn't grant access to any data by itself. Claude can see only the
DecisionNext instances an administrator has enabled for you under **Manage MCP
Access** in the DecisionNext Admin app. If Claude reports that no instances are
available, ask your DecisionNext administrator to enable MCP access for you.

If you have more than one instance, Claude asks which one to use unless you name
it. If you have only one, Claude uses it automatically.

## Support

Contact your DecisionNext customer success specialist or email
[support@decisionnext.com](mailto:support@decisionnext.com).

## License

Copyright © 2026 DecisionNext, Inc. All rights reserved. See [LICENSE](LICENSE).
