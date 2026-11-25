# TITAN v2.0.3

**Native Windows x64 Unified CLI Runtime, `.ti` Scripting Language & MCP Server for AI Agents and Developers**

> Conceived & Architected by **Nourddine Bakour** (Tetouan, Morocco)  
> 100% Native C++20 — Built From Scratch — Zero External Runtime Dependencies — Closed-Source Proprietary Binary Distribution

---

## Why TITAN?

AI coding agents and engineers on Windows typically juggle slow PowerShell pipelines, inconsistent third-party binaries, and fragile shell quoting. **TITAN** replaces that patchwork with a single, fast, crash-safe native executable (`titan.exe`) exposing:

- **69 Unified CLI Commands** — code dissection, AST search/rewrite, surgical edits, atomic transactions, streaming file merge, structured data, archives, media, Office documents, Git, HTTP, FTP/FTPS, Windows Registry, benchmarking, and system diagnostics.
- **53 Native MCP Tools (`titan mcp --stdio`)** — machine-readable JSON-RPC 2.0 Model Context Protocol server ready for Claude, Antigravity, Codex, Cursor, and custom agent harnesses.
- **Built-In `.ti` Programming Language (`titan run`)** — a safe, self-documenting text-processing and workflow language with 102 built-in operations, linear-time regex, closures, arrow lambdas, pattern matching, and an in-process `titan` command bridge.
- **Safety By Design** — SHA-256 optimistic concurrency locks, atomic temp-and-replace writes, collision-proof `.orig` backups with rollback, `--dry-run` previews, and protected Windows OS path guards.

---

## Quick Start (Windows x64)

1. Download `bin/titan.exe` (or clone/download this release repository) and add its folder to your Windows `PATH`.
2. Verify the binary integrity against [`SHA256SUMS.txt`](SHA256SUMS.txt):

```powershell
Get-FileHash .\bin\titan.exe -Algorithm SHA256
# Expected: D0B4F5BF77C58EE25A2237C61FC567660EC99D4FB3B421074A0CBE011447EEF1
```

3. Verify your installation:

```powershell
titan info
titan --help
titan run --guide
```

---

## Command Categories (69 Registered Commands)

| Category | Commands |
| :--- | :--- |
| **Code & AI Dissection** | `dissect`, `dev`, `outline`, `slice`, `read`, `context`, `symbol`, `deps`, `audit`, `agent`, `lsp`, `ast-search`, `ast-replace` |
| **Surgical Edit & Transactions** | `edit`, `inject`, `injection`, `verb`, `tx`, `replace`, `transform`, `format`, `normalize` |
| **Search, Files & Merging** | `search`, `find`, `dir`, `tree`, `create`, `copy`, `move`, `rename`, `name-files`, `delete`, `compare`, `merge`, `core-utils` |
| **Data, Tables & Formats** | `query`, `table`, `stats`, `process`, `convert`, `analyze`, `validate`, `fix`, `inspect-file`, `doc`, `tr` |
| **Archives & Media** | `archive`, `image`, `video`, `mp3`, `audio` |
| **Color Engine** | `hex`, `rgb`, `hsl`, `hsla`, `cmyk`, `named`, `multi`, `color-tips` |
| **System, Network & DevOps** | `git`, `http`, `ftp`, `reg`, `system`, `bench`, `info` |
| **Scripting & MCP Server** | `run`, `ti`, `mcp` |

---

## Connecting AI Agents via MCP

Register `titan` as a standard stdio MCP server in your AI client:

```json
{
  "mcpServers": {
    "titan": {
      "command": "titan",
      "args": ["mcp", "--stdio"]
    }
  }
}
```

Inspect the full tool manifest at any time:

```powershell
titan mcp --manifest
```

---

## Documentation

- **Master Command Reference:** [`docs/TITAN_HELP.md`](docs/TITAN_HELP.md)
- **`.ti` Language Guide:** [`docs/TITAN_LANGUAGE_GUIDE.md`](docs/TITAN_LANGUAGE_GUIDE.md) (or run `titan run --guide`)
- **Per-Tool Manuals (49 Tools):** [`docs/tools/`](docs/tools/)
- **Release Notes:** [`CHANGELOG.md`](CHANGELOG.md)
- **License:** [`LICENSE`](LICENSE)

---

## Release Verification (`v2.0.3`)

- **Binary:** `bin/titan.exe` (`10,683,392` bytes, Windows x64 Native C++20)
- **SHA-256:** `d0b4f5bf77c58ee25a2237c61fc567660ec99d4fb3b421074a0cbe011447eef1`
- **Registered Commands:** `69` CLI commands / `53` in-process MCP tools
- **License:** Proprietary closed-source binary distribution — see [`LICENSE`](LICENSE).
