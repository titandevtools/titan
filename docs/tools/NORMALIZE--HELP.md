## 48. `titan normalize` — Batch Encoding, EOL, Indentation & Whitespace Normalizer (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan normalize [OPTIONS] [--] <file_or_dir...>

Batch text encoding, line-ending, indentation & whitespace normalizer.
All options strictly require double dashes (--). Single-dash flags are rejected.

Transform Options (double-dash ONLY):
  --lf                         Normalize line endings to LF (\n)
  --crlf                       Normalize line endings to CRLF (\r\n)
  --eof-nl                     Ensure non-empty files end with a trailing newline
  --no-eof-nl                  Remove trailing newline at end of file
  --trim-trailing              Strip trailing spaces and tabs on every line
  --trim-leading               Strip leading spaces and tabs on every line
  --tabs-to-spaces <N>         Expand tab characters using column width N (1..16)
  --spaces-to-tabs <N>         Convert leading indent runs of N spaces into tabs (1..16)
  --collapse-blank-lines <N>   Collapse runs of blank lines to at most N (0..10)
  --strip-control              Remove stray ASCII control bytes (keeps \t, \r, \n)
  --bom                        Add UTF-8 BOM (default strips UTF-8 BOM)
  --keep-bom                   Preserve UTF-8 BOM if present

Discovery & Output Options:
  --recursive                  Traverse directories recursively
  --all                        Include hidden/.git/build directories
  --glob <PAT>                 Include files matching glob
  --exclude <PAT>              Exclude files matching glob
  --respect-gitignore          Honor .gitignore rules
  --check                      Check if files need normalization (exit 1 if any)
  --dry-run                    Preview changes without writing to disk
  --diff                       Print unified diff preview for modified files
  --no-backup                  Skip creating .orig backup before modifying
  --quiet                      Suppress per-file output
  --json                       Emit structured TITAN JSON envelope
  --help                       Show this help
```

### Examples
```powershell
titan normalize --lf --trim-trailing --tabs-to-spaces 4 --eof-nl --dry-run --diff .\src
titan normalize --lf --trim-trailing --recursive --glob '*.cpp' --json .\SOURCES
```
