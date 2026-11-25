## 3. `titan replace` — Atomic Replacement, Line-Scoping & Two-Way Smart-Swap


### Verbatim Help Manual
```text
Usage: titan replace [OPTIONS] PATTERN REPLACEMENT FILE [FILES...]
       titan replace [OPTIONS] -swap A B FILE [FILES...]
       titan replace [OPTIONS] -smart-swap A B FILE [FILES...]
       titan replace [OPTIONS] --map-file <file> FILE [FILES...]

Advanced, multi-file, regex-aware replacement engine with atomic safety

Matching & Scoping:
  --regex, -E                   Force PATTERN to be treated as a regular expression
  --fixed, --fixed-strings, -F  Treat PATTERN strictly as literal text
  --ignore, --ignore-case       Case-insensitive matching
  --word, --word-match, -w      Match only whole words
  --multiline                   Allow ^/$ to match embedded line boundaries
  --lines, --line-range <S:E>   Restrict replacements to 1-based line range (e.g. 10:50)
  --max-replacements <N>        Limit total replacements per file

Swap mode (two-way exchange within the same file):
  -swap A B                     Swap every occurrence of A with B and B with A, in one pass
  -smart-swap A B               Same as -swap, but case-insensitive, whole-word, and
                                preserves the original case of each matched text

Replacement text case:
  --upper, --upper-case         Force replacement text to UPPER CASE
  --lower, --lower-case         Force replacement text to lower case
  --title, --title-case         Force replacement text to Title Case
  --preserve, --preserve-case   Match the case pattern of each matched text

Batch mode:
  --map-file <file>             Tab-separated PATTERN<TAB>REPLACEMENT pairs, one per line

File selection:
  --recursive, -r, -R           Apply to files within directories recursively
  --include, -g <glob>          Only process files matching glob (recursive mode)
  --exclude <glob>              Skip files matching glob (recursive mode)
  --exclude-dir <glob>          Skip directories matching glob (recursive mode)
  --follow-symlinks             Follow symbolic links while recursing
  --hidden, --include-hidden    Include hidden files and directories

Safety & output:
  --in-place, -i                Edit file(s) in place
  -i<ext>                       Edit in place and back up with extension (e.g. -i.bak)
  --backup                      Create collision-proof backup (.orig, .orig.~N~)
  --dry-run, -n                 Preview unified diff without modifying files
  --quiet, -q                   Suppress normal output, only set exit status
  --json, -j                    Machine-readable JSON output for AI agents
```