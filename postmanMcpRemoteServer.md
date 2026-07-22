# Set up a remote Postman MCP server

The remote Postman MCP server is hosted by Postman over streamable HTTP and provides the easiest method for getting started.

The remote server supports OAuth for the best developer experience and fastest setup, and doesn't require an API key. OAuth provides stronger security and access control compared to a static API key. It's MCP specification-compliant, including Dynamic Client Registration (DCR), OAuth metadata, and PKCE.

The EU remote server only supports API key authentication.

MCP hosts that support OAuth can discover and use it automatically for all tools. The remote server also accepts a Postman API key (Bearer token in the Authorization header).

### Before you begin

To use API key authentication (required for EU servers), generate a [Postman API key](https://go.postman.co/settings/me/api-keys). The US remote server supports OAuth and doesn't require a key.

### Endpoints

Use the endpoint that matches the tool configuration you want. Each is available in both the US and EU regions:

| Configuration     | US endpoint                       | EU endpoint                          |
| ----------------- | --------------------------------- | ------------------------------------ |
| Minimal (default) | `https://mcp.postman.com/minimal` | `https://mcp.eu.postman.com/minimal` |
| Code              | `https://mcp.postman.com/code`    | `https://mcp.eu.postman.com/code`    |
| Full              | `https://mcp.postman.com/mcp`     | `https://mcp.eu.postman.com/mcp`     |

OAuth is available on the US server only. The EU server requires a Postman API key (Bearer token in the `Authorization` header).

## Claude

To integrate the remote Postman MCP server with Claude using connectors, follow the setup instructions for the [Postman MCP connector for Claude](https://claude.com/connectors/postman).

## Claude Code

On the US server, Claude Code automatically uses OAuth for the best installation experience. To use an API key (required for the EU server), add the `--header` flag.

### OAuth

To use the OAuth installation method for US servers, run one of the following commands in your terminal:

#### Minimal

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/minimal
```

#### Code

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/code
```

#### Full

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/mcp
```

### API key

To use the API key installation method, run one of the following commands in your terminal. If you're using the EU server, you must use the API key installation method. For the EU server, replace `mcp.postman.com` with `mcp.eu.postman.com` in the commands below.

#### Minimal

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/minimal --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

#### Code

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/code --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

#### Full

```bash wordWrap
claude mcp add --transport http postman https://mcp.postman.com/mcp --header "Authorization: Bearer <POSTMAN_API_KEY>"
```

## Cursor

Click the button to install the remote Postman MCP server in Cursor:

<a href="https://cursor.com/en/install-mcp?name=postman_mcp_server&config=eyJ1cmwiOiJodHRwczovL21jcC5wb3N0bWFuLmNvbS9taW5pbWFsIiwiaGVhZGVycyI6eyJBdXRob3JpemF0aW9uIjoiQmVhcmVyIFlPVVJfQVBJX0tFWSJ9fQ%3D%3D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the remote Postman MCP server" src="https://cursor.com/deeplink/mcp-install-dark.svg" width="130px" role="img" />
</a>

If your MCP host supports OAuth, use the `https://mcp.postman.com/mcp`, `https://mcp.postman.com/minimal`, or `https://mcp.postman.com/code` server URL without headers for the fastest setup. Otherwise, ensure the Authorization header uses the `Bearer <YOUR_API_KEY>` format. Note that OAuth isn't supported for EU servers.

After installing, ensure that the Authorization header uses the `Bearer $POSTMAN-API-KEY` format.

To access **Full** mode, change the `url` value to `https://mcp.postman.com/mcp` in the `mcp.json` file. To access **Code** mode, change the value to `https://mcp.postman.com/code` in this file.

## Visual Studio Code

To install the remote Postman MCP server in VS Code, click the install button or use the Postman VS Code Extension:

<a href="https://insiders.vscode.dev/redirect/mcp/install?name=postman_mcp_server&config=%7B%22type%22%3A%20%22http%22%2C%22url%22%3A%20%22https%3A%2F%2Fmcp.postman.com%2Fminimal%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20YOUR_API_KEY%22%7D%7D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the remote Postman MCP server in VS Code" src="https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white" width="130px" />
</a>

To access **Full** mode, change the `url` value to `https://mcp.postman.com/mcp` in the `mcp.json` file. To access **Code** mode, change the value to `https://mcp.postman.com/code` in this file.

### Manual installation

You can use the Postman MCP server with MCP-compatible extensions in VS Code, such as GitHub Copilot, Claude for VS Code, or other AI assistants that support MCP. To do this, add the following JSON block to the `.vscode/mcp.json` configuration file:

#### OAuth

Add one of the following JSON blocks to use the recommended OAuth installation method:

#### Minimal

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal"
        }
    }
}
```

#### Code

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/code"
        }
    }
}
```

#### Full

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/mcp"
        }
    }
}
```

Start the server. When prompted, complete the OAuth sign-in flow.

#### API key

Use one of the following JSON blocks to use the desired API key installation method:

#### Minimal

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal",
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

#### Code

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/code",
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

#### Full

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/mcp",
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

## Codex

To install the remote server in Codex, use one of the following methods, depending on your authentication and region.

### OAuth

Use this method with the US server for the best installation experience. OAuth requires no manual API key setup.

#### Minimal

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/minimal
```

#### Code

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/code
```

#### Full

```bash wordWrap
codex mcp add postman --remote-url https://mcp.postman.com/mcp
```

### API key

If you're using the EU server (`mcp.eu.postman.com`), a local server, or prefer API key authentication, use the API key method. Set the `POSTMAN_API_KEY` environment variable and invoke the MCP server using `npx`.

#### Minimal

```bash wordWrap
codex mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server
```

#### Code

```bash wordWrap
codex mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server --code
```

#### Full

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

## Antigravity CLI

To install the MCP server in Antigravity CLI, run the following command:

```bash wordWrap
agy plugin install https://github.com/postmanlabs/postman-antigravity-cli-extension
```

For more information, see the [Postman Antigravity CLI extension](https://github.com/postmanlabs/postman-antigravity-cli-extension).

### API key

If you're using the EU server (`mcp.eu.postman.com`) or prefer API key authentication, use the API key method.

#### Minimal (US)

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "serverUrl": "https://mcp.postman.com/minimal",
            "headers": {
                "Authorization": "Bearer <POSTMAN_API_KEY>"
            }
        }
    }
}
```

#### Minimal (EU)

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "serverUrl": "https://mcp.eu.postman.com/minimal",
            "headers": {
                "Authorization": "Bearer <POSTMAN_API_KEY>"
            }
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

#### Minimal

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/minimal"
        }
    }
}
```

#### Code

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/code"
        }
    }
}
```

#### Full

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.postman.com/mcp"
        }
    }
}
```

#### API key

Use the following method to install if API key authentication is required for EU servers:

#### Minimal

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.eu.postman.com/minimal",
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

#### Code

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.eu.postman.com/code",
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

#### Full

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "type": "http",
            "url": "https://mcp.eu.postman.com/mcp",
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

## Kiro

To install the remote Postman MCP Server in Kiro, click the install button for the version that you want to use:

| **Minimal**                                                                                                                                                                                                                                                                                    | **Code**                                                                                                                                                                                                                                                                                 | **Full**                                                                                                                                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [![Add Postman MCP Minimal server to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https%3A%2F%2Fkiro.dev%2Flaunch%2Fmcp%2Fadd%3Fname%3Dpostman-mcp-server%26config%3D%7B%22url%22%3A%22https%3A%2F%2Fmcp.postman.com%2Fminimal%22%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D) | [![Add Postman MCP Code server to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https%3A%2F%2Fkiro.dev%2Flaunch%2Fmcp%2Fadd%3Fname%3Dpostman-mcp-server%26config%3D%7B%22url%22%3A%22https%3A%2F%2Fmcp.postman.com%2Fcode%22%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D) | [![Add Postman MCP Full server to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https%3A%2F%2Fkiro.dev%2Flaunch%2Fmcp%2Fadd%3Fname%3Dpostman-mcp-server%26config%3D%7B%22url%22%3A%22https%3A%2F%2Fmcp.postman.com%2Fmcp%22%2C%22disabled%22%3Afalse%2C%22autoApprove%22%3A%5B%5D%7D) |

## Verify your connection

After installing, restart or reload your MCP host so it picks up the new server. To confirm the connection works, check that your host lists the Postman server and its tools, then ask your agent to perform a simple read-only action, such as "List my Postman workspaces." If it returns your workspaces, you're connected.
