# DecisionNext Integration

The DecisionNext Integration provides configuration for connecting to and
interacting with the DecisionNext platform from AI workspaces like Claude and
ChatGPT.

Initially (as of 2026-10-30), we are focused on a Claude Plugin. An alpha-stage MCP
is currently being tested internally while under development, with all teams
starting working on a library of skills, and discover other methods for
maximizing the value customers will gain from adopting the integration.

## Connecting with Claude (OAuth sign-in)

The MCP server supports interactive OAuth 2.0 sign-in: installing the plugin and
adding the DecisionNext MCP server URL prompts Claude to **Sign in to DecisionNext**.
The user signs in with their existing DecisionNext credentials — username/password
plus MFA, or Google Workspace SSO — and grants consent once. No administrator-issued
token and no manual client configuration are required.

Instances are referred to by the names returned by the MCP server's `get_instances`
tool (aliases for external users, customer IDs for internal DecisionNext users).
Users with a single DecisionNext instance never need to choose.
