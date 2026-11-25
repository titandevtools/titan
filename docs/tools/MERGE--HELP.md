## 50. `titan merge` — Streaming Multi-Format File Merger (`--` ONLY)

### Overview
`titan merge` (`MergeEngine`) merges two or more files into a single output (or split outputs) across text, binary, lines, bytes, JSON, JSONL, CSV, TSV, XML, HTML, SRT, VTT, and M3U formats with streaming O(1)-RAM processing for binary and line-by-line text streams.

### Strict Interface Rules
- All options MUST start with double dashes (`--`); short flags (`-x`) and unknown options are rejected with exit code `2`.
- Value options accept both `--opt value` and `--opt=value`.
- Boolean options provide negated forms (`--no-...`, `--clobber`, `--write`).
- Positional arguments are input file paths only (use `--` to stop option parsing).
- Output files inside an input directory/glob are automatically excluded from inputs.
- Conflicting options (e.g. `--overwrite` + `--no-clobber`, `--stdout` + `--output`) fail with exit code `2`.

### Exit Codes
- `0`: Success
- `1`: Runtime error (I/O failure, verification mismatch, `--max-output-size`, `--fail-on-empty`, `--fail-on-missing`, `--fail-on-encoding-error`)
- `2`: Invalid usage, unknown option, short flag, conflicting options, or protected system path
- `3`: Partial failure (`--continue-on-error` with at least one succeeded and one failed input)

### Option Groups
- **Input:** `--input`, `--input-list`, `--input-glob`, `--stdin`, `--recursive`, `--max-depth`, `--include`, `--exclude`, `--include-ext`, `--exclude-ext`, `--min-size`, `--max-size`, `--modified-after`, `--modified-before`, `--follow-symlinks`, `--skip-missing`, `--skip-empty-files`, `--skip-hidden`, `--ignore-duplicates-paths`
- **Ordering:** `--sort <name|natural|size|created|modified|extension|path|none>`, `--reverse`, `--shuffle`, `--seed`, `--order-file`, `--group-by <extension|directory|none>`
- **Output:** `--output`, `--output-dir`, `--output-name-template`, `--overwrite`, `--append`, `--no-clobber`, `--backup`, `--backup-suffix`, `--create-dirs`, `--stdout`, `--split-size`, `--split-lines`, `--split-files`, `--split-name-template`, `--atomic-write`, `--preserve-timestamps`, `--output-permissions`
- **Mode:** `--mode <text|binary|lines|bytes|json|jsonl|csv|tsv|xml|html|srt|vtt|m3u|auto>`, `--chunk-size`, `--buffer-size`
- **Text:** `--encoding`, `--input-encoding`, `--output-encoding`, `--detect-encoding`, `--encoding-errors`, `--strip-bom`, `--add-bom`, `--newline`, `--ensure-trailing-newline`, `--trim-lines`, `--trim-leading`, `--trim-trailing`, `--collapse-blank-lines`, `--max-blank-lines`, `--remove-empty-lines`, `--remove-comments`, `--dedupe-lines`, `--dedupe-lines-global`, `--dedupe-ignore-case`, `--sort-lines`, `--sort-lines-reverse`, `--sort-lines-numeric`, `--unique-sorted`, `--line-numbers`, `--line-number-format`, `--line-number-restart-per-file`, `--head-lines`, `--tail-lines`, `--skip-first-lines`, `--skip-last-lines`, `--line-filter-regex`, `--line-exclude-regex`, `--replace-regex`, `--replace-with`, `--case`
- **Separator & Markers:** `--separator`, `--separator-file`, `--separator-repeat`, `--no-separator`, `--header-template`, `--footer-template`, `--file-header`, `--file-footer`, `--marker-style`, `--marker-prefix`, `--marker-suffix`, `--include-relative-path`, `--include-size`, `--include-timestamp`, `--include-hash`, `--global-header`, `--global-footer`, `--global-header-file`, `--global-footer-file`
- **CSV/TSV:** `--csv-header`, `--csv-dedupe-header`, `--csv-delimiter`, `--csv-quote`, `--csv-align-columns`, `--csv-add-source-column`, `--csv-source-column-name`, `--csv-skip-rows`, `--csv-sort-by`, `--csv-unique-by`
- **JSON:** `--json-strategy <array|object|concat|deep|lines>`, `--json-array-key`, `--json-key-conflict <first|last|error|suffix>`, `--json-indent`, `--json-compact`, `--json-sort-keys`, `--json-ensure-ascii`, `--json-dedupe-by`, `--json-add-source-key`
- **Subtitle/Playlist:** `--renumber`, `--shift-time`, `--offset-per-file`, `--sort-by-time`
- **Binary:** `--binary-align`, `--binary-pad-byte`, `--binary-gap`, `--binary-skip-header`, `--binary-skip-footer`
- **Integrity & Safety:** `--verify`, `--hash <md5|sha1|sha256|sha512|crc32>`, `--hash-output`, `--manifest`, `--manifest-format <json|csv|txt>`, `--max-output-size`, `--fail-on-empty`, `--fail-on-missing`, `--fail-on-encoding-error`, `--lock`, `--dry-run`, `--no-write`
- **Behavior & Reporting:** `--continue-on-error`, `--threads`, `--progress`, `--quiet`, `--verbose`, `--debug`, `--log-file`, `--log-level`, `--summary`, `--summary-format`, `--color`, `--version`, `--help`, `--help-all`, `--list-options`

### Examples
```powershell
titan merge a.txt b.txt --output=merged.txt --newline=lf --ensure-trailing-newline --verify --hash=sha256
titan merge --input-glob="logs/*.log" --sort=natural --dedupe-lines-global --output=all.log --overwrite
titan merge a.csv b.csv --mode=csv --csv-align-columns --csv-unique-by=id --csv-sort-by=id --output=merged.csv
titan merge a.json b.json --mode=json --json-strategy=deep --json-sort-keys --output=config.json
titan merge p1.bin p2.bin --mode=binary --binary-align=16 --binary-pad-byte=FF --verify --output=full.bin
```
