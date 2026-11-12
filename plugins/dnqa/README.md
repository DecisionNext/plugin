# DecisionNext Integration

The DecisionNext Integration provides configuration for connecting to and
interacting with the DecisionNext platform from AI workspaces like Claude and
ChatGPT.

## Install Claude plugin

`/plugin install decisionnext-dnqa --marketplace https://gitlab.decisionnext.com/dn/plugin.git`

(The plugin is preinstalled for DecisionNext Team accounts)

## Connecting with Claude (OAuth2 sign-in)

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
