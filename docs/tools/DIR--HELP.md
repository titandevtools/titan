## 33. `titan dir` — Smart Directory Inspection, Classification & Diagnostics

### Verbatim Help Manual
```text
Usage: titan dir [DIR...] [OPTIONS]

Core Modes & Scope:
  --complete                Full directory intelligence report
  --summary                 Compact single-screen statistical overview
  --names                   Print clean file and directory basenames only
  --full-paths              Print full canonical/resolved paths
  --relative                Print paths relative to target DIR
  --directory, --folders    List directories/folders only
  --files-only              List files only
  -r, --recursive           Traverse subdirectories recursively
  --max-depth <N>           Limit traversal depth

Smart Category Filters (combinable):
  --text-files, --doc-files, --image-files, --audio-files, --video-files,
  --dev-files, --config-files, --archive-files, --executable-files, --font-files, --database-files

Extension, Pattern, Size & Time Filters:
  --extensions, --ext <e1,e2,...>, --exclude-ext <e1,e2,...>, -g/--glob <pat>,
  --exclude <p1,p2,...>, --respect-gitignore, --hidden, --empty,
  --min-size <SIZE>, --max-size <SIZE>, --recent <N[s|m|h|d]>, --older-than <N[s|m|h|d]>

Diagnostics & Export:
  --duplicates, --hash/--sha256, --largest <N>, --smallest <N>,
  --long-paths, --encoding-scan, --line-endings,
  --sort <name|size|ext|modified|count>, --asc/--desc, --limit <N>, --offset <N>,
  -H/--human-readable, -j/--json, --csv, --tsv
```

### Practical Examples
```powershell
titan dir src --full-paths -r
titan dir src --complete -r -j
titan dir src --encoding-scan --line-endings -r -j
titan dir assets --duplicates --largest 5 -H -j
```
