# Changelog

All notable public releases of **TITAN** are documented in this file.

## [2.0.3] - 2026-11-25

### Highlights
- **Single Native Windows x64 Binary (`titan.exe`):** 100% written from scratch in native C++20 with zero external runtime dependencies (`10,683,392` bytes, stripped of internal symbols).
- **69 Unified CLI Commands:** Complete coverage across code dissection, AST search/replace, surgical line editing, multi-file atomic transactions, streaming file merging, text/record/CSV/SQL-lite processing, structured data (`JSON`/`YAML`/`TOML`/`XML`/`INI`/`Qt .ui`/`Sublime Text`), archives (`ZIP`/`TAR`/`GZIP`/`ZSTD`/`7Z`/`RAR`), media (`image`, `video`, `mp3`/`audio`), Office OpenXML (`doc`), Git, HTTP, FTP/FTPS, Windows Registry, benchmarking, and system inspection.
- **53 In-Process MCP Tools (`titan mcp --stdio`):** Full JSON-RPC 2.0 Model Context Protocol server supporting `Content-Length` framing, NDJSON, batch arrays, UTF-8, and persistent sessions for AI coding agents.
- **Native `.ti` Scripting Language (`titan run` / `titan ti`):** Built-in text-processing and automation language featuring 102 standard library/pipeline operations, linear-time Thompson NFA / Pike VM regex engine, closures, arrow lambdas, pattern matching, destructuring, optional chaining, 4 string forms, and a safe Tier-2 `titan` CLI bridge.
- **New `titan dissect` & `titan merge` Engines:**
  - `titan dissect`: Unified 20-language code & text dissection engine (`--xray`, `--outline`, `--lines`, `--read`, `--resolve`, `--context`, `--bundle`, `--hotspots`).
  - `titan merge`: Streaming O(1)-RAM multi-format file merger (`text`, `binary`, `lines`, `bytes`, `json`, `jsonl`, `csv`, `tsv`, `xml`, `html`, `srt`, `vtt`, `m3u`) with cryptographic hashing and Windows long-path (`\\?\`) support.
- **Crash-Safe & Agent-Safe Guardrails:** Atomic file writes, SHA-256 optimistic concurrency locks, collision-proof `.orig` backups with rollback, `--dry-run` previews, and protected Windows system-path guards.
