## 29. `titan lsp` — JSON-RPC 2.0 LSP Bridge & Zero-Index Fallback

### Verbatim Help Manual
```text
Usage: titan lsp <SUBCOMMAND> ...
Optional JSON-RPC 2.0 stdio LSP bridge with automatic TITAN zero-index fallback.

Subcommands:
  definition <FILE> <LINE> <COL> [--server CMD] [--root DIR] [-j]
  references <FILE> <LINE> <COL> [--server CMD] [--root DIR] [-j]
  hover <FILE> <LINE> <COL> [--server CMD] [--root DIR] [-j]
  diagnostics <FILE> [--server CMD] [--root DIR] [-j]
  rename-preview <FILE> <LINE> <COL> <NEW_NAME> [--server CMD] [--root DIR] [-j]
```

### Practical Examples
```powershell
titan lsp definition src/main.cpp 45 12 --root my-project -j
titan lsp rename-preview src/app.cpp 10 5 updated_name -j
```
