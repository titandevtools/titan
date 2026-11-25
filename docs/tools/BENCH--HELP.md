## 42. `titan bench` — High-Precision Win32 Benchmark & Telemetry Runner (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan bench [OPTIONS] [--] <command1> [command2 ...]

Native high-precision Win32 C++20 command execution & comparison benchmarking engine.
All options strictly require double dashes (--). Single-dash flags are rejected.

Execution & Shell Control:
  --shell <cmd|pwsh|none>      Execution shell mode (default: cmd)
  --warmup <N>                 Warmup runs before timing (default: 0)
  --runs <N>                   Exact number of timed runs per command
  --min-runs <N>               Minimum timed runs in adaptive mode (default: 10)
  --max-runs <N>               Maximum timed runs cap in adaptive mode
  --timeout <MS>               Per-run timeout in milliseconds (0 = no timeout)
  --ignore-failure             Continue even if a command exits non-zero or times out
  --verbose                    Print detailed per-run telemetry to stderr
  --env <KEY=VAL>              Set/override environment variable (repeatable)

Lifecycle Hooks, Labels & Parameter Sweeps:
  --setup <CMD>                Run once before each benchmark case begins
  --prepare <CMD>              Run before every single run (warmup and timed)
  --cleanup <CMD>              Run after every single run (warmup and timed)
  --conclude <CMD>             Run once after each benchmark case finishes
  --name <LABEL>               Custom display label for commands (repeatable)
  --param <NAME=v1,v2,...>     Discrete parameter sweep substituting {NAME}
  --param-range <NAME=a:b:s>   Numeric range sweep (start:end:step) for {NAME}

Output & Exports:
  --help                       Show this help message and exit
  --json                       Emit structured JSON telemetry output
  --export-markdown <FILE>     Export summary comparison table as Markdown
  --export-csv <FILE>          Export full statistical telemetry as CSV
  --output <FILE>              Write primary output (text or JSON) to a file
  --sort <none|mean|median>    Sort output rows (default: none)
  --no-color                   Disable ANSI terminal colors
```

### Examples
```powershell
titan bench --warmup 2 --runs 10 --shell none 'titan find src'
titan bench --warmup 1 --runs 5 --export-markdown bench.md --json 'cmd /c echo A' 'cmd /c echo B'
```
