# Use AI agents with the Postman API

The [Postman Model Context Protocol (MCP) server](https://www.postman.com/postman/postman-public-workspace/collection/681dc649440b35935978b8b7) enables AI agents like Claude, Cursor, and VS Code to help you manage your Postman resources, including workspaces, collections, specifications, mocks, and monitors. The server translates your natural language commands into API workflows behind the scenes. With [MCP](https://modelcontextprotocol.io/introduction), you can build AI agents and complex workflows on top of LLMs using the tools and context provided by the servers.

The Postman MCP server is also available in the [Postman MCP server GitHub repository](https://github.com/postmanlabs/postman-mcp-server).

## Before you begin

You need a [Postman account](https://identity.getpostman.com/signup) to use the MCP server. To use API key authentication, generate a Postman API key. An API key is required for the local server and the EU remote server, and optional on the US remote server. Keep this key secret and store it as an environment variable or your host's secret store, not in shared files.

## Communication methods

Communication between the Postman API and the AI agent happens through the following methods:

* **Remote Server** — Securely links the agent to the server over streamable HTTPS, without requiring any extra agent setup. Great for using the Postman MCP server with your preferred IDE or AI agent. It supports several [tool configurations](#tool-configurations) to better serve different use cases.

* **Local Server** — Runs the MCP server locally on the agent machine with STDIO. Requires downloading and running the source code yourself or spinning up a local [Docker](https://www.docker.com/) image. Local servers also support different [tool configurations](#tool-configurations) to support different use cases.

Use the remote server if your host doesn't support local servers, you want the quickest setup, or you work mainly with public APIs. Use the local server for local API testing, internal APIs, specific security or network requirements, or if you prefer to build the server from source.

For a complete list of the Postman MCP server's tools, see the [Postman MCP server collection](https://www.postman.com/postman/postman-public-workspace/collection/681dc649440b35935978b8b7).

## Tool configurations

Both the remote and local servers offer the same tool configurations, so you can load only the tools you need. Loading fewer tools lowers token usage and helps your agent choose the right tool.

* **Minimal** *(default)* — Includes only essential tools for basic Postman operations. Provides faster performance and is best when you only need core Postman features.
* **Code** — Includes tools to generate high-quality, well-organized client code from public and internal API definitions. Ideal for agents that need to consume APIs or get context about APIs.
* **Full** — All available Postman API tools (100+). Best for advanced collaboration and Postman Enterprise features.
* **Learn** — Searches Postman Docs for guides, tutorials, and reference content. Ideal for agents who need to discover Postman features, look up API concepts, or find learning resources.

For the specific endpoint URLs (remote) and command-line flags (local), see **Set up a remote server** and **Set up a local server**.

## EU support

The Postman MCP server supports the EU region for remote and local servers:

* For streamable HTTP, the remote server is available at `https://mcp.eu.postman.com/mcp` (Full), `https://mcp.eu.postman.com/code`, and `https://mcp.eu.postman.com/minimal`.
* For the STDIO public package, use the `--region eu` flag to specify the Postman API EU region, or set the `POSTMAN_API_BASE_URL` environment variable directly.

OAuth isn't supported for the EU Postman MCP server. The EU remote server only supports API key authentication.

## Use cases

* **Code synchronization** — Effortlessly keep your code in sync with your collections and specifications.
* **Collection management** — Create and tag collections, update collection and request documentation, add comments, or perform actions across multiple collections without leaving your editor.
* **Workspace and environment management** — Create workspaces and environments, plus manage your environment variables.
* **Automatic spec creation** — Create specifications from your code and use them to generate Postman Collections.

The Postman MCP server supports both remote servers through streamable HTTP and local servers with STDIO. Postman also offers servers as an [npm package](https://www.npmjs.com/package/@postman/postman-mcp-server) and as a Docker image.

## Authentication

For the best developer experience and fastest setup, use OAuth on the remote server. OAuth is fully compliant with the [MCP Authorization specification](https://modelcontextprotocol.io/specification/draft/basic/authorization) and doesn't require manual API key configuration.

The EU remote server and the local server support only Postman API key authentication.

## Get started with agents

Get set up and running with your remote or local Postman MCP server. Then, explore best practices and tips for getting the most out of its features.
