# MCP Filesystem Example

This example uses the [filesystem MCP server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem), running locally via `npx`.

Run it via:

```
uv run python examples/mcp/filesystem_example/main.py
```

## Details

The example uses the `MCPServerStdio` class from `agents.mcp`, with the command:

```bash
npx -y "@modelcontextprotocol/server-filesystem" <samples_directory>
```

It's only given access to the `sample_files` directory adjacent to the example, which contains some sample data.

Under the hood:

1. The server is spun up in a subprocess, and exposes a bunch of tools like `list_directory()`, `read_file()`, etc.
2. We add the server instance to the Agent via `mcp_agents`.
3. Each time the agent runs, we call out to the MCP server to fetch the list of tools via `server.list_tools()`.
4. If the LLM chooses to use an MCP tool, we call the MCP server to run the tool via `server.run_tool()`.

---


• Environment & API setup
    – Loads variables from .env (via python‑dotenv)
    – Configures openai.api_key from OPENAI_API_KEY

• Model Context Protocol (MCP) server startup
    – Uses the @modelcontextprotocol/server-filesystem npm package (via npx) to spin up a small HTTP server that exposes your sample_files/ folder as a “tool” the agent can call to read
files.
    – Wrapped in MCPServerStdio so the agent can communicate with it over STDIO.

• Tracing
    – Generates a trace_id and opens a trace span (so you can view the end‑to‑end conversation & tool calls in the OpenAI Trace UI).

• Agent orchestration (run() coroutine)
    – Instantiates an Agent named “Assistant” with simple instructions (“Use the tools to read the filesystem…”), passing in the MCP server as its tool-provider.
    – Runs three runs of Runner.run(...), each time:
        1. “Read the files and list them.”
        2. “What is my #1 favorite book?”
        3. “Look at my favorite songs. Suggest one new song that I might like.”
    – Prints out the final outputs of each run to the console.

• Entry point
    – Checks that npx is installed (so it can launch the filesystem server)
    – Uses asyncio.run(main()) to wire everything up and drive the demo

In short, it’s a small demo that 1) spins up a file‑system “tool” using the MCP protocol, 2) creates an LLM agent that can invoke that tool, and 3) runs through a few example prompts to
show how the agent reads and reasons over your local files.