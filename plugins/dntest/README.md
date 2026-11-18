# DecisionNext Integration

The DecisionNext Integration provides configuration for connecting to and
interacting with the DecisionNext platform from AI workspaces like Claude and
ChatGPT. The plugin includes two separate MCP servers:

- **DecisionNext**: market data, forecasts, and decision support at
  `https://mcp.dntest.decisionnext.com/mcp`.
- **Protein ERP**: read-only SQL access to the simulated Summit Protein ERP at
  `https://erp.dntest.decisionnext.com/mcp`.

## Install Claude plugin

`/plugin install decisionnext-dntest --marketplace https://gitlab.decisionnext.com/dn/plugin.git`

(The plugin is preinstalled for DecisionNext Team accounts)

## Connecting with Claude (OAuth sign-in)

The MCP server supports interactive OAuth 2.0 sign-in: installing the plugin and
adding the DecisionNext MCP server URL prompts Claude to **Sign in to DecisionNext**.
The user signs in with their existing DecisionNext credentials — username/password
plus MFA, or Google Workspace SSO — and grants consent once. No administrator-issued
token and no manual client configuration are required.

Instances are referred to by the names returned by the MCP server's `get_instances`
tool (aliases for external users, customer IDs for internal DecisionNext users).
Users with a single DecisionNext instance never need to choose.

`get_instances` lists only the instances an administrator enabled for the user through
**Manage MCP Access** in the Admin app. Sign-in alone grants no instance access: if the
list is empty, ask a Pod Admin to enable MCP access for the instance.

## Connecting to the simulated ERP

The Protein ERP server requires a separate OAuth sign-in using the same DecisionNext
credentials. Signing in to the DecisionNext server does not authorize the ERP server.

ERP access requires membership in **Protein**, MCP access enabled for that instance,
and the **`erp.query`** grant. Ask a Pod Admin to enable **Query the simulated ERP
with SQL** under **Manage MCP Access** in the Admin app.

The ERP server exposes `list_tables()`, `list_columns(table)`, and `execute_query(sql)`
for querying simulated ERP data. It is read-only and separate from DecisionNext market
data and forecasts.
