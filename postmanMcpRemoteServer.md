# Set up a remote Postman MCP server

The remote Postman MCP server is hosted by Postman over streamable HTTP and provides the easiest method for getting started.

The remote server supports OAuth for the best developer experience and fastest setup, and doesn't require an API key. OAuth provides stronger security and access control compared to a static API key. It's MCP specification-compliant, including Dynamic Client Registration (DCR), OAuth metadata, and PKCE.

<Info>
  The EU remote server only supports API key authentication.
</Info>

MCP hosts that support OAuth can discover and use it automatically for all tools. The remote server also accepts a Postman API key (Bearer token in the Authorization header).

### Use cases

Consider using the remote Postman MCP server if:

* Your MCP host doesn't support local MCP servers.
* You want a quick way to get started with the Postman MCP server.

### Supported configurations

The remote Postman MCP server offers the following tool configurations through streamable HTTP:

* **Minimal** — (Default) Only includes essential tools for basic Postman operations, available at `https://mcp.postman.com/minimal` and `https://mcp.eu.postman.com/minimal` for EU users. This offers faster performance and simplifies use for those who only need basic Postman operations.
* **Code** — Includes tools for searching public and internal API definitions and generating client code, available at `https://mcp.postman.com/code` and `https://mcp.eu.postman.com/code` for EU users. This configuration is ideal for users who need to consume APIs or get context about APIs to their agents.
* **Full** — Includes all available Postman API tools (100+ tools), available at `https://mcp.postman.com/mcp` and `https://mcp.eu.postman.com/mcp` for EU users.

## Cursor

Click the button to install the remote Postman MCP server in Cursor:

<a href="https://cursor.com/en/install-mcp?name=postman_mcp_server&config=eyJ1cmwiOiJodHRwczovL21jcC5wb3N0bWFuLmNvbS9taW5pbWFsIiwiaGVhZGVycyI6eyJBdXRob3JpemF0aW9uIjoiQmVhcmVyIFlPVVJfQVBJX0tFWSJ9fQ%3D%3D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the remote Postman MCP server" src="https://cursor.com/deeplink/mcp-install-dark.svg" width="130px" role="img" />
</a>

If your MCP host supports OAuth, use the `https://mcp.postman.com/mcp`, `https://mcp.postman.com/minimal`, or `https://mcp.postman.com/code` server URL without headers for the fastest setup. Otherwise, ensure the Authorization header uses the `Bearer <YOUR_API_KEY>` format. Note that OAuth isn't supported for EU servers.

After installing, ensure that the Authorization header uses the `Bearer $POSTMAN-API-KEY` format.

To access **Full** mode, change the `url` value to `https://mcp.postman.com/mcp` in the `mcp.json` file. To access **Code** mode, change the value to `https://mcp.postman.com/code` in this file.

## Visual Studio Code

To install the remote Postman MCP server in VS Code, click the install button or use the [Postman VS Code Extension](/docs/developer/vs-code-extension/postman-mcp-server/):

<a href="https://insiders.vscode.dev/redirect/mcp/install?name=postman_mcp_server&config=%7B%22type%22%3A%20%22http%22%2C%22url%22%3A%20%22https%3A%2F%2Fmcp.postman.com%2Fminimal%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20YOUR_API_KEY%22%7D%7D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the remote Postman MCP server in VS Code" src="https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white" width="130px" />
</a>

To access **Full** mode, change the `url` value to `https://mcp.postman.com/mcp` in the `mcp.json` file. To access **Code** mode, change the value to `https://mcp.postman.com/code` in this file.

### Manual installation

You can use the Postman MCP server with MCP-compatible extensions in VS Code, such as GitHub Copilot, Claude for VS Code, or other AI assistants that support MCP. To do this, add the following JSON block to the `.vscode/mcp.json` configuration file:

#### OAuth

Add the following JSON block to use the recommended OAuth installation method:

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal"
                // "https://mcp.postman.com/code" for Code mode
                // "https://mcp.postman.com/mcp" for Full mode
        }
    }
}
```

Start the server. When prompted, enter your Postman API key.

#### API key

Use the following JSON block to use the API key installation method:

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal",
                // "https://mcp.postman.com/code" for Code mode
                // "https://mcp.postman.com/mcp" for Full mode
            "headers": {
                "Authorization": "Bearer ${input:postman-api-key}"
            }
        }
    },
    "inputs": [
        {
            "id": "postman-api-key",
            "type": "promptString",
            "description": "Enter your Postman API key"
        }
    ]
}
```

Start the server. When prompted, enter your Postman API key.

## Claude Code

On the US server, Claude Code automatically uses OAuth for the best installation experience. To use an API key (required for the EU server), add the `--header` flag.

### OAuth

To use the OAuth installation method for US servers, run the following command in your terminal:

**Minimal**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/minimal
```

**Code**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/code
```

**Full**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/mcp
```

### API key

To use the API key installation method if required and for EU servers (`mcp.eu.postman`), run the following command in your terminal:

**Minimal**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/minimal --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

**Code**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/code --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

**Full**

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/mcp --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

## Codex

To install the remote server in Codex, use one of the following methods, depending on your authentication and region.

### OAuth

Use this method with the US server for the best installation experience. OAuth requires no manual API key setup.

**Minimal**

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/minimal
```

**Code**

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/code
```

**Full**

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/mcp
```

### API key

If you're using the EU server (`mcp.eu.postman`), a [local server](/docs/developer/postman-api/postman-mcp-server/postman-mcp-local-server#codex), or prefer API key authentication, use the API key method. Set the `POSTMAN_API_KEY` environment variable and invoke the MCP server using `npx`.

**Minimal**

```bash wordWrap
codex mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server --minimal
```

**Code**

```bash wordWrap
codex mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server --code
```

**Full**

```bash wordWrap
codex mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server --full
```

### Manual installation

To manually install the MCP server in Codex, create a `~/.codex/config.toml` config file, then copy the following config into the file:

```bash wordWrap
[mcp_servers.postman-mcp-server]
command = "npx"
args = ["-y", "@postman/postman-mcp-server"]

[mcp_servers.postman-mcp-server.env]
POSTMAN_API_KEY="XXX"
```

## Windsurf

To install the MCP server in Windsurf, copy the following JSON config into the `.codeium/windsurf/mcp_config.json` file. This configuration uses the remote server, which automatically authenticates with OAuth.

```json wordWrap
{
    "mcpServers": {
        "postman-full": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/mcp"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        },
        "postman-code": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/code"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        },
        "postman-minimal": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/minimal"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        }
    }
}
```

## Antigravity

To install the MCP server in Antigravity, click **Manage MCP servers > View raw config**. Then, copy the following JSON config into the `.mcp_config.json` file. This configuration uses the remote server, which automatically authenticates with OAuth.

```json wordWrap
{
    "mcpServers": {
        "postman-full": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/mcp"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        },
        "postman-code": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/code"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        },
        "postman-minimal": {
            "args": [
                "mcp-remote",
                "https://mcp.postman.com/minimal"
            ],
            "disabled": false,
            "disabledTools": [],
            "env": {}
        }
    }
}
```

## GitHub Copilot CLI

You can add the MCP server to your Copilot CLI either with OAuth (recommended) or an API key.

Use the Copilot CLI to interactively add the MCP server:

```bash wordWrap
/mcp add
```

For more information, see the [Copilot CLI documentation](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli).

### Manual installation

Copy the following JSON config into the `~/.copilot/mcp-config.json` file:

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal"
                // "https://mcp.postman.com/mcp" for Full mode
                // "https://mcp.postman.com/code" for Code mode
        }
    }
}
```

#### API key

Use the following method to install if API key authentication is required for EU servers (`mcp.eu.postman`):

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal",
                // "https://mcp.postman.com/mcp" for Full mode
                // "https://mcp.postman.com/code" for Code mode
            "headers": {
                "Authorization": "Bearer ${input:postman-api-key}"
            }
        }
    },
    "inputs": [
        {
            "id": "postman-api-key",
            "type": "promptString",
            "description": "Enter your Postman API key"
        }
    ]
}
```
