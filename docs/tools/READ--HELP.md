## 24. `titan read` — Agent-Oriented Universal File Reader & Linear-Time Regex Engine

### Verbatim Help Manual
```text
Usage: titan read [OPTIONS] [--] <FILES or DIRECTORIES...>

Agent-oriented file reader and searcher. Reads UTF-8, UTF-8 BOM, UTF-16 and legacy ANSI
files, skips binaries, and always emits valid UTF-8. Regex engine is linear-time (no ReDoS).

Input:
  -i, --input <path>          File or directory (repeatable). '-' reads stdin. Positional paths work too.
  -g, --glob <pattern>        Filter files found in directories (repeatable). Supports *, **, ?, [..], {a,b}.
                              Prefix with '!' to exclude. Directories are scanned recursively (.git skipped).

Line selection:
  --line, --lines <spec>      Lines to read: N | A-B | A- | -B | tail:K, comma separated (1-based).
  -from, --from <N>           Start at line N (to the end). Bound it with --limit.
  --all                       Read everything and disable the default output caps.
                              Without --all/--limit, output is capped (2000 records, 1 MiB).
  --limit <N>                 Stop after N records.

Search (a line matches if ANY pattern matches):
  -string, --strings <text>   Literal text (repeatable).
  -regex, --regex <pattern>   Regular expression (repeatable). Supports . [] \d \w \s \b ^ $ | () (?:)
                              * + ? {n,m} lazy variants, (?i), \xHH, \x{H..}. No backreferences/lookaround.
  -case-insensitive, -ignore, --case-insensitive, --ignore-case
                              Ignore case in matching, --unique, --duplicates and --sort.
  -word, --word-match         Match whole words only.
  --only-matching             Output only the matched text.
  --context-lines <N>         Context lines around matches. -before/--before <N>, -after/--after <N> override.

Line filters (applied before searching):
  -filter, --filter <kinds>   blank, nonblank, comments, nocomments, code, ascii, nonascii (comma separated).
                              Comment detection depends on the file extension.
  -len, --length <spec>       Keep lines by length in characters: N | A-B | A- | -B | >N | >=N | <N | <=N.

Output shaping:
  -upper, -lower, -title      Convert output case (Latin-1, Greek and Cyrillic aware; Arabic untouched).
  -u, --unique                Drop repeated records (first occurrence wins).
  -duplicate, --duplicates    Show only records that appear more than once.
  -sort, --sort[=mode]        asc (default) | desc | natural | length | count. Numeric when --numbers is used.
  -num, --numbers             Extract numbers (ints, decimals, exponents, hex, Arabic-Indic digits).
  -count, --counts            Count records per file; with --unique/--duplicates prints 'count<TAB>text'.
  -line-number, --line-number, -line-numbers, --line-numbers
                              Prefix records with their line numbers.
  -sep, --separator <text>    Record separator (default \n). Escapes: \n \t \r \0 \\.
  --json                      One JSON document: results, per-file info, summary (numbers statistics included).

Exit codes: 0 ok, 1 no matches, 2 error.
```

### Practical Examples
```powershell
# 1. Read lines 50 through 100 with line numbers
titan read --lines 50-100 src/main.cpp --line-numbers

# 2. Search for regex pattern with 3 lines of context
titan read --regex "class\s+[A-Za-z0-9_]+" include/ --glob "*.hpp" --context-lines 3

# 3. Extract and sort unique numeric values formatted as JSON
titan read --numbers --unique --sort data.txt --json

# 4. Filter code only (stripping comments and blanks)
titan read --filter nocomments,nonblank src/engine/read.cpp
```
