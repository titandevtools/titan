## 14. `titan core-utils` — Native C++20 POSIX Utilities (All 19 Subcommands)

### Detailed Subcommand Reference & Options
1. **`titan core-utils count` (or `wc`):**
   - Single-pass `core::SimdScanner::count_all` (AVX2 256-bit SIMD + 64-bit SWAR): `-l` (lines), `-w` (words), `-c` (bytes), `-m` (max line length), `-j` (JSON).
2. **`titan core-utils sort`:**
   - `-n` (numeric), `-r` (reverse), `-u` (unique), `-f` (ignore-case), `-k <field>` (1-based key), `-t <delim>` (delimiter).
3. **`titan core-utils unique` (or `uniq`):**
   - `-c` (prefix occurrence count), `-i` (ignore case), `-d` (only duplicates), `-u` (only unique lines).
4. **`titan core-utils md5sum <files...>` & `titan core-utils sha256sum <files...>`:**
   - Pure C++20 cryptographic hashing (`-j` for JSON array of `{file, hash}`).
5. **`titan core-utils cut`:**
   - `-d <delim>` (delimiter, default TAB), `-f <fields>` (e.g. `1,3` or `2-4`), `-c <ranges>` (character positions `1-10`).
6. **`titan core-utils paste`:**
   - `-d <delims>` (custom delimiter characters), `-s` (paste one file at a time serially).
7. **`titan core-utils join`:**
   - `-t <char>` (field separator), `-1 <field>` (join field for file 1), `-2 <field>` (join field for file 2).
8. **`titan core-utils split`:**
   - `-l <lines>` (lines per chunk, default 1000), `-b <bytes>` (bytes per chunk, supports `k`, `m`), `-j` (JSON list of created chunk files).
9. **`titan core-utils head` & `titan core-utils tail`:**
   - `-n <lines>` (default 10), `-c <bytes>`.
10. **`titan core-utils base64`:**
    - `-d` / `--decode` (decode Base64), `-u` / `--url-safe` (URL-safe alphabet `-` and `_`).
11. **`titan core-utils rev`:**
    - Reverses characters on each line.
12. **`titan core-utils tr`:**
    - `-d` (delete `SET1`), `-s` (squeeze repeats), `-c` / `-C` (complement `SET1`). Supports `a-z`, `A-Z`, `0-9`, `[:lower:]`, `[:upper:]`, `[:digit:]`, `[:space:]`.
13. **`titan core-utils grep`:**
    - `-i` (ignore-case), `-v` (invert), `-n` (line numbers), `-c` (count), `-E` (linear-time Thompson NFA regex via `core::Regex`).
14. **`titan core-utils touch` / `cp` / `mv` / `rm`:**
    - File management with glob expansion (`*`, `?`), `-r`/`-R` (recursive), `-f` (force with safe non-existent path tolerance on `rm -rf`), self-move and case-rename safety in `mv`, `-n` (no-clobber), `-v` (verbose), `-j` (JSON summary).
