# MCP SSE Example

This example uses a local SSE server in [server.py](server.py).

Run the example via:

```
uv run python examples/mcp/sse_example/main.py
```

## Details

The example uses the `MCPServerSse` class from `agents.mcp`. The server runs in a sub-process at `https://localhost:8000/sse`.

---

what it is a sse server?

    codex
    A “Server‑Sent Events” (SSE) server is an HTTP endpoint that keeps a connection open and streams text‑based event data to the client in real time. It uses the W3C “EventSource” protocol to
     push updates one‑way—from the server to any number of listening browsers or clients—over a single long‑lived HTTP connection.

    Key points:
    • Protocol and headers
      – Content-Type: text/event‑stream
      – Cache‑Control: no‑cache
      – Connection: keep‑alive

    • Message format
      The server writes blocks of UTF‑8 text, each separated by a blank line. A block can contain:
      – id: an optional event ID (used by the client for reconnection)
      – event: an optional event name (if you want named events)
      – data: the payload (can be multi‑line—each line prefixed with “data:”)
      Example:
        id: 42
        event: tick
        data: { "time": "2025‑04‑23T15:00:00Z" }

    • Client side
      In the browser you do:
        const src = new EventSource('/events');
        src.addEventListener('tick', e => console.log(e.data));
        src.onmessage = e => console.log('default event:', e.data);
        src.onerror = e => console.error('connection lost');

    • Automatic reconnect
      If the HTTP connection drops, the client will automatically re‑open it, sending a “Last‑Event‑ID” header so the server can resume from where it left off.

    • When to use SSE vs. WebSockets
      – SSE is uni‑directional (server→client) only—perfect for live feeds, notifications, dashboards, logs.
      – Uses plain HTTP/1.1—easier to get through proxies and firewalls.
      – Lightweight: no framing, subprotocols, or binary fragmentation.
      – If you need bidirectional, low‑latency, full‑duplex messaging, you’d choose WebSockets.

    In short, an SSE server is just an HTTP endpoint that writes an endless “event stream” of text, keeping the connection open so clients can receive real‑time updates without constantly
    polling.