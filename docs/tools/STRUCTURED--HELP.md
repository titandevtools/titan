## 22. `titan convert | analyze | validate | fix` — Structured Data, Qt Designer & Sublime Text Engine

### Conversion matrix (verified by `tests/cli/run_structured_cli_tests.ps1`)
| Source | Targets verified |
| :--- | :--- |
| JSON | CSV, XML, YAML, TOML, INI |
| CSV | JSON, TSV, XML |
| XML | JSON |
| Qt `.ui` | JSON, and JSON back to `.ui` |
| `.sublime-settings` | JSON |
| `.sublime-snippet` | JSON, and back |
| `.sublime-syntax` | JSON, and back |
| `.tmTheme` | JSON, and back |

Other pairs (TSV, YAML, TOML, INI sources; HTML and other JSONC-based Sublime formats as targets) are wired in the same engine but not individually tested. Treat them as experimental.

### Sublime Text support
| Format | Convert | Analyze | Fix |
| :--- | :--- | :--- | :--- |
| `.sublime-syntax` | to/from JSON (semantic, not byte-identical) | metadata, undefined contexts and variables, unbalanced regex | tab indentation, missing `%YAML` header |
| `.sublime-color-scheme` | to JSON | undefined/unused variables, invalid colors, duplicate scopes | only if invalid; never rewrites valid files |
| `.tmTheme` | to/from JSON | structure, color values | XML normalization |
| `.sublime-snippet` | to/from JSON | required content, placeholders | XML normalization |
| `.sublime-settings`, `-keymap`, `-mousemap`, `-menu`, `-commands`, `-completions`, `-theme`, `-build`, `-project`, `-workspace`, `-macro` | to JSON | structure and basic semantic checks | JSONC repair only when file is invalid and comments would survive |
| Package directory | not applicable | scans every Sublime resource file | not applicable |

Cross-file resource checks (missing images, build/project paths) are not implemented.

### Known limitations
- Comments in JSONC/Sublime files are dropped when converting to strict JSON; the report sets `"lossy": true` and lists the omission. JSON back to a Sublime format does not restore them.
- `.sublime-syntax` round trip preserves meaning, not quoting style or comments. YAML support covers block mappings/sequences and flow collections only (no anchors, multi-line scalars, or comments in output).
- `.ui` round trip was checked with Qt `uic` 6.12.0 and a text check of connections, widget classes and names; no full structural diff tool exists yet. Reformatting may change whitespace.
- XML repair does not auto-close mismatched tags; it reports and exits 1. JSON repair handles trailing commas, comments (strict mode), BOM, raw newlines in strings, and up to 3 unclosed trailing containers.
- Lossy conversions that were observed: JSON null becomes `""` in TOML; nested values become inline JSON in CSV/INI.
- Sublime Text itself was not available for validation; compatibility was not tested against the application.

### Examples
```powershell
titan convert --input data.json --output data.csv
titan convert --input form.ui --output form.json
titan analyze --input MySyntax.sublime-syntax --json
titan validate Preferences.sublime-settings
titan fix --input data.json --dry-run
titan fix --input form.ui --backup --report fix.json
```
