## 41. `titan dev` — Multi-Language Structural Code Analyzer & Symbol Extractor (20 Languages)

### Verbatim Help Manual
```text
Usage: titan dev [OPTIONS] <TARGET...>

Multi-language structural code analyzer, symbol lister, and extractor (20 languages).

Modes:
  -l, --list [all|fn|method|class]     List symbols (default mode)
  -x, --extract <NAME>                 Extract symbol source code (supports globs & Class.method)
      --extract-kind <KIND>            Filter extract kind (all|fn|method|class)
      --outline                        Print indented hierarchical outline
      --count                          Output matched symbol count only
      --stats                          Output file code/comment/complexity statistics
      --imports                        Extract file imports/includes
      --todos                          Extract TODO/FIXME/HACK/BUG/NOTE comments

Filtering:
  -L, --lang <LANG>                    Force language (e.g. cpp, py, js, ts, go, rs, sql, asm)
  -m, --match <REGEX>                  Filter symbols by regex on name/qualified name
  -i, --ignore-case                    Case-insensitive matching
      --visibility <VIS>               Filter by visibility (public|private|protected|internal|package)
      --async                          Only async/suspend functions
      --static                         Only static functions/methods
      --abstract                       Only abstract/pure-virtual functions
      --min-lines <N> / --max-lines <N> Filter by symbol line count
      --min-params <N> / --max-params <N> Filter by parameter count
      --min-complexity <N>             Filter by minimum cyclomatic complexity
      --max-complexity <N>             Filter by maximum cyclomatic complexity
      --parent <NAME>                  Filter symbols inside parent class/namespace
      --top-level                      Only top-level symbols (depth == 0)
      --no-nested                      Exclude nested inner functions
      --decorator <TEXT>               Filter symbols carrying matching decorator/attribute
      --declarations                   Include body-less declarations/prototypes
      --all-labels                     Include local labels in Assembly

Sorting & Output:
      --sort <line|name|lines|params|complexity|kind>
      --reverse                        Reverse sort order
      --limit <N>                      Limit number of symbols per file
      --first                          Keep only the first matched symbol per file
  -f, --format <table|names|csv|md>    Text output format (default: table)
  -j, --json                           Emit TITAN JSON envelope
      --signature                      Include signature column
      --complexity                     Include cyclomatic complexity column
      --with-docs                      Include preceding doc comments/docstrings
      --no-body / --body-only          Extract signature only or body only
  -n, --line-numbers                   Prefix extracted code with line numbers
  -C, --context <N>                    Add N context lines around extracted code
      --strip-comments                 Strip comments from extracted code
      --dedent                         Remove common leading indentation
      --raw                            Omit header comments in --extract output

Traversal & I/O:
  -r, --recursive                      Traverse directories recursively (auto-skips .git/build/node_modules)
  -a, --all                            Include hidden/build directories during recursive traversal
      --respect-gitignore              Honor .gitignore rules during recursive traversal
      --max-depth <N>                  Limit recursion depth
  -g, --glob <PAT>                     Include files matching glob
      --exclude <P1,P2,...>            Exclude files matching globs
      --max-file-mb <N>                Skip files larger than N MB (default: 16)
  -o, --output <PATH>                  Write output to file
      --force                          Overwrite existing --output file
  -q, --quiet                          Suppress non-error stderr messages
      --strict                         Return exit code 1 if no symbols match
  -h, --help                           Show this help
```
- **Supported Languages (20):** C++, C, C#, Java, Dart, JavaScript, TypeScript, PHP, Go, Rust, Kotlin, Swift, Python, Ruby, Lua, MATLAB, SQL, PowerShell, R, Assembly.
- **Mandatory AI-Agent Workflow Rule (Use `titan dev` First):** Whenever any AI model is asked to analyze, audit, inspect, or refactor a source file or directory, it **MUST** run `titan dev -r --complexity --signature --declarations <target>` and `titan dev -r --stats <target>` FIRST to obtain exact symbol boundaries, visibility, parameter counts, cyclomatic complexity (`CC`), and code/comment/blank line breakdowns, and use `titan dev -x "<SymbolName>" [-n] [--strip-comments] <file>` to extract targeted functions/classes without loading entire files into context.
- **Directory Safety & Token Efficiency:** Recursively auto-skips `.git`, `node_modules`, `build`, `buildings`, `.vs`, `dist`, `target`, `__pycache__`, and `.venv` unless `-a`/`--all` is passed. Rejects binary files, auto-decodes UTF-16/UTF-8 BOM, and enforces `--output` atomic writes + OS protected-path guard. Accurately counts EOF trailing newlines (no phantom extra blank line), accumulates multi-line Python/JS/TS imports, and ignores lowercase prose inside `--todos`.

### Key Options & Examples
```powershell
# 1. Full symbol table with visibility, line bounds, parameter counts, cyclomatic complexity & signatures:
titan dev -r --complexity --signature --declarations src/search

# 2. File-level code/comment/blank line counts and complexity summary:
titan dev -r --stats --imports --todos src/search

# 3. List all symbols in a single source file:
titan dev -l src/calc.cpp

# 4. Surgically extract a specific class method with docstrings, body-only, and dedented:
titan dev -x "Calc.add" --with-docs --body-only --dedent src/calc.cpp

# 5. Extract a function with 1-based line numbers and comments stripped to save AI context tokens:
titan dev -x "SearchEngine.search_in_text" -n --strip-comments src/engine/search.cpp

# 6. Find high-complexity hotspot functions (CC >= 8) sorted highest-first in JSON:
titan dev -r src --min-complexity 8 --sort complexity --reverse -j

# 7. Export complete Markdown audit report (--stats + --imports + --todos) atomically to a file:
titan dev -r src --stats --imports --todos -f md -o report.md --force

# 8. Count async Python functions across a repository:
titan dev -r . --async --lang py --count
```
