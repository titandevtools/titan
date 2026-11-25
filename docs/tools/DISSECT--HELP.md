## 49. `titan dissect` — Unified 20-Language Code & Text Dissection Super-Engine

### Verbatim Help Manual
```text
Usage: titan dissect [OPTIONS] <TARGET...>

Unified 20-Language Code & Text Dissection Engine (X-Ray + Outline + Slice + Read + Symbol + Context + Bundle)
Note: Strict '--' double-dash options ONLY (single-dash flags are rejected).

Primary Modes (default: --xray):
  --xray                       Unified file dossier: stats, SHA-256, outline, hotspots, imports & TODOs
  --outline                    Hierarchical 20-language symbol outline with [start:end] bounds
  --list [all|fn|method|class] Flat symbol listing table (default: all)
  --extract <SYMBOL>           Extract exact symbol source code (supports --body-only, --dedent)
  --lines <SPEC>               Surgical line slicing (e.g. 10:40, 1:20,80:95, tail:30)
  --around <LINE>              Slice centered around line number (use with --context-lines)
  --read                       Safe multi-encoding reader (UTF-8/UTF-16/ANSI, binary-safe)
  --resolve <SYMBOL>           Cross-project symbol definitions & caller-tagged call sites
  --context <QUERY>            AI Smart Context Packager enforcing strict --max-tokens budget
  --bundle <SYMBOL>            Full Symbol Dissection Bundle (code + SHA-256 + CC + imports + callers)
  --stats                      Code, comment, blank, complexity & token statistics
  --imports                    Extract imports, includes, and module dependencies
  --todos                      String-safe TODO/FIXME/HACK/NOTE technical debt scan
  --hotspots                   Rank highest cyclomatic-complexity functions/methods

Slicing, Reading & Filtering:
  --pattern <PAT>              Filter lines (literal BMH default; add --regex for Thompson NFA)
  --regex                      Interpret --pattern as linear-time regex
  --ignore-case                Case-insensitive matching
  --whole-word                 Whole-word boundary matching
  --invert                     Invert --pattern line match
  --filter <MODE>              Line filter: code, comments, nonblank, blank
  --numbers                    Extract numeric tokens with min/max/sum/mean stats
  --case <upper|lower|title>   Transform line text case
  --context-lines <N>          Surrounding context lines (or --before <N> / --after <N>)
  --match <REGEX>              Filter symbols by name regex
  --kind <KIND>                Symbol kind filter: all, fn, method, class
  --visibility <VIS>           Filter visibility: public, private, protected, internal
  --min-complexity <N>         Minimum cyclomatic complexity (also --max-complexity)
  --min-lines <N>              Minimum symbol line span (also --max-lines, --min-params, --max-params)
  --parent <NAME>              Filter nested symbols by parent class/namespace
  --top-level, --no-nested     Restrict to top-level / non-nested symbols
  --defs-only, --refs-only     Restrict --resolve to definitions or references
  --include-body               Attach definition source code inside --resolve output

Output Shaping, Budgeting & Atomic Export:
  --signatures                 Include full symbol signatures (alias: --signature)
  --complexity                 Include cyclomatic complexity column
  --body-only, --no-body       Extract only body / only signature
  --with-docs                  Include leading doc comments on --extract
  --dedent                     Strip common leading indentation
  --strip-comments             Remove comment-only lines
  --strip-blank                Remove blank lines
  --line-numbers, --raw        Force/suppress line numbers and headers
  --hash                       Include file_sha256 & slice_sha256 digests
  --max-tokens <N>             Enforce strict LLM token budget cap
  --max-line-len <N>           Truncate lines longer than N bytes
  --sort <KEY>, --reverse      Sort by: line, name, lines, params, kind, complexity
  --limit <N>, --first         Cap emitted results
  --count                      Print only matched count
  --format <FMT>               Output format: table, names, csv, markdown, json
  --json                       Emit standard TITAN JSON envelope
  --output <FILE>              Atomic file export (--force/--overwrite, --append, --backup)

Workspace Discovery:
  --lang <LANG>                Force language parser (20 languages)
  --recursive                  Traverse directories recursively
  --respect-gitignore          Honor .gitignore rules
  --all                        Include hidden/build directories
  --max-depth <N>              Maximum recursion depth
  --glob <PAT>, --exclude <P>  Include/exclude file globs
  --max-file-mb <N>            Maximum file size in MB (default: 16)
  --quiet, --strict, --help    Quiet mode / fail-fast on unreadable files / help
```

### Primary Modes
- **`--xray` (default):** Single-call complete dossier of a file or workspace — language, encoding, `file_sha256`, estimated tokens, code/comment/blank line stats, hierarchical outline with `[start:end]` & cyclomatic complexity, complexity hotspots, imports, and string-safe `TODO`/`FIXME` debt.
- **`--outline` / `--list [all|fn|method|class]`:** 20-language hierarchical outline or flat symbol table (`--signatures`, `--complexity`, `--format table|names|csv|markdown|json`).
- **`--extract <SYMBOL>`:** Surgical 20-language symbol source extraction (`--body-only`, `--no-body`, `--with-docs`, `--dedent`, `--strip-comments`, `--hash`).
- **`--lines <SPEC>` / `--around <LINE>` / `--read`:** Safe multi-encoding (`UTF-8`/`UTF-16LE`/`UTF-16BE`/`ANSI`, binary-safe) surgical slicing & filtered reading (`tail:N`, multi-range `1:20,80:95`, `--filter code|comments|nonblank|blank`, `--pattern` with BMH or `--regex` NFA, `--numbers`, `--case`, `--context-lines`, `--max-tokens`, `--max-line-len`, `--hash`, atomic `--output` with protected-path guard).
- **`--resolve <SYMBOL>`:** Cross-project zero-index definitions (`--defs-only`, `--include-body`) and whole-word call-site references (`--refs-only`) tagged with `enclosing_symbol`.
- **`--context <QUERY>`:** AI Smart Context Packager ranking definitions and call-site snippets strictly within `--max-tokens <N>` (default `4000`).
- **`--bundle <SYMBOL>`:** Single-call **Full Symbol Dissection Bundle** returning the symbol's full source code, `file_sha256`, `slice_sha256`, cyclomatic complexity, file imports, and cross-project callers within `--max-tokens`.
- **`--stats` / `--imports` / `--todos` / `--hotspots`:** Complete structural analytics across files or `--recursive` workspaces (`--respect-gitignore`).

### Examples
```powershell
titan dissect --json --signatures .\SOURCES\DISSECTING\src\engine\dissect.cpp
titan dissect --bundle DissectEngine --max-tokens 3000 --json .\SOURCES\DISSECTING
titan dissect --lines 1:30,tail:20 --hash --dedent .\src\app.cpp
titan dissect --filter code --pattern "return .*" --regex --json .\src\app.cpp
titan dissect --resolve parse_args --include-body --json .\src
```
