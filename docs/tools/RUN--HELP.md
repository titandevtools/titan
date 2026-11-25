## 32. `titan run` / `titan ti` — Native TITAN (`.ti`) Text-Processing Scripting Language

### Verbatim Help Manual
```text
Usage: titan run [OPTIONS] <script.ti> [script args...]
       titan run [OPTIONS] -c "<inline script>" [-- script args...]
       titan run --guide [-j]

Execute native TITAN (.ti) text-processing scripts.

Options:
  -c, --code <SCRIPT>    Execute inline .ti script text
  -i, --input <FILE>     Pre-bind 'input' variable to FILE
  --check                Validate syntax & imports without executing code
  -n, --dry-run          Preview 'save' operations without writing files
  -b, --backup           Create collision-proof .orig backup before overwriting (default)
  --no-backup            Disable .orig backup creation when overwriting files
  --max-steps <N>        Override execution step cap (default: 20000000, max: 1000000000)
  --guide, --spec        Print complete built-in .ti language reference
  -j, --json             Output structured JSON execution report
  -h, --help             Show this help message
```

### Practical Examples
```powershell
titan run --guide
titan run extract_colors.ti
titan run clean_logs.ti --dry-run -j
titan ti -c 'tita total = [1,2,3,4,5] | filter(x => x % 2 == 1) | reduce((a, b) => a + b, 0); print total'
```
