## 13. `titan stats` — Statistical Aggregation, Percentiles & GroupBy (`datamash`)

### Verbatim Help Manual
```text
Usage: titan stats [OPERATION] [COLUMN] [FILE]
       titan stats groupby [GROUP_COL] [OPERATION] [VAL_COL] [FILE]

Mathematical and statistical aggregation engine (datamash replacement)

Operations:
  sum, mean (avg), median (p50), p90, p95, p99, iqr, min, max, range, count, pstdev, stdev, variance

Options:
  -t <sep>           Field separator
  --csv              CSV mode
  -j, --json         Output structured JSON for AI agents
```

### Practical Examples
```powershell
# 1. Fast zero-allocation mean, p95, and iqr on column 1
titan stats mean 1 numbers.txt
titan stats p95 1 numbers.txt
titan stats iqr 1 numbers.txt

# 2. GroupBy aggregation on CSV (group by column 1, sum column 3)
titan stats --csv groupby 1 sum 3 transactions.csv --json
```
