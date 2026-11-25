## 30. `titan tx` — Multi-File Atomic Transaction Engine & Rollback Journal

### Verbatim Help Manual
```text
Usage: titan tx <SUBCOMMAND> [OPTIONS]

Multi-File Atomic Transaction Engine with 3-Phase Commit & Rollback Journal

Subcommands:
  begin                     Start a new staged transaction
  add <FILE> [RANGE]        Stage an edit operation (supports --content, --input, --expect-hash, --delete, --insert)
  preview                   Preflight-validate all staged operations and show unified diffs
  commit                    Execute 3-phase atomic commit across all staged files
  rollback                  Restore all files from the last committed transaction journal
  abort                     Discard the currently staged transaction without touching files
  status                    Inspect currently staged operations and last rollback journal
  apply <MANIFEST.json>     Run a multi-file batch JSON manifest atomically

Common Options:
  --tx-dir <DIR>            Directory for transaction state & rollback journal (default: .titan)
  --validate <CMD>          Run command after atomic writes; exit != 0 triggers automatic rollback
  -b, --backup              Create collision-proof .orig backups for modified files
  -n, --dry-run             Preflight and preview diffs without modifying disk
  --force                   Overwrite existing staged transaction on begin
  -j, --json                Emit structured JSON envelope
```

### Practical Examples
```powershell
titan tx begin -j
titan tx add src/a.cpp --range 10:12 --content "return 42;" -j
titan tx commit --validate "cmake --build build --target titan" -b -j
titan tx rollback -j
```
