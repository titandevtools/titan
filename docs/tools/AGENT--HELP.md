## 21. `titan agent | context | symbol | deps | audit | edit` — AI-Powered Agent Intelligence Suite

### Verbatim Help Manual
```text
Usage:
  titan context <SYMBOL_OR_QUERY> [DIR_OR_FILE] [--max-tokens <N>] [-j]
  titan symbol <SYMBOL_NAME> [DIR_OR_FILE] [--def-only] [--refs-only] [-i] [-j]
  titan deps [FILE_OR_DIR] [--reverse <NAME>] [-j]
  titan audit [DIR_OR_FILE] [-j]
  titan edit <FILE> <START:END> [--content <TEXT> | --input <FILE> | --delete] [--expect-hash <SHA256>] [-b] [--batch <MANIFEST.json>] [--validate <CMD>] [-n] [-j]
```

### Practical Examples
```powershell
# 1. Build an AI-ready context package for a symbol capped at 2,000 tokens in JSON
titan context "ReplaceEngine" src --max-tokens 2000 --json

# 2. Find where a function/class is defined and every place it is called across the project
titan symbol "extract_symbols" src

# 3. Find all files in a project (or Unity Assets/ folder) that depend on a header or GUID
titan deps src --reverse "mmap.hpp"

# 4. Run a full security, technical debt, complexity hotspot & LLM token audit
titan audit src --json

# 5. Surgically replace lines 40:55 of a file only if its SHA-256 hash matches
titan edit src/app.cpp 40:55 --expect-hash 386ff5c9 --backup --content "int run() {\n    return 0;\n}"
```
