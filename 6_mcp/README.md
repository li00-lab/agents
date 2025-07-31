# Model Context Protocol

## MCP is not
1. A framework for building agents.
2. A fundational change to how angents work.
3. A way to code agent.

## MCP is
1. A protocol - a standard to do things consistently and simply. NOTE: MCP is a standard not a tool themselves.
    a. We can already make any function into a tool using decorators.
    b. So if we are already writing our own tool and equipping the agent with them is easy, but MCP might make it harder.
2. A simple way to integrate tools, resources (RAG) and prompts written by others. Great for sharing tools.
3. A connection to other people's tools.
4. LangChain already has big Tools Ecosystem.
5. Makes it frictionless to connect with other people's tool.

## MCP Core Concepts
1. MCP host: is an LLM application like Claude or Agent architecture (Google ADK) in which we are going to be equpping an them with tools.
2. MCP client: lives inside the host and connects 1:1 to MCP server. It is like a plugin that runs inside that host.
3. MCP server: the actual piece of code that provides tools (ie. asking_weather), context and prompts to these extra capabilities to the agent. Usually the servers are running on our own machine.
    1. We can also have a remote server that contains the MCP server and we can use MCP client to connect to the server. (this is rare).
    2. Very common to have an MCP server that is connecting online and calling some remote service.
    3. Download open-source MCP servers, run them locally.

Example: Fetch is an MCP Server that searches the web via a headless browser.

## Two "Transport" Mechanisms
1. Stdio: spawns a process and communicates via standard input/output.
2. SSE: Server-Side-Events that uses HTTPS connection and it streams back result just like LLM. (This is must for remote server)