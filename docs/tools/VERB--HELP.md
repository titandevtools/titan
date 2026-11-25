## 8. `titan verb` — Offset-Tolerant Atomic Patching & Instant Rollback

### Verbatim Help Manual
```text
Usage: titan verb apply [OPTIONS] --input <patch_file> [target_file]
       titan verb rollback [OPTIONS] <target_file>

Atomic patch application & rollback engine with collision-proof backups

Subcommands:
  apply                  Apply a unified diff patch atomically (default)
  rollback, undo         Restore a file atomically from its latest .orig backup

Options:
  --input, -i <file>     Patch file to apply (or '-' for stdin)
  --backup, -b           Create versioned backup (.orig, .orig.~1~, ...)
  --reverse, -R          Apply patch in reverse (swap additions and deletions)
  --dry-run              Verify whether patch applies cleanly without writing
  -j, --json             Machine-readable JSON output for AI agents
```

### Practical Examples
```powershell
# 1. Verify if a patch applies cleanly without modifying disk
titan verb apply --dry-run --input fix.patch src/main.cpp

# 2. Apply patch atomically and save collision-proof backup (.orig, .orig.~1~)
titan verb apply --backup --input fix.patch src/main.cpp

# 3. Revert/undo the last modification to src/main.cpp from its latest backup
titan verb rollback --json src/main.cpp
```
