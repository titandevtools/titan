## 6. `titan tree` — Token-Efficient Workspace Directory Mapper

### Verbatim Help Manual
```text
Usage: titan tree [DIR] [OPTIONS]

Fast, token-efficient workspace tree & line telemetry for AI Agents

Options:
  --depth, -d, -L <N> Maximum directory depth (default: 4)
  --all, -a           Include hidden and build directories (.git, build, node_modules)
  -j, --json          Structured JSON workspace summary
```

### Practical Examples
```powershell
# 1. Display workspace hierarchy up to depth 2
titan tree my-project -L 2

# 2. Emit structured JSON workspace tree including file sizes
titan tree my-project -L 3 --json
```
