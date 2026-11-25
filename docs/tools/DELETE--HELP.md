## 40. `titan delete` — Safe Windows File & Folder Deletion Engine

### Verbatim Help Manual
```text
Usage: titan delete [options]

Targets:
  --target <file>          Delete a single file (repeatable)
  --folder <folder>        Delete a folder and everything inside it (repeatable)
  --files <pattern>        Delete files matching a wildcard such as "*.css" (repeatable)
  --empty-folders          Remove empty folders under --path

Scope:
  --path <folder>          Base folder for --files and --empty-folders (default: current folder)
  --recursive              Search sub-folders when using --files
  --contents-only          With --folder, keep the folder and delete only its contents
  --exclude <pattern>      Skip names matching the pattern (repeatable)
  --include-hidden         Include hidden and system files in --files
  --case-sensitive         Match patterns case-sensitively

Filters (--files):
  --older-than <time>      Examples: 30d, 12h, 90m, 2w
  --newer-than <time>
  --larger-than <size>     Examples: 10MB, 500KB
  --smaller-than <size>

Behavior:
  --recycle                Move to the Recycle Bin instead of deleting permanently
  --secure                 Overwrite file contents before deleting
  --passes <1-10>          Overwrite passes for --secure (default 1)
  --force                  Also delete read-only items
  --dry-run                Show what would be deleted without deleting
  --yes                    Do not ask for confirmation
  --verbose                Print every deleted item
  --quiet                  Print errors only
  -j, --json               Emit structured JSON summary
  --help                   Show this help

Exit codes: 0 success, 1 failures, 2 usage error, 3 aborted
```
- **Safety Requirement (`--empty-folders`):** `--empty-folders` requires `--path <folder>` explicitly (exit code 2 if omitted, never falling back silently to the current working directory). When invoked through the `.ti` Tier-2 bridge, `stdout`/`stderr` diagnostics are captured and surfaced cleanly.

### Practical Examples
```powershell
titan delete --target "style.css" --yes
titan delete --folder "build_tmp" --yes -j
titan delete --files "*.log" --path "logs" --older-than 30d --recursive --dry-run
titan delete --folder "cache" --contents-only --recycle --yes
titan delete --target "secret.key" --secure --passes 3 --yes
titan delete --empty-folders --path "D:\Music" --yes
```
