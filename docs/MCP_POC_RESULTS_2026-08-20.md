# Companion MCP PoC validation results — 2026-08-20

## Summary

During the MCP integration test session the execution chain was validated:

```
ChatGPT
  -> Companion MCP
      -> execution node / VPS environment
          -> Docker container
```

## Confirmed capabilities

### Test marker creation

Tool `create_test_marker` was validated on both MCP instances.

Examples:

```
/tmp/chatgpt-final-test.txt
/tmp/chatgpt-test-server-0.txt
/tmp/chatgpt-test-server-2.txt
```

Successful response format:

```json
{
  "created": true,
  "path": "/tmp/<marker>.txt"
}
```

## Schema refresh experiment

Observed behavior:

- MCP tool schema refresh is required for discovering newly added tools.
- Existing conversations can use updated implementations after MCP refresh/reconnect behavior.
- Tool implementation changes can affect execution without necessarily changing the visible conversation context.

## Version endpoint experiment

`Companion_MCP_Test` exposed:

```
get_server_version()
```

Returned:

```json
{
  "version": "0.4.0",
  "schema_test": "refresh_check"
}
```

`Companion_MCP_Test_2` initially did not expose the version method.

## Runtime verification

Docker runtime verification:

```bash
docker exec companion-mcp cat /tmp/chatgpt-test-server-2.txt
```

Confirmed generated content:

```
created_by_mcp_NEW_VERSION
```

This demonstrated that the execution node was running the updated implementation.

## Deployment state

Current architecture:

```
VPS
 └── cloudflared tunnel
      └── local MCP endpoint
            └── companion-mcp Docker container
```

Next infrastructure step:

- move from temporary tunnel endpoint to permanent domain;
- configure named Cloudflare Tunnel using existing domain;
- stabilize public MCP endpoint.

## Next development phase

After infrastructure stabilization:

1. Define MCP API v1 contract.
2. Add capability discovery.
3. Add permission model.
4. Replace test tools with real execution tools.
