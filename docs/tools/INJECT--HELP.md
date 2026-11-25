## 31. `titan inject` / `titan injection` — Surgical Code & Text Injection

### Verbatim Help Manual
```text
Usage: titan inject [OPTIONS] <FILE>
       titan injection [OPTIONS] <FILE>

Surgical line, column, pattern, and symbol code/text injector with
single-block formatting, auto-indentation, UTF-8 column math, and safety locks.
NOTE: Only double-dash ('--') options are accepted by 'titan inject'.

Placement & Anchors:
  --line <N|A:B>          Target 1-based line number or range A:B
  --col <N>               1-based Unicode codepoint column (requires single --line)
  --clamp                 Clamp --col past line end to EOL instead of error
  --before                Insert before target line/column (default)
  --after                 Insert after target line/column
  --start-of-line         Insert at column 1 of target line(s)
  --end-of-line           Insert before line ending of target line(s)
  --top                   Insert at line 1 (preserves UTF-8 BOM)
  --bottom                Append cleanly at EOF
  --before-pattern <PAT>  Anchor before line matching <PAT> (literal or --regex)
  --after-pattern <PAT>   Anchor after line matching <PAT> (literal or --regex)
  --before-symbol <NAME>  Anchor immediately before symbol definition
  --after-symbol <NAME>   Anchor immediately after symbol closing boundary
  --inside-symbol <NAME>  Inject inside symbol body before closing boundary

Payload & Text Transforms:
  --text <TEXT>           Inline payload (unescapes \n, \t, \r, \\ unless --raw)
  --raw                   Treat --text literally without escape expansion
  --from-file <PATH>      Read payload verbatim from file
  --stdin                 Read payload verbatim from standard input
  --case <MODE>           Transform payload: upper|lower|capitalize|title|snake|camel
  --trim                  Trim leading/trailing whitespace from payload

Language, Formatting & Indentation:
  --lang <TYPE>           Language: auto|cpp|c|cs|java|js|ts|json|css|html|xml|svg|sql|py
  --auto-indent           Match surrounding anchor indentation
  --format-block          Expand & format ONLY the injected block
  --indent-width <N>      Spaces per indent level (default: auto-inferred or 4)
  --use-tabs              Use tabs instead of spaces for indent/formatting
  --newline <MODE>        Line ending policy: auto|crlf|lf (default: auto)

Replacement, Deduplication & Safety Gates:
  --replace               Replace target line(s) or --col span (--replace-len)
  --replace-len <N>       Overwrite N Unicode codepoints from --col
  --unique                Skip cleanly (changed:false, exit 0) if already present
  --all-matches           Apply pattern injection to every matching line
  --regex                 Use linear-time Thompson NFA regex for pattern anchors
  --dry-run               Preview unified diff without writing disk or backup
  --backup / --no-backup  Create .orig backup before disk write (default: ON)
  --expect-hash <SHA256>  Require pre-edit SHA-256 hex prefix (>=12 hex chars)
  --check-syntax          Validate post-injection delimiter/JSON balance before write
  --json                  Emit structured JSON telemetry envelope
  --help                  Display this help message
```

### Practical Examples
```powershell
titan inject --inside-symbol calc --text "if (x < 0) { x = 0; }" --auto-indent --format-block --check-syntax --json src/calc.cpp
titan inject --line 1 --col 2 --before --text "X" --no-backup notes.txt
titan inject --after-pattern "^//\s*HOOKS" --regex --unique --text "register_hook();" --json src/app.cpp
```
