# MCP Server

This guide explains how to configure various AI agents and IDEs to use the VisuallyJs MCP servers. These servers provide documentation and search capabilities for `@visuallyjs/browser-ui` and its library-specific integrations.

## Available MCP Servers[​](#available-mcp-servers "Direct link to Available MCP Servers")

You can choose to install the all-in-one server or a specific one for your library:

| Package                              | Library                                    | Command                                  |
| ------------------------------------ | ------------------------------------------ | ---------------------------------------- |
| `@visuallyjs/browser-ui-angular-mcp` | Angular                                    | `npx @visuallyjs/browser-ui-angular-mcp` |
| `@visuallyjs/browser-ui-react-mcp`   | React                                      | `npx @visuallyjs/browser-ui-react-mcp`   |
| `@visuallyjs/browser-ui-svelte-mcp`  | Svelte                                     | `npx @visuallyjs/browser-ui-svelte-mcp`  |
| `@visuallyjs/browser-ui-vue-mcp`     | Vue                                        | `npx @visuallyjs/browser-ui-vue-mcp`     |
| `@visuallyjs/browser-ui-vanilla-mcp` | Vanilla JS                                 | `npx @visuallyjs/browser-ui-vanilla-mcp` |
| `@visuallyjs/browser-ui-mcp`         | All (Angular, React, Svelte, Vue, Vanilla) | `npx @visuallyjs/browser-ui-mcp`         |

### Version Management[​](#version-management "Direct link to Version Management")

The MCP package versions are kept in sync with their related `@visuallyjs/browser-ui` packages.

While it's not required (omitting the version will always pull the latest), you may want to include a specific version number in your configuration to ensure compatibility with the version of VisuallyJs you are using in your project.

To use a specific version, append `@<version>` to the package name:

* `npx -y @visuallyjs/browser-ui-mcp@1.1.0`

***

## Setup[​](#setup "Direct link to Setup")

### Claude Desktop[​](#claude-desktop "Direct link to Claude Desktop")

To use VisuallyJs MCP with Claude Desktop, you need to edit your `claude_desktop_config.json` file.

1. Open your Claude Desktop configuration file:

   * **macOS:** `~/Library/Application\ Support/Claude/claude_desktop_config.json`
   * **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

2. Add the server to the `mcpServers` section. For example, to add the all-in-one server:

```json
{
  "mcpServers": {
    "visuallyjs": {
      "command": "npx",
      "args": [
        "-y",
        "@visuallyjs/browser-ui-mcp"
      ]
    }
  }
}

```

3. Restart Claude Desktop.

***

### Cursor[​](#cursor "Direct link to Cursor")

Cursor supports MCP servers natively.

1. Open Cursor and go to **Settings** > **Cursor Settings** > **Features**.

2. Scroll down to the **MCP** section.

3. Click on **+ Add New MCP Server**.

4. Fill in the details:

   <!-- -->

   * **Name:** `VisuallyJs`
   * **Type:** `command`
   * **Command:** `npx -y @visuallyjs/browser-ui-mcp` (or your framework-specific package)

5. Click **Save**.

***

### IntelliJ IDEA[​](#intellij-idea "Direct link to IntelliJ IDEA")

In IntelliJ IDEA, you can configure MCP servers for both the **AI Assistant** and **Junie**.

#### AI Assistant[​](#ai-assistant "Direct link to AI Assistant")

1. Open **Settings** (or **Settings/Preferences** on macOS) and navigate to **Tools** > **AI Assistant**.

2. Look for the **MCP Servers** section.

3. Click **+ Add Server**.

4. Configure the server:

   <!-- -->

   * **Name:** `VisuallyJs`
   * **Command:** `npx`
   * **Arguments:** `-y @visuallyjs/browser-ui-mcp` (or your specific framework package)

5. Click **OK** to save.

#### Junie[​](#junie "Direct link to Junie")

1. Open **Settings** and navigate to **Tools** > **Junie**.

2. Find the **MCP Servers** configuration area.

3. Click **Add** or **+**.

4. Fill in the details:

   <!-- -->

   * **Name:** `VisuallyJs`
   * **Command:** `npx`
   * **Arguments:** `-y @visuallyjs/browser-ui-mcp`

5. Click **Save** or **Apply**.

***

### VS Code (via Continue or Roo Code)[​](#vs-code-via-continue-or-roo-code "Direct link to VS Code (via Continue or Roo Code)")

#### Continue[​](#continue "Direct link to Continue")

Follow the same steps as for IntelliJ (edit `~/.continue/config.json`).

#### Roo Code (formerly Roo Cline)[​](#roo-code-formerly-roo-cline "Direct link to Roo Code (formerly Roo Cline)")

1. Open the Roo Code side panel.

2. Click on the **Settings** (cog) icon.

3. Find the **MCP Servers** section.

4. Add the server:

   <!-- -->

   * **Name:** `visuallyjs`
   * **Command:** `npx -y @visuallyjs/browser-ui-mcp`

***

### Goose[​](#goose "Direct link to Goose")

Goose is a CLI-based agent that supports MCP.

To add the VisuallyJs MCP server to Goose:

```bash
goose configure

```

Follow the prompts to add a new MCP server with the command `npx -y @visuallyjs/browser-ui-mcp`.

Alternatively, you can manually edit the goose configuration file (usually in `~/.goose/config.yaml` or similar depending on your OS).

***

### Other Agents[​](#other-agents "Direct link to Other Agents")

Most agents that support the Model Context Protocol (MCP) follow a similar pattern: they require a `command` (usually `npx`) and `arguments` (the package name).

If you are using a different agent, look for "MCP" or "Model Context Protocol" in its settings and provide the following:

* **Command:** `npx`
* **Arguments:** `-y @visuallyjs/browser-ui-mcp`

***

## Available Tools[​](#available-tools "Direct link to Available Tools")

Each library-specific package provides tools with unique suffixes, allowing them to coexist in a flat namespace if multiple servers are connected simultaneously.

info

In 1.2.7 the previous tools for searching the main docs and the API docs were combined into one. In this section we now list the combined tool names - see below for the previous tool names, which are valid for all versions up to 1.2.6 (and which are still present in 1.2.7, but deprecated)

### Angular[​](#angular "Direct link to Angular")

* `visuallyjs_angular` Search VisuallyJs Angular documentation and API docs

### React[​](#react "Direct link to React")

* `visuallyjs_react` Search VisuallyJs React documentation and API docs

### Vue[​](#vue "Direct link to Vue")

* `visuallyjs_vue` Search VisuallyJs Vue documentation and API docs

### Svelte[​](#svelte "Direct link to Svelte")

* `visuallyjs_svelte` Search VisuallyJs Svelte documentation and API docs

### Vanilla[​](#vanilla "Direct link to Vanilla")

* `visuallyjs_vanilla` Search VisuallyJs Vanilla documentation and API docs

## Deprecated tools (< 1.2.7)[​](#deprecated-tools--127 "Direct link to Deprecated tools (< 1.2.7)")

These tools are named following the pattern `search_vjs_<suffix>` for general documentation and `search_vjs_<suffix>_api` for API-specific documentation. Use these tools if you're using a version of VisuallyJs < 1.2.7.

### Angular[​](#angular-1 "Direct link to Angular")

* `search_vjs_ng`: Search VisuallyJs Angular documentation.
* `search_vjs_ng_api`: Search VisuallyJs Angular API documentation.

### React[​](#react-1 "Direct link to React")

* `search_vjs_react`: Search VisuallyJs React documentation.
* `search_vjs_react_api`: Search VisuallyJs React API documentation.

### Vue[​](#vue-1 "Direct link to Vue")

* `search_vjs_vue`: Search VisuallyJs Vue documentation.
* `search_vjs_vue_api`: Search VisuallyJs Vue API documentation.

### Svelte[​](#svelte-1 "Direct link to Svelte")

* `search_vjs_svelte`: Search VisuallyJs Svelte documentation.
* `search_vjs_svelte_api`: Search VisuallyJs Svelte API documentation.

### Vanilla[​](#vanilla-1 "Direct link to Vanilla")

* `search_vjs_vanilla`: Search VisuallyJs Vanilla documentation.
* `search_vjs_vanilla_api`: Search VisuallyJs Vanilla API documentation.

### All libraries[​](#all-libraries "Direct link to All libraries")

The `@visuallyjs/browser-ui-mcp` package (the `all` package) offers all of the search commands from each of the library-specific packages listed above. This allows you to have a single MCP server that can search across all VisuallyJs integrations.
