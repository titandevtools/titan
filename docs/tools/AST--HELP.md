## 26. `titan ast-search | ast-replace` — Structural AST Pattern Search & Rewrite Engine

### Verbatim Help Manual
```text
Usage: titan ast-search [OPTIONS] PATTERN [PATHS...]
Structural AST pattern matching ignoring comments & whitespace.
Metavariables: $VAR (single node/expr), $$$ARGS (0+ nodes), $_ (wildcard).

Options:
  --lang <L>             c, cpp, py, js, ts, rs, go, cs, json
  -r, -R, --recursive    Recurse directories
  -g, --include <GLOB>   Filter files
  --respect-gitignore    Honor .gitignore rules
  -q, --quiet            Quiet mode
  -j, --json             Output JSON envelope with coordinates & bindings

Usage: titan ast-replace [OPTIONS] PATTERN REPLACEMENT [PATHS...]
Structural AST rewrite preserving formatting outside matched spans.

Options:
  --lang <L>             c, cpp, py, js, ts, rs, go, cs, json
  -i, --in-place         Apply changes atomically in place
  -b, --backup           Create collision-proof backup (.orig, .orig.~N~)
  -n, --dry-run          Preview unified diff without writing files
  -r, -R, --recursive    Recurse directories
  -g, --include <GLOB>   Filter files
  --respect-gitignore    Honor .gitignore rules
  -q, --quiet            Quiet mode
  -j, --json             Output structured JSON envelope
```

### Practical Examples
```powershell
titan ast-search -r --respect-gitignore "malloc($SIZE)" src/ -j
titan ast-replace -r -n "old_call($A, $$$REST)" "new_call($$$REST, $A)" src/ -j
```
