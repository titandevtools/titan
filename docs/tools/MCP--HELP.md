## 7. `titan mcp` — Native Model Context Protocol (JSON-RPC 2.0) Server

### Verbatim Help Manual
```text
Usage: titan mcp [OPTIONS]

Native Model Context Protocol (MCP) JSON-RPC 2.0 Server & AI Agent Manifest

Options:
  --stdio          Run persistent JSON-RPC 2.0 MCP server over stdin/stdout (default)
                   Supports both NDJSON lines and Content-Length header framing
  --manifest, -m   Dump complete JSON tool schema and capability manifest for AI Agents
  --tools          List MCP tool definitions in JSON
```

### Protocol & Registered Tools (53 In-Process Tools)
- **Transport:** Binary-safe `stdin`/`stdout` on Windows (`_O_BINARY`), supporting both `NDJSON` and `Content-Length` framing, UTF-8 BOM stripping, JSON-RPC 2.0 batch arrays, and notifications (`initialize`, `ping`, `tools/list`, `tools/call`).
- **Core Tools (21):** `titan_outline`, `titan_slice`, `titan_tree`, `titan_search`, `titan_replace`, `titan_find`, `titan_compare`, `titan_stats`, `titan_verb_rollback`, `titan_image`, `titan_video`, `titan_mp3`, `titan_format`, `titan_context`, `titan_symbol`, `titan_deps`, `titan_audit`, `titan_edit`, `titan_read`, `titan_archive`, `titan_name_files`.
- **Extended Tools (22):** `titan_ast_search`, `titan_ast_replace`, `titan_query`, `titan_table`, `titan_lsp`, `titan_tx`, `titan_inject`, `titan_run`, `titan_dir`, `titan_copy`, `titan_move`, `titan_rename`, `titan_create`, `titan_dev`, `titan_normalize`, `titan_http`, `titan_doc`, `titan_reg`, `titan_bench`, `titan_git`, `titan_ftp`, `titan_dissect`.
- **Complete Parity Tools (10):** `titan_merge`, `titan_delete`, `titan_system`, `titan_info`, `titan_structured`, `titan_process`, `titan_transform`, `titan_core_utils`, `titan_color`, `titan_verb_apply`.
