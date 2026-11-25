## 28. `titan table` — Streaming SQL-Lite Analytics (`CSV`, `TSV`, `JSONL`)

### Verbatim Help Manual
```text
Usage: titan table [OPTIONS] "SELECT ..." FILE1 [FILE2...]
Streaming SQL-lite analytics across CSV, TSV, and JSONL files.
Aggregates: COUNT, SUM, AVG, MIN, MAX, MEDIAN, P90, P95, P99.

Options:
  -Q, --query <SQL>     Explicit SQL query string
  -f, --format <FMT>    csv, tsv, jsonl (auto-detected from extension)
  -d, --delimiter <CH>  Custom input delimiter
  --csv / --tsv         Emit result rows as CSV or TSV
  -j, --json            Emit uniform JSON envelope
```

### Practical Examples
```powershell
titan table "SELECT dept, COUNT(*), AVG(score), P95(score) FROM t1 GROUP BY dept ORDER BY dept" metrics.csv -j
```
