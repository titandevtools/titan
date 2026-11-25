## 12. `titan process` — Structured Record, AWK & RFC 4180 CSV Engine (`gawk`)

### Verbatim Help Manual
```text
Usage: titan process [OPTIONS] 'PROGRAM' [FILE]

Structured record, AWK and CSV processing engine

Options:
  -F <sep>           Field separator (default: whitespace)
  --csv              RFC 4180 CSV mode with quote handling
  -j, --json         Output structured JSON rows for AI agents
```

### Practical Examples
```powershell
# 1. Extract columns 1 and 3 from whitespace-delimited text
titan process '{print $1, $3}' table.txt

# 2. Extract columns 2 and 4 from an RFC 4180 CSV file (handles commas inside quotes)
titan process --csv '{print $2, $4}' report.csv
```
