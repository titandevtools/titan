## 9. `titan compare` — Myers O(ND) Unified Diff & Binary Comparison

### Verbatim Help Manual
```text
Usage: titan compare [OPTIONS] <FILE1|DIR1> <FILE2|DIR2>

High-performance difference and byte comparison engine (diffutils replacement) - Pro Max Advanced

Options:
  -u, --unified          Output unified diff format (default)
  -q, --brief            Report only when files differ
  --bytes                Perform byte-by-byte binary comparison
  -U, --context <N>      Output N lines of copied context (default 3)
  -i, --ignore-case      Ignore case differences
  -w, --ignore-whitespace  Ignore leading/trailing/repeated whitespace
  -r, --recursive        Compare directories recursively
  --exclude <pattern>    Skip paths containing pattern (used with -r)
  --side-by-side         Show a two-column line comparison
  --stat                 Show a summary of added/removed lines and similarity
  --color                Colorize +/- lines in terminal output
  -o, --output <file>    Write output to file instead of stdout
  -j, --json             Structured JSON output for AI agents
```

### Practical Examples
```powershell
# 1. Standard unified diff with 3 lines of context
titan compare -u file_old.cpp file_new.cpp

# 2. Summary statistics (added, removed, kept lines, and similarity %) in JSON
titan compare --stat --json file_old.cpp file_new.cpp

# 3. Byte-for-byte binary comparison
titan compare --bytes build/titan.exe bin/titan.exe
```
