## 20. `titan format` — Multi-Language Code Formatter, Minifier & Syntax Validator (`JS`, `JSON`, `CSS`, `HTML`, `SQL`, `C++`)

### Verbatim Help Manual
```text
Usage: titan format [OPTIONS] <file_or_dir...>

Native C++20 Multi-Language Code Formatter, Minifier & Syntax Validator
Supported Languages:
  - JSON / JSONC (.json, .jsonc)       [Pretty-Print, Minify, Sort-Keys, Syntax Validation]
  - JavaScript / TypeScript (.js, .ts, .jsx, .tsx, .mjs)
  - CSS / SCSS / LESS (.css, .scss, .less)
  - HTML / XML / SVG (.html, .htm, .xml, .svg)
  - SQL (.sql)
  - C / C++ / C# / Java (.c, .cpp, .h, .hpp, .cs, .java)

Options:
  -i, --in-place       Format file(s) atomically in-place
  -b, --backup         Create collision-proof backup (.orig) before modifying in-place
  -m, --minify         Minify code (strip comments & unnecessary whitespace)
  -c, --check          Check syntax & formatting without modifying (exit 1 if unformatted/invalid)
  -n, --dry-run        Preview formatting status without modifying files
  -s, --sort-keys      Sort object keys alphabetically (JSON)
  --indent <N>         Number of spaces per indentation level (default: 2)
  -t, --tabs           Use tabs instead of spaces for indentation
  -l, --lang <LANG>    Explicitly set language (json, js, ts, css, html, xml, svg, sql, cpp)
  -r, --recursive      Format all supported files in directory recursively
  -o, --output <FILE>  Write formatted result to specific output file
  -j, --json           Emit structured JSON report (status, bytes saved/changed, syntax errors)
```

### Practical Examples
```powershell
# 1. Pretty-print and alphabetically sort keys in a JSON file in-place
titan format config.json --sort-keys -i

# 2. Minify a JavaScript or CSS file into a .min.js / .min.css output file
titan format app.js --minify -o app.min.js
titan format styles.css --minify -o styles.min.css

# 3. Validate JSON/JS/CSS syntax and formatting across an entire directory in JSON mode
titan format .\src -r --check --json

# 4. Format all JS, JSON, CSS, and HTML files in a project in-place with 4-space indentation
titan format .\web_project -r --indent 4 -i
```
