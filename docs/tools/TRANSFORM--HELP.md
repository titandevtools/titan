## 11. `titan transform` — Stream Text Transformation & Line Filtering (`sed`)

### Verbatim Help Manual
```text
Usage: titan transform [OPTIONS] [EXPRESSIONS...] [FILE]

Stream transformation and line filtering (modern sed replacement)

Options:
  -n, --quiet, --silent   Suppress automatic printing of pattern space
  -e <expr>               Add script expression to commands to execute

Supported Expressions:
  s/pattern/replacement/[g|i]  Substitute string or regex pattern
  <start>,<end>d               Delete lines within line range
  /<pattern>/d                 Delete lines matching pattern
  <start>,<end>p               Print lines within range
```

### Practical Examples
```powershell
# 1. Chain multiple expressions (-e): substitute and delete comments
titan transform -e "s/http:/https:/g" -e "/^#/d" urls.txt

# 2. Print only lines 10 to 25
titan transform -n "10,25p" src/main.cpp
```
