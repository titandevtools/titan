## 16. `titan hex | rgb | hsl | hsla | cmyk | named | multi` — CSS Color Engine

### Verbatim Help Manual
```text
Subcommands:
  titan hex [OPTIONS] [FILE | COLOR_STRING]
  titan rgb [OPTIONS] [FILE | COLOR_STRING]
  titan hsl [OPTIONS] [FILE | COLOR_STRING]
  titan hsla [OPTIONS] [FILE | COLOR_STRING]
  titan cmyk [OPTIONS] [FILE]
  titan named [OPTIONS] [FILE]
  titan multi [OPTIONS] [FILE]
  titan color-tips

Direct Color Format Conversion Flags (when passing a color literal):
  -hex               Convert input color to #RRGGBB / #RRGGBBAA
  -rgb               Convert input color to rgb(r, g, b) / rgba(...)
  -hsl               Convert input color to hsl(h, s%, l%) / hsla(...)
  -name              Convert input color to nearest CSS named color (e.g. RED, BLUE, GREEN)

File Extraction & Transformation Flags:
  -i <file>          Input file path
  -o <file>          Output file path
  -u                 Convert output to UPPER CASE
  -l                 Convert output to lower case
  -unique            Remove duplicate colors from result
  -duplicates        Extract only colors that appear more than once
  -subf              Search recursively in subfolders
  -lc                       Extract only light colors (luminance >= 50%)
  -dc                       Extract only dark colors (luminance < 50%)
  -n, --hex-number <3|6|8>  Extract only hex colors with N digits (-n 3, -n 6, -n 8)
  -6, --hex6                Shortcut for 6-digit hex colors (#RRGGBB)
  -3, --hex3                Shortcut for 3-digit hex colors (#RGB)
  -8, --hex8                Shortcut for 8-digit hex colors (#RRGGBBAA)
  -lighted-N                Lighten extracted colors by N% (1-100), use with -s on single-format commands to swap
  -darked-N          Darken extracted colors by N% (1-100), use with -s on single-format commands to swap
  -s                 Swap matched/transformed colors back into the source text (single-format commands only; exit 2 on multi)
  -j, --json         Output structured JSON for AI agents
```

> **`titan multi` Feature Parity & Read-Only Guard:** `titan multi` shares full filtering, deduplication, and transform parity with single-format color commands (`-unique`, `-duplicates`, `-lc`, `-dc`, `-u`, `-l`, `-lighted-N`, `-darked-N`, `-n`/`-3`/`-6`/`-8`, overlap deduplication, and exact `hsl` vs `hsla` typing), while explicitly rejecting `-s` (`exit 2`).

### Practical Examples
```powershell
# 1. Direct color conversions
titan rgb "rgb(255, 0, 0)" -hex        # -> #FF0000
titan hex "#ff0000" -name              # -> RED
titan hsl "hsl(240, 100%, 50%)" -name  # -> BLUE
titan hsla "hsla(120, 100%, 25%, 1)" -name # -> GREEN

# 2. Extract all unique HEX colors from a CSS directory recursively in JSON
titan hex -i src/styles -subf -unique --json

# 3. Extract ONLY hex colors by digit count using -n or --hex-number:
titan hex -n 6 -i styles.css -unique
titan hex -n 3 "#fff #123456 #12345678"         # -> #fff
titan hex -n 6 "#fff #123456 #12345678 #aabbcc" # -> #123456, #aabbcc
titan hex -n 8 "#fff #123456 #12345678"         # -> #12345678
titan hex --hex-number 6 -i app.js -u -unique

# 4. Darken all HEX colors in a stylesheet by 15% and write the modified CSS to dark_theme.css
titan hex -i styles.css -darked-15 -s -o dark_theme.css
```
