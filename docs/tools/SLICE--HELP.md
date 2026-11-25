## 5. `titan slice` — Zero-Copy Surgical Line-Range Reader & Extractor

### Verbatim Help Manual
```text
Usage: titan slice [OPTIONS] [--] <FILE> [RANGE...]

Zero-copy surgical line-range reader & extractor for AI Agents & developers

Range Formats (comma-separated or multiple args):
  START:END          1-based inclusive line range (e.g. 100:180)
  START:+COUNT       Start line plus COUNT lines (e.g. 50:+30)
  START: / :END      Open-ended from START to EOF or line 1 to END
  tail:N             Last N lines of the file (e.g. tail:50)

Options:
  -n, --lines        Prefix lines with 1-based line numbers (default)
  --raw              Output raw lines without line number prefixes
  --sha256, --hash   Include file SHA-256 and slice SHA-256 fingerprints
  -C, --context <N>  Expand range(s) by N lines before and after
  -B, --before <N>   Expand range(s) by N lines before
  -A, --after <N>    Expand range(s) by N lines after
  --symbol <NAME>    Slice symbol(s) by name (comma-separated or repeatable)
  --around <PAT>     Slice lines around first match (default -C 5)
  -E, --regex        Treat --around pattern as regex
  --all-matches      With --around, slice around every matching line
  --max-tokens <N>   Cap output to ~N tokens with pagination metadata
  --dedent           Strip common leading indentation from sliced block
  --strip-blank      Omit blank/whitespace-only lines
  --max-line-len <N> Truncate lines longer than N characters
  -o, --output <F>   Write sliced content atomically to file F
  --append           Append to --output file instead of replacing
  --force, --overwrite Allow overwriting existing --output file
  -b, --backup       Create collision-proof .orig backup before overwriting
  --dry-run          Preview --output write without modifying disk
  -j, --json         Structured JSON output with file & slice telemetry
```

### Practical Examples
```powershell
# 1. Multi-range slice in a single call with SHA-256 integrity hashes
titan slice src/engine/video.cpp 1:45,620:650 --hash --json

# 2. Slice a symbol directly with dedent and blank-line stripping
titan slice src/engine/replace.cpp --symbol execute --dedent --strip-blank

# 3. Read the last 80 lines of a log file under a strict token budget
titan slice app.log tail:80 --max-tokens 600 --json

# 4. Atomically extract selected line ranges into a new source file
titan slice big.cpp 1:50,600:900 --raw -o part.cpp --force
```
