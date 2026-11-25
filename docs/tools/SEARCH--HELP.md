## 2. `titan search` — High-Performance Pattern, Regex & Fuzzy Search

### Verbatim Help Manual
```text
Usage: titan search [OPTIONS] PATTERN [FILES...]

Sophisticated, Agent-Grade Modern Search Engine (Full POSIX & Beyond)

Matching Criteria (Full & Abbreviated):
  -e, --or <pattern>              Add extra literal/regex OR pattern (repeatable)
  --and <pattern>                 Require line to ALSO match pattern (repeatable)
  --not <pattern>                 Exclude matching lines containing pattern (repeatable)
  --ignore, --ignore-case, -i     Ignore character case
  --smart-case, -S                Case-insensitive if pattern is all lowercase, else case-sensitive
  --invert, --invert-match, -v    Select non-matching lines
  --word, --word-match, -w        Match whole words only
  --fixed, --fixed-strings, -F    Treat pattern as fixed literal text
  --regex, -E                     Force pattern to linear-time Thompson NFA regex
  --multiline                     Multiline pattern boundary matching
  --fuzzy <N>                     Fuzzy search allowing Levenshtein distance <= N

Line Selection & Pre-Match Filters (Agent Intelligence):
  --range, --line-range <spec>    Restrict search to line ranges (N | A-B | A:B | A..B | tail:K)
  --from <N>                      Start searching from 1-based line N
  --length <spec>                 Filter lines by character length (N | A-B | >N | >=N | <N | <=N)
  --code                          Shorthand for '--line-filter code' (skip comments & blanks)
  --line-filter <kinds>           Filter lines: blank, nonblank, comments, nocomments, code, ascii, nonascii

Case Transformation & Extraction:
  --upper, --upper-case           Transform matching output to UPPER CASE (UTF-8 aware)
  --lower, --lower-case           Transform matching output to lower case (UTF-8 aware)
  --title, --title-case           Transform matching output to Title Case (UTF-8 aware)
  --num, --numbers                Extract numbers (ints, decimals, hex, Arabic-Indic) & emit stats
  --unique, -u                    Deduplicate matched records (first occurrence wins)
  --duplicates                    Show only matched records appearing more than once
  --sort[=mode]                   Sort matches: asc | desc | natural | length | count

Reporting & Output Control:
  --lines, --line-number, -n      Print line numbers
  --columns, --column             Print column numbers
  --with-symbol, --enclosing-symbol Annotate each match with its enclosing symbol & line span
  --count, --count-only, -c       Print only count of matches per file
  --extract, --only-matching, -o  Print only matched text fragments (all hits per line)
  --list-files, --files-with-matches, -l   Print only filenames with matches
  --list-without, --files-without-match, -L Print filenames with no match
  --trim, --trim-lines            Trim leading and trailing whitespace
  --max-line-len <N>              Truncate matched lines longer than N chars around hit (>= 16)
  --color, --colorized            Colorize matched text in terminal
  --quiet, --silent, -q           Suppress standard output
  --stats, --summary              Show performance telemetry & timing
  --json, --agent-json, -j        Rich structured JSON output for AI Agents

Context & Limits:
  --context, -C <N>               Print N lines of leading & trailing context
  --before, --before-context, -B <N> Print N lines of leading context
  --after, --after-context, -A <N>  Print N lines of trailing context
  --limit, --max-count, -m <N>    Stop scanning after N matches per file
  --max-total <N>                 Stop globally after N total matches across all files
  --max-tokens <N>                Cap global match output to ~N approximate tokens
  --with-filename, -H             Always prefix filename
  --no-filename, -h               Never prefix filename

Filesystem Discovery:
  --recursive, --subfolders, -r, -R Recursively traverse directories
  --type, -t <lang[,lang...]>     Filter by built-in language type (cpp, py, js, ts, rust, go, json...)
  --type-not, -T <lang[,...]>     Exclude built-in language type(s)
  --max-filesize <SIZE>           Skip files larger than SIZE (e.g. 500K, 5M, 1G)
  --depth, --max-depth <N>        Maximum directory recursion depth
  --min-depth <N>                 Minimum directory recursion depth
  --respect-gitignore             Honor .gitignore rules during recursive traversal
  --glob, --include, -g <glob>    Include/exclude glob (repeatable, supports {a,b}, **, !excl)
  --exclude <glob>                Exclude files matching glob (repeatable)
  --exclude-dir <glob>            Exclude directories matching glob (repeatable)
  --hidden, --include-hidden      Include hidden files (dotfiles)
  --follow-symlinks               Follow directory symbolic links
  --text, --binary, -a            Search binary files as text (auto-transcodes UTF-8/UTF-16/ANSI)
```

### JSON Telemetry Schema (`-j` / `--json`)
Returns a JSON object containing `query`, `stats` (`files_scanned`, `files_matched`, `total_matches`, `binary_files_skipped`, `oversized_files_skipped`, `truncated`, `estimated_tokens`, `elapsed_ms`, plus `numbers` `{count, sum, min, max, mean}` when `--num` is used), and a `matches` array of objects with `file`, `line`, `column`, `byte_offset`, `length`, `content`, `matched_text`, `encoding` (`utf-8`, `utf-16le`, `ansi`, etc.), `symbol` / `symbol_kind` / `symbol_start` / `symbol_end` (with `--with-symbol`), `value` (with `--num`), and `count` (with `--unique`/`--duplicates`).

### Practical Examples
```powershell
# 1. Fast recursive literal search with line numbers across *.cpp files, skipping build dir
titan search -n -r -g "*.cpp" --exclude-dir "build" "ReplaceEngine::execute" my-project

# 2. Search ONLY inside live source code (skipping comments & blank lines) with brace-expanded globs
titan search -r -g "*.{cpp,hpp}" --code -n "MemoryMappedFile" src/

# 3. Multi-pattern OR search inside specific line ranges, filtering lines by length
titan search --range 10:120 --length ">15" -e "error" -e "fatal" -n server.log

# 4. Extract, deduplicate, and numerically sort all numeric constants matching a pattern
titan search -r -g "*.hpp" --code --num --sort asc --unique -j "timeout" include/

# 5. Case-insensitive whole-word search with 2 lines of before/after context
titan search -i -w -n -C 2 "rollback" src/

# 6. Fuzzy search allowing edit distance <= 2 (finds "MemoryMappedFile" even if spelled "MemoryMapedFile")
titan search -n -r --fuzzy 2 "MemoryMapedFile" include/

# 7. Extract all matched regex tokens per line in structured JSON for AI Agents
titan search -E -o -j "std::[a-z0-9_]+" src/engine/replace.cpp
```