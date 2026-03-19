title: Set up a local Postman MCP server
-------

The local server is based on STDIO transport and is hosted locally on an environment of your choice. STDIO is a lightweight solution that's ideal for integration with editors and tools like Visual Studio Code. Install an MCP-compatible VS Code extension, such as GitHub Copilot, Claude for VS Code, or other AI assistants that support MCP. The local server only supports API key authentication (with a Postman API key or Bearer token).

<Info>
  The local server only supports API key authentication (with a Postman API key or Bearer token).
</Info>

### Use cases

Consider using the local Postman MCP server if:

* You want to power local use cases, such as local API testing.
* You have specific security and network requirements.
* You prefer to build the MCP server from the source code in this repo.

### Supported configurations

The local server supports the following tool configurations:

* **Minimal** — (Default) Only includes essential tools for basic Postman operations.
* **Code** — Includes tools for searching public and internal API definitions and generating client code.
* **Full** — Includes all available Postman API tools (100+ tools).

Use the `--region` flag to specify the Postman API region (`us` or `eu`), or set the `POSTMAN_API_BASE_URL` environment variable directly. By default, the server uses the `us` option.

<Note>
  To run the server as a Node application, install [Node.js](https://nodejs.org/) before getting started.
</Note>

## Visual Studio Code

Click the button to install the local Postman MCP server in VS Code:

<a href="https://insiders.vscode.dev/redirect/mcp/install?name=postman-api-mcp&inputs=%5B%7B%22id%22%3A%22postman-api-key%22%2C%22type%22%3A%22promptString%22%2C%22description%22%3A%22Enter%20your%20Postman%20API%20key%22%7D%5D&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22%40postman%2Fpostman-mcp-server%22%2C%22--full%22%5D%2C%22env%22%3A%7B%22POSTMAN_API_KEY%22%3A%22%24%7Binput%3Apostman-api-key%7D%22%7D%7D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the local Postman MCP server in VS Code" src="https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white" width="130px" />
</a>

By default, the server uses **Full** mode. To access **Minimal** mode, remove the `--full` flag from the `mcp.json` configuration file. To access **Code** mode, replace the `--full` flag with the `--code` flag.

### Manual configuration

You can manually integrate your MCP server with Cursor or VS Code to use it with extensions that support MCP. To do this, create a `mcp.json` file in your project and add the following JSON block to it:

```json wordWrap
{
    "servers": {
        "postman": {
            "type": "stdio",
            "command": "npx",
            "args": [
                "@postman/postman-mcp-server",
                "--full", // (optional) Use this flag to enable full mode...
                "--code", // (optional) ...or this flag to enable code mode.
                "--region us" // (optional) Use this flag to specify the Postman API region (us or eu). Defaults to us.
            ],
            "env": {
                "POSTMAN_API_KEY": "${input:postman-api-key}"
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

## Cursor

Click the button to install the local Postman MCP server in Cursor:

<a href="https://cursor.com/en/install-mcp?name=postman-api-mcp&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyJAcG9zdG1hbi9wb3N0bWFuLW1jcC1zZXJ2ZXIiLCItLWZ1bGwiXSwiZW52Ijp7IlBPU1RNQU5fQVBJX0tFWSI6IllPVVJfQVBJX0tFWSJ9fQ%3D%3D" target="_blank" rel="noopener noreferrer">
  <img alt="Install the local Postman MCP server in Cursor" src="https://cursor.com/deeplink/mcp-install-dark.svg" width="130px" role="img" />
</a>

By default, the server uses **Full** mode. To access **Minimal** mode, remove the `--full` flag from the `mcp.json` configuration file. To access **Code** mode, replace the `--full` flag with the `--code` flag.

### Manual installation

You can manually integrate your MCP server with VS Code to use it with extensions that support MCP. To do so, create a `.vscode/mcp.json` file in your project and add the following JSON block to it:

```json wordWrap
{
    "servers": {
        "postman-api-mcp": {
            "type": "stdio",
            "command": "npx",
            "args": [
                "@postman/postman-mcp-server",
                "--full" // (optional) Use this flag to enable full mode.
                "--code" // (optional) Use this flag to enable code mode.
                "--region us" // (optional) Use this flag to specify the Postman API region (us or eu). Defaults to us.
            ],
            "env": {
                "POSTMAN_API_KEY": "${input:postman-api-key}"
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

## Claude

To integrate the local Postman MCP server with Claude, check the [latest Postman MCP server release](https://github.com/postmanlabs/postman-mcp-server/releases) and get the `.mcpb` file:

* **Minimal** — `postman-api-mcp-minimal.mcpb`
* **Code** — `postman-mcp-server-code.mcpb`
* **Full** — `postman-api-mcp-full.mcpb`

For more information, see the [Claude Desktop Extensions](https://www.anthropic.com/engineering/desktop-extensions) documentation.

## Claude Code

To install the MCP server in Claude Code, run the following command in your terminal:

**Minimal**

```bash wordWrap
claude mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server@latest
```

**Code**

```bash wordWrap
claude mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server@latest --code
```

**Full**

```bash wordWrap
claude mcp add postman --env POSTMAN_API_KEY=<POSTMAN_API_KEY> -- npx @postman/postman-mcp-server@latest --full
```

## Codex

To install the local server, use the API key installation method. Set the `POSTMAN_API_KEY` environment variable and invoke the MCP server using `npx`.

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

## Windsurf

To manually install the MCP server in Windsurf, do the following:

1. Click **Open MCP Marketplace** in Windsurf.
2. Enter "Postman" in the search text box to filter the marketplace results.
3. Click **Install**.
4. When prompted, enter a valid Postman API key.
5. Select the tools that you want to enable, or click **All Tools** to select all available tools.
6. Turn on **Enabled** to enable the Postman MCP server.

### Manual installation

Copy the following JSON config into the `.codeium/windsurf/mcp_config.json` file:

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "args": [
                "@postman/postman-mcp-server"
            ],
            "command": "npx",
            "disabled": false,
            "disabledTools": [],
            "env": {
                "POSTMAN_API_KEY": "<POSTMAN_API_KEY>"
            }
        }
    }
}
```

## Antigravity

To install the MCP server in Antigravity, click **Manage MCP servers > View raw config**. Then, copy the following JSON config into the `mcp_config.json` file:

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "args": [
                "@postman/postman-mcp-server"
            ],
            "command": "npx",
            "disabled": false,
            "disabledTools": [],
            "env": {
                "POSTMAN_API_KEY": "<POSTMAN_API_KEY>"
            }
        }
    }
}
```

## GitHub Copilot CLI

Use the Copilot CLI to interactively add the MCP server:

```bash wordWrap
/mcp add
```

### Manual installation

Copy the following JSON config into the `~/.copilot/mcp-config.json` file:

```json wordWrap
{
    "mcpServers": {
        "postman": {
            "command": "npx",
            "args": [
                "@postman/postman-mcp-server"
            ],
            "env": {
                "POSTMAN_API_KEY": "<POSTMAN_API_KEY>"
            }
        }
    }
}
```

## Gemini CLI extension

To install the MCP server as a Gemini CLI extension, run the following command in your terminal:

```bash wordWrap
gemini extensions install https://github.com/postmanlabs/postman-mcp-server
```

## Kiro

To set up the Postman MCP server with one-click, go to [Kiro Powers](https://kiro.dev/powers/) and click **API Testing with Postman**. Then, click **Add to Kiro**.

### Manual installation

To manually install the Postman MCP server in Kiro, do the following:

1. Launch the Kiro app, then click the Kiro ghost icon in the left navigation.
2. Add an MCP Server, then select **User Config** or **Workspace Config** to install the Postman MCP server.
3. Add the following JSON block to the `mcp.json` configuration file:

   ```json wordWrap
   {
       "mcpServers": {
           "postman": {
           "command": "npx",
               "args": [
                   "@postman/postman-mcp-server"
               ],
               "env": {
                   "POSTMAN_API_KEY": "<POSTMAN_API_KEY>"
               },
               "disabled": false,
               "autoApprove": [
                   "getAuthenticatedUser"
               ]
           }
       }
   }
   ```

## Docker

{/* To use the Postman MCP server in Docker, you can use one of the following methods:  */}

To install the Postman MCP server in Docker, see the [Postman MCP server](https://hub.docker.com/mcp/server/postman/overview) at Docker MCP Hub. Click **+ Add to Docker Desktop** to automatically install it.

To run the Postman MCP server image in Docker, run the following command in your terminal. Docker automatically discovers, downloads, and runs the Postman MCP server image:

```bash wordWrap
docker run -i -e POSTMAN_API_KEY="<POSTMAN_API_KEY>" mcp/postman
```

### Manual installation

To build and run the server in Docker manually, run the `docker build -t postman-api-mcp-stdio .` command. Then, run one of the following commands:

**Minimal**

```bash wordWrap
docker run -i -e POSTMAN_API_KEY="<POSTMAN_API_KEY>" postman-api-mcp-stdio
```

**Full**

```bash wordWrap
docker run -i -e POSTMAN_API_KEY="<POSTMAN_API_KEY>" postman-api-mcp-stdio --full
```
