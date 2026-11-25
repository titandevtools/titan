## 10. `titan find` — Ultra-Fast Recursive Filesystem Discovery

### Verbatim Help Manual
```text
Usage: titan find [DIR...] [OPTIONS]

Ultra-fast recursive filesystem discovery engine (findutils replacement) - Pro Max Advanced

Options:
  -g, -name <pattern>     Glob match pattern (e.g. '*.cpp', 'test_*')
  -iname <pattern>        Case-insensitive glob match pattern
  -ext <ext>              Filter by file extension (e.g. 'cpp', 'txt')
  -exclude <pattern>      Exclude paths matching glob pattern
  -maxdepth <N>           Maximum directory recursion depth
  -mindepth <N>           Minimum directory recursion depth
  -type <f|d>             Filter by regular file (f) or directory (d)
  -size <[+|-]N[k|m|g]>   Filter by file size (+ larger, - smaller)
  -newer, --newer <file>  Only entries modified after <file>'s mtime
  --older-than <DUR>      Only entries older than duration (e.g. 30d, 12h, 45m, 60s)
  -empty, --empty         Only 0-byte files or empty directories
  -exclude-hidden         Skip hidden files/directories (dotfiles)
  --respect-gitignore     Skip files/directories matching .gitignore rules
  -follow                 Follow symbolic links (with cycle detection)
  --regex <pattern>       Regex match on path
  -sort <name|size|mtime> Sort results
  -r, --reverse           Reverse sort order
  --limit <N>             Cap returned entries after sorting (1..1000000)
  -c, -count, --count     Print only the total number of matched entries
  -delete                 Delete all matched entries
  --full, --full-paths    Print full resolved absolute paths
  --relative              Print paths relative to the scanned root
  -j, --json              Structured JSON output for AI agents
```

> **Multi-Root Discovery & Display Modes:** Pass multiple root paths in one command (`titan find dir1 dir2 dir3 [OPTIONS]`) with automatic deduplication of overlapping trees. Pass `--full` / `--full-paths` for canonical absolute paths or `--relative` for paths relative to each scanned root.

### Practical Examples
```powershell
# 1. Scan multiple roots for C++ files, sorted by name, capped to 20 results
titan find SOURCES\VIDEO SOURCES\AUDIO -ext cpp -sort name --limit 20

# 2. Count empty files or directories across a tree in JSON
titan find my-project --empty --count -j

# 3. Find log files older than 30 days with relative paths
titan find logs -ext log --older-than 30d --relative
```
