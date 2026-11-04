# DecisionNext AI Integration

This repository implements DN platform integrations for Claude, with plans for
expanded support in the mid term.

## Claude Marketplace

`.claude-plugin/marketplace.json` defines a custom Claude Plugin Marketplace,
which is published internally.

## Plugins

Plugins go in the `plugins/` directory, with the following layout.claude-plugin
    │   │── plugin.json
    │   └── icon.png
    ├── .mcp.json
    ├── commands
    ├── LICENSE
    ├── README.md
    └── skills

Claude plugins support 5 components: Commands, Skills, Agents, MCP/Connectors,
and MCP Apps.
A plugin containing only an MCP, or only skills, is a valid plugin.

Adding a plugin to the marketplace makes it available for internal users to
install. Alternatively, an admin can configure a plugin to automatically install
to each Team account.

*NOTE*: When adding a plugin, make sure you copy `icon.png` or another icon (.png
required) into the plugin's `.claude-plugin/` directory.

Add an entry for the plugin in `./.claude-plugin/marketplace.json`. See existing
listings for schema.
