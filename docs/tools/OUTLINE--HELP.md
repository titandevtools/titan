## 4. `titan outline` — Structural Code AST Symbol & Line-Bound Extractor

### Verbatim Help Manual
```text
Usage: titan outline [OPTIONS] <FILE...> 

Instant structural code outline (AST-lite symbol & line-bound extractor for AI Agents)

Options:
  --kind <type>      Filter by symbol kind (function, class, struct, enum, namespace, include)
  --no-includes      Omit #include and import directives
  -j, --json         Structured JSON output with exact [start_line, end_line] bounds
```

### Practical Examples
```powershell
# 1. View compact structural outline of a C++ file (omitting #includes)
titan outline src/engine/replace.cpp --no-includes

# 2. Extract only function definitions in machine-readable JSON
titan outline --kind function --json src/engine/search.cpp
```
