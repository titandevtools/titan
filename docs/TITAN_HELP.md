# TITAN (v2.0.2) — Complete Command-Line & AI-Agent Instructional Guide

- **Creator & Chief Architect:** Nourddine Bakour (Tetouan, Morocco)
- **Platform:** Windows x64 Native C++20 (`AVX2` 256-Bit SIMD + 64-Bit `SWAR` + Win32 `MemoryMappedFile`)
- **Distribution:** Native Windows x64 (`bin/titan.exe`)
- **Global CLI Command:** `titan` (add `bin/` to Windows `PATH`)
- **Latest Update Timestamp:** `2026-11-24 00:25:00 UTC`
- **Copyright:** Copyright (C) 2026 Nourddine Bakour. All Rights Reserved. Proprietary & Confidential.

---

## Table of Contents

0. [AI-Agent Decision Matrix (Mandatory Tool Selection Rules)](#0-ai-agent-decision-matrix-mandatory-tool-selection-rules)
1. [Global Usage, Architecture & Deterministic Exit Codes](#1-global-usage-architecture--deterministic-exit-codes)
2. [`titan search` — High-Performance Pattern, Regex & Fuzzy Search](#2-titan-search--high-performance-pattern-regex--fuzzy-search)
3. [`titan replace` — Atomic Replacement, Line-Scoping & Two-Way Smart-Swap](#3-titan-replace--atomic-replacement-line-scoping--two-way-smart-swap)
   - [3.1 Deep-Dive: `-swap` vs. `-smart-swap` (Single-Pass Two-Way Exchange)](#31-deep-dive--swap-vs--smart-swap-single-pass-two-way-exchange)
4. [`titan outline` — Structural Code AST Symbol & Line-Bound Extractor](#4-titan-outline--structural-code-ast-symbol--line-bound-extractor)
5. [`titan slice` — Zero-Copy Surgical Line-Range Reader](#5-titan-slice--zero-copy-surgical-line-range-reader)
6. [`titan tree` — Token-Efficient Workspace Directory Mapper](#6-titan-tree--token-efficient-workspace-directory-mapper)
7. [`titan mcp` — Native Model Context Protocol (JSON-RPC 2.0) Server](#7-titan-mcp--native-model-context-protocol-json-rpc-20-server)
8. [`titan verb` — Offset-Tolerant Atomic Patching & Instant Rollback](#8-titan-verb--offset-tolerant-atomic-patching--instant-rollback)
9. [`titan compare` — Myers O(ND) Unified Diff & Binary Comparison](#9-titan-compare--myers-ond-unified-diff--binary-comparison)
10. [`titan find` — Ultra-Fast Recursive Filesystem Discovery](#10-titan-find-files--ultra-fast-recursive-filesystem-discovery)
11. [`titan transform` — Stream Text Transformation & Line Filtering (`sed`)](#11-titan-transform--stream-text-transformation--line-filtering-sed)
12. [`titan process` — Structured Record, AWK & RFC 4180 CSV Engine (`gawk`)](#12-titan-process--structured-record-awk--rfc-4180-csv-engine-gawk)
13. [`titan stats` — Statistical Aggregation, Percentiles & GroupBy (`datamash`)](#13-titan-stats--statistical-aggregation-percentiles--groupby-datamash)
14. [`titan core-utils` — Native C++20 POSIX Utilities (All 19 Subcommands)](#14-titan-core-utils--native-c20-posix-utilities-all-19-subcommands)
15. [`titan tr` — High-Speed L1-Table Character Translation, Squeeze & Delete](#15-titan-tr--high-speed-l1-table-character-translation-squeeze--delete)
16. [`titan hex | rgb | hsl | hsla | cmyk | named | multi` — CSS Color Engine](#16-titan-hex--rgb--hsl--hsla--cmyk--named--multi--css-color-engine)
17. [`titan image` — Universal Image Metadata Extractor & Multi-Format Converter (27+ Formats)](#17-titan-image--universal-image-metadata-extractor--multi-format-converter-27-formats)
18. [`titan video` — Video Container, Codec, Resolution & Stream Metadata Extractor](#18-titan-video--video-container-codec-resolution--stream-metadata-extractor)
19. [`titan mp3 | titan audio` — Audio & MP3 Metadata, ID3v1/ID3v2, VBR & Stream Analyzer](#19-titan-mp3--titan-audio--audio--mp3-metadata-id3v1id3v2-vbr--stream-analyzer)
20. [`titan format` — Multi-Language Code Formatter, Minifier & Syntax Validator (`JS`, `JSON`, `CSS`, `HTML`, `SQL`, `C++`)](#20-titan-format--multi-language-code-formatter-minifier--syntax-validator-js-json-css-html-sql-c)
21. [`titan agent | context | symbol | deps | audit | edit` — AI-Powered Agent Intelligence Suite](#21-titan-agent--context--symbol--deps--audit--edit--ai-powered-agent-intelligence-suite)
22. [`titan convert | analyze | validate | fix` — Structured Data, Qt Designer & Sublime Text Engine](#22-titan-convert--analyze--validate--fix--structured-data-qt-designer--sublime-text-engine)
23. [`titan name-files` — Windows Filename Inspection & Safe Batch-Renaming Engine](#23-titan-name-files--windows-filename-inspection--safe-batch-renaming-engine)
24. [`titan read` — Agent-Oriented Universal File Reader & Linear-Time Regex Engine](#24-titan-read--agent-oriented-universal-file-reader--linear-time-regex-engine)
25. [`titan archive` — Native Universal Archive Suite (`ZIP/ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`, `7Z`, `RAR4`, `RAR5`)](#25-titan-archive--native-universal-archive-suite-zipzip64-tar-gzip-targz-zstd-tarzst-7z-rar4-rar5)
26. [`titan ast-search | ast-replace` — Structural AST Pattern Search & Rewrite Engine](#26-titan-ast-search--ast-replace--structural-ast-pattern-search--rewrite-engine)
27. [`titan query` — Structured Path/Filter Query & Mutation Engine](#27-titan-query--structured-pathfilter-query--mutation-engine)
28. [`titan table` — Streaming SQL-Lite Analytics (`CSV`, `TSV`, `JSONL`)](#28-titan-table--streaming-sql-lite-analytics-csv-tsv-jsonl)
29. [`titan lsp` — JSON-RPC 2.0 LSP Bridge & Zero-Index Fallback](#29-titan-lsp--json-rpc-20-lsp-bridge--zero-index-fallback)
30. [`titan tx` — Multi-File Atomic Transaction Engine & Rollback Journal](#30-titan-tx--multi-file-atomic-transaction-engine--rollback-journal)
31. [`titan inject` / `titan injection` — Surgical Code & Text Injection](#31-titan-inject--titan-injection--surgical-code--text-injection)
32. [`titan run` / `titan ti` — Native TITAN (`.ti`) Text-Processing Scripting Language](#32-titan-run--titan-ti--native-titan-ti-text-processing-scripting-language)
33. [`titan dir` — Smart Directory Inspection, Classification & Diagnostics](#33-titan-dir--smart-directory-inspection-classification--diagnostics)
34. [`titan create` — Batch File & Directory Creation Engine](#34-titan-create--batch-file--directory-creation-engine)
35. [`titan copy` — Verified, Filter-Aware File & Directory Copy Engine](#35-titan-copy--verified-filter-aware-file--directory-copy-engine)
36. [`titan move` — Crash-Safe File & Directory Move Engine](#36-titan-move--crash-safe-file--directory-move-engine)
37. [`titan rename` — Collision-Safe Composable Batch Renaming Engine](#37-titan-rename--collision-safe-composable-batch-renaming-engine)
38. [`titan info` — Fast Runtime Health, Binary & Guide Inspector](#38-titan-info--fast-runtime-health-binary--guide-inspector)
39. [`titan system` — Native Windows Environment, Hardware, Disk, Network & Process Inspector](#39-titan-system--native-windows-environment-hardware-disk-network--process-inspector)
40. [`titan delete` — Safe Windows File & Folder Deletion Engine](#40-titan-delete--safe-windows-file--folder-deletion-engine)
41. [`titan dev` — Multi-Language Structural Code Analyzer & Symbol Extractor (20 Languages)](#41-titan-dev--multi-language-structural-code-analyzer--symbol-extractor-20-languages)
42. [`titan bench` — High-Precision Win32 Benchmark & Telemetry Runner (`--` ONLY)](#42-titan-bench--high-precision-win32-benchmark--telemetry-runner---only)
43. [`titan git` — Zero-Dependency Native `.git` Repository Inspector (`--` ONLY)](#43-titan-git--zero-dependency-native-git-repository-inspector---only)
44. [`titan http` — Advanced Native Windows WinHTTP Client (`--` ONLY)](#44-titan-http--advanced-native-windows-winhttp-client---only)
45. [`titan ftp` — Native RFC 959/2428/3659 FTP & WinINet FTPS Client (`--` ONLY)](#45-titan-ftp--native-rfc-95924283659-ftp--wininet-ftps-client---only)
46. [`titan doc` — Native Office, EPUB, RTF & PDF Document Extractor (`--` ONLY)](#46-titan-doc--native-office-epub-rtf--pdf-document-extractor---only)
47. [`titan reg` — Native Win32 Windows Registry Inspector, Diff & Exporter (`--` ONLY)](#47-titan-reg--native-win32-windows-registry-inspector-diff--exporter---only)
48. [`titan normalize` — Batch Encoding, EOL, Indentation & Whitespace Normalizer (`--` ONLY)](#48-titan-normalize--batch-encoding-eol-indentation--whitespace-normalizer---only)
49. [`titan dissect` — Unified 20-Language Code & Text Dissection Super-Engine](#49-titan-dissect--unified-20-language-code--text-dissection-super-engine)
50. [`titan merge` — Streaming Multi-Format File Merger (`--` ONLY)](#50-titan-merge--streaming-multi-format-file-merger---only)

---

## 0. AI-Agent Decision Matrix (Mandatory Tool Selection Rules)

Every AI model operating on this system **MUST** use `titan` instead of legacy PowerShell or POSIX commands. Below is the mandatory mapping from task intent to the optimal TITAN command:

| AI Agent Task / Intent | ❌ NEVER USE (Slow / Token-Heavy) | ✅ ALWAYS USE (TITAN Native C++20) | Speed / Token Advantage |
| :--- | :--- | :--- | :--- |
| **Analyze code symbols, signatures, complexity & extract functions (20 langs)** | Reading whole files or writing ad-hoc regex parsers | `titan dev -r [--complexity --signature] <dir>` / `titan dev -x "<Sym>" <file>` | Instant 20-language symbol table, cyclomatic complexity (`CC`), `--stats`, `--imports`, `--todos` & body extraction |
| **Map project folder structure** | `Get-ChildItem -Recurse`, `tree` | `titan tree <dir> -L 3 [--json]` | **1.73x faster**, **94% fewer tokens** |
| **Inspect directory intelligence & duplicates** | Manual `Get-ChildItem` loops + hashing | `titan dir <dir> --complete [--duplicates] [-j]` | Instant category breakdown, encoding/EOL scan & SHA-256 duplicate detection |
| **Find files by glob/ext/size** | `Get-ChildItem -Filter`, `find` | `titan find <dir> -g "*.cpp" [--full-paths]` | Zero-stat fast path, full glob/size/mtime/`--respect-gitignore` support |
| **Understand a source file's structure** | Reading entire 1,000-line file into context | `titan dev <file> --complexity --signature` or `titan outline <file> --no-includes` | Extracts exact `[start:end]` line bounds, params & complexity in **< 2ms** |
| **Read a specific function or block** | `Get-Content <file> \| Select-Object` | `titan dev -x "<Class.method>" <file>` or `titan slice <file> <start:end>` | **3.86x faster**, **84.1% fewer tokens**, zero-copy surgical extraction |
| **Search text/regex across files** | `Select-String`, `findstr`, `grep` | `titan search -n -r [-E] "<pat>" <dir>` | **3.02x faster** (Boyer-Moore-Horspool + linear-time Thompson NFA `-E` + UTF-16) |
| **Search with typo tolerance** | Manual regex combinations | `titan search -n --fuzzy 2 "<pat>" <dir>` | Native Levenshtein edit-distance scanner |
| **Replace text inside ONE function** | Global `-replace` (risks corrupting file) | `titan replace "<old>" "<new>" <file> --lines S:E -i` | Surgical line-range isolation + atomic write |
| **Swap two identifiers (`A <-> B`)** | 3-step `__TMP__` placeholder script | `titan replace -smart-swap "A" "B" <file> -i` | **16.92x faster**, single-pass, preserves case |
| **Apply unified diff patch safely** | `git apply` / `patch` (fails on line drift) | `titan verb apply --backup --input <patch>` | Auto-searches $\pm 250$ lines if offset drifted |
| **Undo/restore a modified file** | Manual copy/paste | `titan verb rollback <file>` | Instant atomic restore from `.orig.~N~` / `.orig` |
| **Count lines/words/bytes** | `Get-Content \| Measure-Object -Line` | `titan core-utils count -l [-w] [-c] <file>` | **37.85x faster** (AVX2/SWAR single-pass `count_all`) |
| **Compute stats / percentiles on data** | Custom Python/PowerShell script | `titan stats <mean\|p95\|iqr\|groupby> <col> <file>` | Zero-allocation `std::from_chars` streaming |
| **Extract CSV / tabular columns** | `Import-Csv` (slow object boxing) | `titan process --csv '{print $1, $3}' <file>` | Native RFC 4180 state machine |
| **Extract image details / EXIF / convert** | External Python/ImageMagick scripts | `titan image info <img...> [--hash] [-j]` / `titan image convert` | Native binary parser + 27+ format batch converter |
| **Extract video container/codec metadata** | Slow external media probes | `titan video <file_or_dir> [--hash] [-j]` | Zero-copy MP4/MOV/MKV/WEBM/AVI/FLV box parser |
| **Extract MP3 / audio ID3 & stream tags** | Slow PowerShell/Python tag readers | `titan mp3 <file_or_dir> [--hash] [-j]` | Native ID3v1/v2.4, Xing/VBRI VBR, FLAC & WAV parser |
| **Format, minify, or validate code** | Heavy Node/Prettier/jq spawns | `titan format <files...> -i` / `--minify` / `--check` | Zero-dependency JS/TS, JSON, CSS, HTML, SQL, C++ engine |
| **AI codebase context / symbol / audit / lock edit** | Manual `Get-Content` + regex passes | `titan context / symbol / deps / audit / edit` | Token-budgeted AST bundles, mini-LSP, SHA-256 edit lock |
| **Agent-oriented file reading & linear regex** | `Get-Content`, `Select-String`, `cat` | `titan read [OPTIONS] <files...>` | Multi-encoding (UTF-8/16/ANSI), linear-time regex, token safety caps |
| **Inspect, create, extract, or verify archives** | `Expand-Archive`, `Compress-Archive`, `tar` | `titan archive <list\|extract\|create\|test\|detect> <archive>` | Zero-dependency ZIP/ZIP64, TAR, GZIP/TAR.GZ, ZSTD/TAR.ZST (+7Z extract/verify, RAR inspect), Zip-Slip guard |
| **Structural code search & rewrite** | Fragile multi-line regex | `titan ast-search / ast-replace` (`search --ast`) | CST/AST token matching ignoring whitespace & comments |
| **Structured query & 64-bit JSON/YAML/TOML edit** | `jq`, `yq`, fragile string replace | `titan query EXPR <file>` / `--set PATH=VAL` | Exact `int64_t` preservation, atomic `-i -b` |
| **SQL analytics on CSV / TSV / JSONL** | Python pandas / Excel | `titan table "SELECT ..." <files...>` | Streaming `WHERE`, `JOIN`, `GROUP BY`, percentiles |
| **Semantic LSP / fallback symbol queries** | Manual grep / IDE only | `titan lsp <op> <file> <line> <col>` | JSON-RPC 2.0 stdio LSP + zero-index fallback |
| **Atomic multi-file edits & rollback** | Partial manual edits | `titan tx <begin\|add\|commit\|rollback\|apply>` | 3-phase commit, SHA-256 locks, `--validate` hook |
| **Surgical code/text insertion at line/col/symbol** | Manual line counting or fragile `sed` | `titan inject [--line N\|--inside-symbol S] --text "..." <file>` | `--`-only flags, single-block `--format-block`, UTF-8 cols, `.orig` backup |
| **Batch create, copy, move, rename, or delete files** | `New-Item`, `Copy-Item`, `Move-Item`, `Remove-Item` | `titan create / copy / move / rename / delete` | SHA-256 verified, `.gitignore`-aware, undo journals, protected-path guards |
| **Execute `.ti` pipelines or inspect system/runtime** | PowerShell loops / `systeminfo` / `netstat` | `titan run <script.ti>` / `titan info` / `titan system <flag>` | Native `.ti` language engine + zero-WMI Win32 hardware/network/process inspector |

---

## 1. Global Usage, Architecture & Deterministic Exit Codes

### Synopsis
```powershell
titan <command> [arguments...]
titan --help | -h
titan --version | -v
```

### Complete Command Registry (67 Registered Dispatch Targets)
| Command | Engine | Description |
| :--- | :--- | :--- |
| `dev` | `DevEngine` | Multi-language structural code analyzer, symbol lister, complexity calculator & symbol source extractor across 20 languages |
| `bench` | `BenchEngine` | High-precision Win32 command execution & comparison benchmarking runner with CPU/RSS telemetry (`--` options only) |
| `git` | `GitEngine` | Zero-dependency native `.git` status, branches, tags, log, object decoding, index & remotes inspector (`--` options only) |
| `http` | `HttpEngine` | Advanced Windows WinHTTP client with auth, cookies, multipart `--form`, retries, HTTP/2 & proxy (`--` options only) |
| `ftp` | `FtpEngine` | Native RFC 959/2428/3659 FTP & WinINet FTPS client, recursive transfer, resume & mirror sync (`--` options only) |
| `doc` | `DocEngine` | Native zero-dependency document extractor across DOCX, XLSX, PPTX, ODT/ODS/ODP, EPUB, RTF & PDF (`--` options only) |
| `reg` | `RegEngine` | Read-only native Win32 Registry query, keys, tree, search, diff & `.reg` v5.00 exporter (`--` options only) |
| `normalize` | `NormalizeEngine` | Batch EOL, BOM, tab/space indent, blank-line, control-byte normalizer & unified diff preview (`--` options only) |
| `search` | `SearchEngine` | High-performance literal (Boyer-Moore-Horspool), linear-time Thompson NFA regex (`-E`), and Levenshtein fuzzy search |
| `replace` | `ReplaceEngine` | In-place literal/regex replacement (`-E`), capture groups, `--lines` surgical scoping, `-swap`, and `-smart-swap` |
| `outline` | `InspectEngine` | Instant structural code outline (classes, structs, namespaces, functions, `[start:end]` bounds) |
| `slice` | `InspectEngine` | Zero-copy surgical line-range reader with SHA-256 integrity verification |
| `tree` | `InspectEngine` | Fast token-efficient workspace directory tree for AI Agents |
| `mcp` | `McpEngine` | Native Model Context Protocol (MCP) JSON-RPC 2.0 server & AI Agent manifest (42 tools including `titan_ftp`, `titan_bench`, `titan_git`, `titan_http`, `titan_doc`, `titan_reg`, `titan_normalize`) |
| `verb` | `VerbEngine` | Atomic patch application (`apply`) and multi-version collision-proof restoration (`rollback`) |
| `compare` | `CompareEngine` | Myers $O(ND)$ unified diff, similarity scoring, side-by-side diff, and byte comparison |
| `find` | `FindEngine` | Ultra-fast native filesystem discovery, globbing, metadata filtering, `--respect-gitignore`, and sorting |
| `dir` | `DirEngine` | Smart directory inspection, classification, duplicate finder, encoding/line-ending scanner & disk analytics |
| `create` | `CreateEngine` | Batch file & directory creation engine with templates, numbering, encodings, atomic rollback & conflict policies |
| `copy` | `CopyEngine` | Verified, filter-aware file & directory copy engine with SHA-256 verification & atomic staging |
| `move` | `MoveEngine` | Crash-safe, cross-volume-aware file & directory move engine with SHA-256 verification & empty-dir pruning |
| `rename` | `RenameEngine` | Collision-safe composable batch file & directory renaming engine with case conversions, regex & undo journal |
| `delete` | `DeleteEngine` | Safe Windows file & folder deletion engine with protected-path guard, Recycle Bin, multi-pass secure wipe & filters |
| `info` | `InfoEngine` | Fast runtime health, binary size, PATH status, registered command count (`67`), and AI guide inspector |
| `system` | `SystemEngine` | Native Win32 environment, PATH, OS, CPU/GPU/RAM/BIOS/disk/network/ports/process/service inspector (39 flags) |
| `run` | `TiScriptEngine` | Execute native TITAN (`.ti`) text-processing pipelines and scripts (`--guide` built-in specification) |
| `ti` | `TiScriptEngine` | Alias for `titan run` — execute native TITAN (`.ti`) text-processing scripts |
| `transform` | `TransformEngine` | Stream text transformation, linear-time regex pattern substitution, and line filtering (`sed`) |
| `process` | `ProcessEngine` | Structured record, AWK field extraction, and RFC 4180 CSV processing (`gawk`) |
| `stats` | `StatsEngine` | Zero-allocation streaming statistical summaries, percentiles (`p50`–`p99`), and `groupby` |
| `core-utils` | `CoreUtilsEngine` | 19 native POSIX utilities (`count`, `sort`, `unique`, `md5sum`, `sha256sum`, `cut`, `paste`, `join`, `split`, `head`, `tail`, `base64`, `rev`, `tr`, `grep`, `touch`, `cp`, `mv`, `rm`) |
| `tr` | `CoreUtilsEngine` | Direct top-level alias for `core-utils tr` (translate, squeeze `-s`, delete `-d`, complement `-c`) |
| `image` | `ImageEngine` | Universal image metadata extractor (`info`) & multi-format single/batch converter (`convert`) across 27+ formats |
| `video` | `VideoEngine` | Native video metadata inspector & Media Foundation / GDI+ frame, contact-sheet, scene-cut & WAV audio extractor |
| `mp3` | `AudioEngine` | Native MP3 & audio metadata, lyrics, cover artwork (`--covers`) & Media Foundation PCM WAV (`--wav`) extractor (`ID3`, `FLAC`, `WAV`, `OGG`, `M4A`) |
| `audio` | `AudioEngine` | Alias for `titan mp3` — extract complete audio metadata, lyrics, cover artwork & PCM WAV |
| `format` | `FormatEngine` | Multi-language code formatter, minifier (`--minify`), and syntax validator (`--check`) for `JSON`, `JS`/`TS`, `CSS`, `HTML`/`XML`/`SVG`, `SQL`, `C`/`C++` |
| `agent` | `AgentEngine` | AI-Powered Agent Intelligence Suite dispatcher (`context`, `symbol`, `deps`, `audit`, `edit`) |
| `context` | `AgentEngine` | Smart AI context packager extracting AST definitions & call sites within `--max-tokens` |
| `symbol` | `AgentEngine` | Cross-project symbol definition & call-site reference resolver (Zero-Index Mini-LSP) |
| `deps` | `AgentEngine` | Multi-language `#include`, JS/TS `import`, C# `using`, and Unity `guid:` dependency graph analyzer |
| `audit` | `AgentEngine` | Codebase security secret scanner, `TODO`/`FIXME` debt finder, complexity hotspot & token auditor |
| `edit` | `AgentEngine` | Surgical line-range block replacement with SHA-256 optimistic concurrency lock & atomic backup |
| `convert` | `StructuredEngine` | Bidirectional converter across JSON, CSV, TSV, XML, YAML, TOML, INI, HTML, Qt `.ui` & 15 Sublime Text formats |
| `analyze` | `StructuredEngine` | Read-only structural analysis of structured files, Qt `.ui`, and Sublime Text formats/packages |
| `validate` | `StructuredEngine` | Strict schema & syntax validator (`exit 0` valid, `1` invalid) for structured, Qt `.ui`, and Sublime Text files |
| `inspect-file` | `StructuredEngine` | Alias of `analyze` for structured data, Qt Designer `.ui`, and Sublime Text files |
| `fix` | `StructuredEngine` | Conservative format-aware repair with `--dry-run`, backup, report, and post-repair validation |
| `name-files` | `NameFilesEngine` | Windows filename case inspection (read-only queries) and collision-safe atomic batch renaming |
| `read` | `ReadEngine` | Agent-oriented universal file reader (`UTF-8`/`UTF-16`/`ANSI`), linear-time regex, comment filter & JSON output |
| `archive` | `ArchiveEngine` | Native multi-format archive suite (`ZIP/ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`, `7Z`, `RAR4`, `RAR5`) with Zip-Slip & zip-bomb guards |
| `hex` | `ColorEngine` | Extract, filter, lighten/darken, convert, and swap CSS `#RGB`/`#RGBA`/`#RRGGBB`/`#RRGGBBAA` colors |
| `rgb` | `ColorEngine` | Extract, convert, and transform CSS `rgb(...)` and `rgba(...)` colors |
| `hsl` | `ColorEngine` | Extract, convert, and transform non-alpha CSS `hsl(...)` colors |
| `hsla` | `ColorEngine` | Extract, convert, and transform alpha-enabled CSS `hsl(...)` & `hsla(...)` colors |
| `cmyk` | `ColorEngine` | Extract and validate `cmyk(...)` color tokens |
| `named` | `ColorEngine` | Extract standard CSS named color identifiers (`red`, `cornflowerblue`, etc.) |
| `multi` | `ColorEngine` | Extract all CSS color formats simultaneously (`hex`, `rgb`, `hsl`, `cmyk`, `named`) |
| `color-tips` | `ColorEngine` | Display advanced color processing options and usage tips |
| `ast-search` | `AstEngine` | Structural AST pattern search across C/C++, Python, JS/TS, Rust, Go, C#, JSON |
| `ast-replace` | `AstEngine` | Structural AST rewrite with metavariable bindings and atomic backups |
| `query` | `QueryEngine` | Structured query & surgical mutation across JSON, JSONC, YAML, TOML, XML, INI |
| `table` | `TableEngine` | Streaming SQL-lite analytics across CSV, TSV, and JSONL tables |
| `lsp` | `LspEngine` | JSON-RPC 2.0 stdio LSP bridge with automatic TITAN zero-index fallback |
| `tx` | `TxEngine` | Multi-file atomic transaction engine with 3-phase commit & rollback journal |
| `inject` | `InjectEngine` | Surgical line, column, pattern & symbol code/text injection (`--` options only) |
| `injection` | `InjectEngine` | Alias for `titan inject` — surgical line, column, pattern & symbol code injection |

### Deterministic Exit Codes
- `0` — **Success** (Operation succeeded / match found in `search` / files identical in `compare`)
- `1` — **Logical False / Difference** (No match found in `search` / differences detected in `compare`)
- `2` — **Error** (Invalid CLI syntax, malformed regex, missing file, or I/O failure)

---------------------------------------------------------------------------------------

## 2. `titan search` — High-Performance Pattern, Regex & Fuzzy Search

### Architecture & Algorithmic Behavior
- **Literal-by-Default Safety:** Treats patterns strictly as literal text by default (never silently auto-upgrading punctuation like `.`, `()`, `[]`, or `$` into regex). When literal and case-sensitive, uses **Boyer-Moore-Horspool** bad-character shift tables over memory-mapped files (`MemoryMappedFile`) at hardware RAM bandwidth.
- **Linear-Time Thompson NFA Regex (`-E` / `--regex`):** When `-E` or `--regex` is passed (and `-F` / `--fixed-strings` is not set), compiles the pattern using TITAN's native **Thompson NFA / Pike VM** engine (`core::Regex`), guaranteeing strict $O(N)$ linear-time execution with zero catastrophic ReDoS backtracking.
- **UTF-16LE/BE & Genuine `--multiline`:** Automatically decodes UTF-16LE and UTF-16BE files (via BOM or UTF-16 byte heuristics) into UTF-8 prior to scanning, and supports genuine cross-line pattern boundaries when `--multiline` is enabled.
- Automatically skips binary files (files containing non-UTF-16 NUL `\0` bytes in the first 4 KB) unless `-a` / `--binary` / `--text` is specified.
- Supports **Levenshtein Fuzzy Matching** (`--fuzzy <N>`) to find identifiers even when the query contains typos, insertions, or deletions.

### Verbatim Help Manual
DIR = docs/tools/SEARCH--HELP.md

---------------------------------------------------------------------------------------

## 3. `titan replace` — Atomic Replacement, Line-Scoping & Two-Way Smart-Swap

### Architecture & Safety Guarantees
- **Literal-by-Default & Linear-Time Regex (`-E` / `--regex`):** Treats `PATTERN` as literal text unless `-E` / `--regex` is explicitly passed (overridden back to literal if `-F` / `--fixed-strings` is also set). Regex mode runs on TITAN's shared **Thompson NFA / Pike VM** engine (`core::Regex`) with zero catastrophic backtracking, genuine `--multiline` support, and capture-group expansion (`$&`, `$0`, `$1`–`$9`, `\1`–`\9`, `$$`).
- **Atomic Staging Write (`BackupManager::atomic_write`):** Writes modified content to a temporary `.titan_tmp_*` staging file in the target directory and atomically swaps it into place via Win32 `MoveFileExW(..., MOVEFILE_REPLACE_EXISTING)`. A crash or power loss never leaves a half-written file.
- **Collision-Proof Multi-Version Backups (`--backup`):** Automatically generates `.orig`, `.orig.~1~`, `.orig.~2~`, ..., `.orig.~N~` so existing backups are never overwritten.
- **Surgical Line-Range Scoping (`--lines <START:END>`):** Computes exact byte offsets for lines `START..END` (1-based, inclusive), leaving lines before `START` and after `END` 100% untouched.

### Verbatim Help Manual
DIR = docs/tools/REPLACE--HELP.md

---------------------------------------------------------------------------------------

### 3.1 Deep-Dive: `-swap` vs. `-smart-swap` (Single-Pass Two-Way Exchange)

Standard tools (`sed`, `grep`, PowerShell `-replace`) cannot swap two words `A` and `B` in a single pass without corrupting the file (because replacing `A -> B` and then `B -> A` turns everything into `A`). **TITAN** executes two-way exchanges in a **single linear $O(N)$ pass**.

#### Comparison Table: `-swap` vs. `-smart-swap`
| Feature / Behavior | `titan replace -swap A B` | `titan replace -smart-swap A B` |
| :--- | :--- | :--- |
| **Direction** | Two-way simultaneous (`A <-> B`) | Two-way simultaneous (`A <-> B`) |
| **Case Sensitivity** | Exact case by default (or add `--ignore`) | **Automatically Case-Insensitive** |
| **Word Boundaries** | Substring match by default (or add `-w`) | **Automatically Whole-Word (`-w`)** |
| **Case Preservation** | Uses literal `A` and `B` (or add `--preserve`) | **Automatically Preserves Original Case** |
| **Prefix Overlap (`color` vs `colorful`)** | Longest-match wins at same position | Longest-match wins at same position |
| **Multiple Pairs in One Command** | Supported (`-swap A B -swap C D`) | Supported (`-smart-swap A B -smart-swap C D`) |
| **Line-Range Scoping (`--lines S:E`)** | Supported | Supported |

#### How `-smart-swap` Automatic Case Preservation Works
When `-smart-swap "client" "server"` matches a token, `matchCaseOf()` inspects the casing of the matched token (including UTF-8 multi-byte uppercase/lowercase sequences) and applies it to the replacement:
- `client` (all lower) $\longleftrightarrow$ `server` (all lower)
- `CLIENT` (ALL UPPER) $\longleftrightarrow$ `SERVER` (ALL UPPER)
- `Client` (Title Case) $\longleftrightarrow$ `Server` (Title Case)

Because `-smart-swap` enforces **whole-word boundaries** (`!isalnum` on both sides), compound identifiers like `clientConfig` or `serverless` are never corrupted.

#### Practical Examples for `titan replace`
```powershell
# 1. Surgical replacement restricted to lines 331..421 with dry-run unified diff preview
titan replace "old_var" "new_var" --lines 331:421 --dry-run src/engine/replace.cpp

# 2. In-place replacement with collision-proof backup (.orig, .orig.~1~)
titan replace -i --backup "v0.1.0" "v1.0.0" include/titan/core/platform.hpp

# 3. Exact literal two-way swap (swaps "left" <-> "right" everywhere in layout.css)
titan replace -swap "left" "right" -i layout.css

# 4. Intelligent case-preserving whole-word swap across all *.cpp files with JSON telemetry
titan replace -smart-swap "client" "server" -r -g "*.cpp" -i --backup --json src/
```

---

## 4. `titan outline` — Structural Code AST Symbol & Line-Bound Extractor

### Architecture & Purpose
Designed specifically for AI coding agents. Scans source files (`C`, `C++`, `Python`, `Rust`, `Go`, `TypeScript`, `JavaScript`, `Java`, `C#`) in microseconds using a quote/comment/escape-aware brace & indentation tracker to emit every `namespace`, `class`, `struct`, `enum`, and `function` with its **exact `[start_line:end_line]` boundary**.

### Verbatim Help Manual
DIR = docs/tools/OUTLINE--HELP.md

---------------------------------------------------------------------------------------

## 5. `titan slice` — Zero-Copy Surgical Line-Range Reader & Extractor

### Architecture & Purpose
Reads exact 1-based line ranges (`START:END`, `START:+COUNT`, `tail:N`, or comma-separated multi-ranges), symbol spans (`--symbol`), or pattern-anchored windows (`--around`) directly from a Win32 `MemoryMappedFile` view without loading the entire file into AI context, saving **84%+ of context tokens**. Supports `--sha256` / `--hash` (both file and slice SHA-256), `--max-tokens` pagination, `--dedent`, `--strip-blank`, `--max-line-len`, and safe atomic `--output` extraction with protected-path guards.

### Verbatim Help Manual
DIR = docs/tools/SLICE--HELP.md

---------------------------------------------------------------------------------------

## 6. `titan tree` — Token-Efficient Workspace Directory Mapper

### Architecture & Purpose
Maps a workspace directory tree while automatically skipping noisy build/dependency directories (`.git`, `build`, `node_modules`, `dist`, `__pycache__`, `target`) unless `--all` (`-a`) is specified. Reduces AI context consumption by **94%** compared to `Get-ChildItem -Recurse`.

### Verbatim Help Manual
DIR = docs/tools/TREE--HELP.md

---------------------------------------------------------------------------------------

## 7. `titan mcp` — Native Model Context Protocol (JSON-RPC 2.0) Server

### Architecture & Exposed MCP Tools (43 Tools)
Runs a zero-dependency **JSON-RPC 2.0 MCP Server** over `stdin`/`stdout` (`titan mcp --stdio`), transparently supporting both newline-delimited JSON (NDJSON, with automatic UTF-8 BOM stripping) and LSP/MCP `Content-Length: N\r\n\r\n` framed stdio messages. Handles `initialize`, JSON-RPC notifications (suppressing responses on frames without `id`), `ping`, `tools/list`, and `tools/call` in-process via O(1) modular dispatch tables with zero subprocess spawning overhead. Request arguments are isolated cleanly inside `params.arguments` via `RpcJsonParser`.

### Exposed MCP Tool Names & Parameters
| MCP Tool Name | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- |
| `titan_outline` | `path` | `kind` | Extract AST symbols and `[start_line, end_line]` bounds |
| `titan_slice` | `path` | `range`, `symbol`, `around`, `context`, `before`, `after`, `max_tokens`, `max_line_len`, `dedent`, `strip_blank`, `raw`, `hash`, `output`, `flags` | Read ranges, `tail:N`, or symbols with SHA-256 verification & token budget |
| `titan_tree` | `dir` | `depth` | Token-efficient workspace directory tree |
| `titan_search` | `pattern`, `path` | `smart_case`, `and_pattern`, `not_pattern`, `type`, `type_not`, `with_symbol`, `max_total`, `max_tokens`, `max_filesize`, `max_line_len`, `flags` | Boyer-Moore-Horspool, linear-time regex, fuzzy & symbol-tagged search |
| `titan_replace` | `pattern`, `replacement`, `path` | `lines`, `mode` (`replace`, `swap`, `smart-swap`, `dry-run`) | Atomic replacement or smart-swap |
| `titan_find_files` | — | `dir`, `dirs`, `glob`, `ext`, `type`, `size`, `older_than`, `empty`, `count`, `limit`, `sort`, `reverse`, `relative`, `full_paths`, `respect_gitignore`, `max_depth`, `flags` | Multi-root recursive file discovery with filtering, dedup & count mode |
| `titan_compare` | `file1`, `file2` | `brief`, `bytes`, `stat`, `side_by_side`, `ignore_case`, `ignore_whitespace`, `recursive`, `flags` | Myers O(ND) unified diff and binary comparison |
| `titan_stats` | `operation`, `path` | `column` | Statistical aggregations & percentiles |
| `titan_verb_rollback` | `path` | — | Atomic restoration from latest `.orig.~N~` / `.orig` backup |
| `titan_image` | `path` | `action` (`info`\|`convert`), `to`, `from` | Extract image metadata/EXIF or batch-convert across 27+ formats |
| `titan_video` | `path` | `strip_metadata`, `output`, `in_place`, `no_backup`, `keep_timestamps`, `out_dir`, `contact_sheet`, `extract_audio`, `format`, `grid`, `at`, `every`, `count`, `from`, `to`, `scene_threshold`, `max_width`, `max_height`, `quality`, `probe`, `rotate`, `flip`, `grayscale`, `timestamps`, `overwrite`, `dry_run`, `flags` | Extract video metadata, losslessly strip container metadata (MP4/MOV/MKV/WebM/AVI), frames, contact sheets, scene cuts & WAV audio |
| `titan_mp3` | `path` | `covers`, `wav`, `from`, `to`, `output`, `format`, `recursive`, `overwrite`, `dry_run`, `flags` | Extract audio metadata, lyrics, album artwork & timeline-trimmed PCM WAV (`MP3`, `FLAC`, `WAV`, `OGG`, `M4A`) |
| `titan_format` | `path` | `mode` (`beautify`, `format`, `minify`, `check`, `in-place`, `apply`) | Format, minify, or syntax-validate `JSON`, `JS`/`TS`, `CSS`, `HTML`, `SQL`, `C`/`C++` |
| `titan_context` | `query` | `path`, `max_tokens` | Smart AI context packager extracting AST blocks within token budget |
| `titan_symbol` | `symbol` | `path`, `mode` (`all`, `definitions`, `references`) | Zero-index cross-project symbol definition & reference resolver |
| `titan_deps` | `path` | `reverse` | C/C++ `#include`, JS/TS `import`, C# `using`, and Unity GUID dependency analyzer |
| `titan_audit` | `path` | — | Codebase secret scanner, `TODO`/`FIXME` debt, complexity hotspot & token auditor |
| `titan_edit` | `path`, `range`, `content` | `expect_hash` | Surgical line-range block edit with SHA-256 optimistic concurrency lock |
| `titan_read` | `path` | `lines`, `filter`, `pattern`, `flags` | Multi-encoding safe reader (`UTF-8`/`UTF-16`/`ANSI`) with linear-time regex & filters |
| `titan_archive` | `action` (`list`\|`extract`\|`create`\|`test`\|`detect`\|`caps`) | `archive`, `output`, `inputs`, `level` | Multi-format archive engine (`ZIP`/`ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`, `7Z`, `RAR`) with Zip-Slip & zip-bomb guards |
| `titan_name_files` | `path`, `action` | `flags` | Windows filename case inspection & collision-safe atomic batch renamer |
| `titan_ast_search` | `pattern` | `path`, `lang`, `flags` | Structural AST pattern search across C/C++, Python, JS/TS, Rust, Go, C#, JSON |
| `titan_ast_replace` | `pattern`, `replacement`, `path` | `lang`, `mode`, `flags` | Structural AST rewrite with metavariable bindings and atomic backups |
| `titan_query` | `path` | `expr`, `set`, `del`, `mode`, `format`, `raw_str` | Structured query & mutation across JSON, JSONC, YAML, TOML, XML, INI (`64-bit` ints) |
| `titan_table` | `sql`, `paths` | `format`, `delimiter` | Streaming SQL-lite analytics across CSV, TSV, and JSONL |
| `titan_lsp` | `operation`, `file` | `line`, `col`, `new_name`, `server`, `root` | JSON-RPC 2.0 stdio LSP bridge with TITAN zero-index fallback |
| `titan_tx` | `action` | `tx_dir`, `manifest`, `path`, `range`, `content`, `expect_hash`, `validate`, `flags` | Multi-file atomic transaction engine with 3-phase commit & rollback journal |
| `titan_inject` | `path` | `line`, `col`, `anchor`, `pattern`, `symbol`, `text`, `from_file`, `mode`, `flags` | Surgical line, column, pattern & symbol injector (`mode: "dry-run"` default, `--` options only) |
| `titan_run` | — | `script`, `path`, `mode`, `args`, `guide`, `step_limit` | Execute native `.ti` text-processing pipeline scripts (and built-in `--guide`) |
| `titan_dir` | — | `path`, `recursive`, `flags` | Directory listing, summaries, duplicate SHA-256 & line-ending diagnostics |
| `titan_copy` | `src`, `dest` | `mode`, `verify`, `backup`, `recursive`, `flags` | Verified SHA-256 copy engine (`mode: "dry-run"` default) |
| `titan_move` | `src`, `dest` | `mode`, `verify`, `backup`, `flags` | Crash-safe cross-volume move engine (`mode: "dry-run"` default) |
| `titan_rename` | `path` | `mode`, `flags` | Collision-safe batch rename engine (`mode: "dry-run"` default) |
| `titan_create` | `path` | `mode`, `content`, `flags` | Batch file & directory creation engine (`mode: "dry-run"` default) |
| `titan_dev` | `path` | `extract`, `outline`, `signature`, `complexity`, `stats`, `imports`, `todos`, `lang`, `match`, `recursive`, `flags` | 20-language structural code analyzer, complexity auditor & symbol extractor |
| `titan_normalize` | `path` | `eol`, `eof_nl`, `no_eof_nl`, `trim_trailing`, `bom`, `keep_bom`, `recursive`, `glob`, `respect_gitignore`, `check`, `dry_run`, `no_backup`, `flags` | Batch encoding, EOL, indentation & whitespace normalizer (`--` options only) |
| `titan_http` | `url` | `method`, `data`, `output`, `include`, `timeout`, `flags` | Native Windows WinHTTP client (`--` options only) |
| `titan_doc` | `path` | `info`, `sheet`, `format`, `output`, `flags` | Native DOCX/XLSX/PPTX/ODF/EPUB/RTF/PDF document extractor (`--` options only) |
| `titan_reg` | `key` | `action`, `value`, `pattern`, `recursive`, `ignore_case`, `flags` | Read-only native Win32 Registry query/keys/tree/search/export/diff (`--` options only) |
| `titan_bench` | `command` | `command2`, `warmup`, `runs`, `ignore_failure`, `flags` | High-precision Win32 command benchmarking & CPU/RSS telemetry (`--` options only) |
| `titan_git` | — | `action`, `dir`, `rev`, `rev2`, `path`, `pattern`, `limit`, `ignore_case`, `flags` | Zero-dependency native `.git` repository inspector (`info`/`status`/`log`/`diff`/`blame`/`grep`/`cat`/`reflog`/`stash`, `--` options only) |
| `titan_ftp` | `target` | `action`, `dest`, `host`, `port`, `user`, `pass`, `tls`, `recursive`, `resume`, `overwrite`, `dry_run`, `flags` | Native RFC 959/2428/3659 FTP & WinINet FTPS client and mirror sync (`--` options only) |
| `titan_dissect` | — | `path`, `mode`, `symbol`, `query`, `lines`, `around`, `pattern`, `regex`, `filter`, `numbers`, `max_tokens`, `signatures`, `complexity`, `dedent`, `hash`, `recursive`, `respect_gitignore`, `flags` | Unified 20-language X-Ray dossier, outline, surgical UTF-16/ANSI safe slice & read, cross-project symbol resolver, smart context packager & single-call symbol bundle (`--` options only) |

### Verbatim Help Manual
DIR = docs/tools/MCP--HELP.md

---------------------------------------------------------------------------------------

## 8. `titan verb` — Offset-Tolerant Atomic Patching & Instant Rollback

### Architecture & AI Patch Tolerance
AI models frequently generate unified diffs whose `@ -old_start,old_count +new_start,new_count @` line numbers are off by several lines. `VerbEngine::execute` uses `locate_hunk_with_offset` to automatically search expanding radii up to **$\pm 250$ lines** around the target line, applying the hunk cleanly and reporting the exact `applied_offset` in JSON!

### Verbatim Help Manual
DIR = docs/tools/VERB--HELP.md

---------------------------------------------------------------------------------------

## 9. `titan compare` — Myers O(ND) Unified Diff & Binary Comparison

### Architecture
Uses $O(N)$ common prefix/suffix trimming combined with Myers $O(ND)$ Shortest Edit Script (SES) for precise minimal hunks, plus a fast linear $O(N)$ path for massive dense diffs (`> 2,048` changed lines) so memory usage remains bounded and execution finishes in milliseconds.

### Verbatim Help Manual
DIR = docs/tools/COMPARE--HELP.md

---------------------------------------------------------------------------------------

## 10. `titan find` — Ultra-Fast Recursive Filesystem Discovery

### Verbatim Help Manual
DIR = docs/tools/FIND--HELP.md

---------------------------------------------------------------------------------------

## 11. `titan transform` — Stream Text Transformation & Line Filtering (`sed`)

> Pattern matching and substitutions (`s/pattern/replacement/[g|i]`, `/<pattern>/d`) run on TITAN's linear-time **Thompson NFA / Pike VM** regex engine (`core::Regex`), preventing backtracking stalls.

### Verbatim Help Manual
DIR = docs/tools/TRANSFORM--HELP.md

---------------------------------------------------------------------------------------

## 12. `titan process` — Structured Record, AWK & RFC 4180 CSV Engine (`gawk`)

> **Encoding Safety:** Input files and piped standard input (`-`) automatically strip UTF-8 BOM and decode UTF-16LE/BE cleanly into UTF-8.

### Verbatim Help Manual
DIR = docs/tools/PROCESS--HELP.md

---------------------------------------------------------------------------------------

## 13. `titan stats` — Statistical Aggregation, Percentiles & GroupBy (`datamash`)

> **Encoding Safety:** File inputs and piped stdin (`-`) transparently strip UTF-8 BOM and decode UTF-16LE/BE before `std::from_chars` numeric parsing, ensuring Windows PowerShell piped UTF-8 BOM streams parse row 1 cleanly.

### Verbatim Help Manual
DIR = docs/tools/STATS--HELP.md

---------------------------------------------------------------------------------------

## 14. `titan core-utils` — Native C++20 POSIX Utilities (All 19 Subcommands)

### Master Subcommand Overview
```text
Usage: titan core-utils <SUBCOMMAND> [OPTIONS] [ARGUMENTS...]

Subcommands:
  count, wc        Count lines (-l), words (-w), bytes (-c), max line length (-m); multi-file totals
  sort             Sort lines (-n numeric, -r reverse, -u unique, -f ignore-case, -k N field, -t C delim)
  unique, uniq     Filter adjacent duplicate lines (-c counts, -i ignore-case, -d dupes-only, -u unique-only)
  md5sum           Compute MD5 checksum
  sha256sum        Compute SHA256 checksum
  cut              Extract columns (-d delim, -f fields) or characters (-c ranges)
  paste            Merge lines of files horizontally (-d delims, -s serial)
  join             Relational join of two files on a common field (-t delim, -1 f1, -2 f2)
  split            Split a file into pieces (-l lines, -b bytes)
  head             Output first part of files (-n lines, -c bytes)
  tail             Output last part of files (-n lines, -c bytes)
  base64           Base64 encode/decode (-d decode, -u url-safe)
  rev              Reverse each line
  tr               Translate, squeeze (-s), or delete (-d) characters with ranges (a-z, A-Z, 0-9)
  grep             Search lines by pattern (-i ignore-case, -v invert, -n line-numbers, -c count, -E regex)
  touch            Create empty file or update timestamp
  cp               Copy files (-r recursive, -v verbose, -n no-clobber, supports * ? globs)
  mv               Move/rename files (-v verbose, -n no-clobber)
  rm               Remove files (-r recursive, -f force, -v verbose, supports * ? globs)

Global: -j / --json  Structured JSON output where supported
```

### Verbatim Help Manual
DIR = docs/tools/CORE-UTILS--HELP.md

---------------------------------------------------------------------------------------

## 15. `titan tr` — High-Speed L1-Table Character Translation, Squeeze & Delete

### Verbatim Help Manual
DIR = docs/tools/TR--HELP.md

---------------------------------------------------------------------------------------

## 16. `titan hex | rgb | hsl | hsla | cmyk | named | multi` — CSS Color Engine

### Verbatim Help Manual
DIR = docs/tools/COLOR--HELP.md

---------------------------------------------------------------------------------------

## 17. `titan image` — Universal Image Metadata Extractor & Multi-Format Converter (27+ Formats)

### Architecture & Hybrid Multi-Codec Engine
`ImageEngine` (`include/titan/engine/image.hpp`, `src/engine/image.cpp`) combines three zero-compromise subsystems:
1. **Zero-Copy Binary & EXIF Metadata Parser (`info` / `metadata`):** Parses headers, color spaces, bit depth, alpha channels, DPI, animation frames, PNG `tEXt` chunks, and full TIFF/JPEG **EXIF IFD0, ExifIFD, and GPSIFD** tags (Camera Make/Model, Software, DateTime, ISO, ExposureTime, FNumber, FocalLength, GPS Latitude/Longitude/Altitude) directly from `MemoryMappedFile` across 27+ formats.
2. **Native C++20 Binary & Win32 GDI+ Codecs:** Hardware-accelerated in-memory encoding/decoding for `JPG`, `JPEG`, `PNG`, `BMP`, `GIF`, `TIFF`, `ICO`, `CUR`, `TGA`, `PNM` (`PPM`/`PGM`), `PCX`, `QOI` (Quite OK Image format), `HDR` (Radiance RGBE), `DDS` (DirectDraw Surface uncompressed RGBA8), `PSD` / `PSB` (Adobe Photoshop), `SVG`, `PDF` (native PDF 1.4 `/DCTDecode` vector wrapper), and `EPS` / `AI` (PostScript Level 2 colorimage).
3. **High-Speed FFmpeg Codec Bridge:** Automatically utilizes `ffmpeg` when converting advanced next-gen/cinema formats (`WEBP`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `JP2`, `EXR`, `RAW`, `DNG`).

### Complete Supported Conversion Matrix
- **From `JPG` / `JPEG` ->** `JPEG`/`JPG`, `PNG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `ICO`, `CUR`, `TGA`, `DDS`, `JP2`, `PCX`, `PNM`, `QOI`, `HDR`, `EXR`, `SVG`, `PDF`, `EPS`, `PSD`, `PSB`, `RAW`
- **From `PNG` ->** `JPG`, `JPEG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `ICO`, `CUR`, `TGA`, `DDS`, `JP2`, `PCX`, `PNM`, `QOI`, `HDR`, `EXR`, `SVG`, `PDF`, `EPS`, `PSD`, `PSB`, `RAW`
- **From `WEBP` ->** `JPG`, `JPEG`, `PNG`, `GIF`, `BMP`, `TIFF`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `ICO`, `TGA`, `DDS`, `JP2`, `QOI`, `PDF`
- **From `GIF` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `BMP`, `TIFF`, `AVIF`, `HEIC`, `JXL`, `ICO`, `TGA`, `PDF`
- **From `BMP` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `GIF`, `TIFF`, `AVIF`, `HEIC`, `JXL`, `ICO`, `TGA`, `DDS`, `JP2`, `PDF`
- **From `TIFF` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `GIF`, `BMP`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `PDF`, `PSD`
- **From `AVIF` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `HEIC`, `JXL`, `PDF`
- **From `HEIF` / `HEIC` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `AVIF`, `HEIF`, `HEIC`, `JXL`, `PDF`
- **From `JXL` ->** `JPG`, `JPEG`, `PNG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `AVIF`, `HEIC`, `PDF`
- **From `ICO` ->** `JPG`, `JPEG`, `PNG`, `BMP`, `GIF`, `TIFF`, `WEBP`
- **From `SVG` ->** `PNG`, `JPG`, `JPEG`, `WEBP`, `GIF`, `BMP`, `TIFF`, `AVIF`, `PDF`, `EPS`
- **From `EPS` ->** `SVG`, `PDF`, `PNG`, `JPG`, `TIFF`
- **From `AI` ->** `SVG`, `EPS`, `PDF`, `PNG`, `JPG`
- **From `PSD` / `PSB` ->** `PNG`, `JPG`, `JPEG`, `WEBP`, `TIFF`, `BMP`, `PDF`
- **From `PDF` ->** `PNG`, `JPG`, `JPEG`, `WEBP`, `TIFF`, `BMP`, `SVG`
- **From `RAW` / `DNG` ->** `JPG`, `JPEG`, `PNG`, `TIFF`, `WEBP`, `AVIF`, `DNG`

### Verbatim Help Manual
DIR = docs/tools/IMAGE--HELP.md

---------------------------------------------------------------------------------------

## 18. `titan video` — Video Metadata, Frame, Contact-Sheet & WAV Extractor

### Architecture & Supported Capabilities
- **Metadata Engine:** Zero-copy `ISOBMFF` (`MP4`, `MOV`, `M4V`, `3GP`), Matroska/EBML (`MKV`, `WEBM`), `RIFF AVI`, and `FLV` box/stream parser (`VideoEngine::extract_metadata`).
- **Media Foundation + GDI+ Extraction Engine:** Loads `mfplat.dll` and `mfreadwrite.dll` dynamically (`IMFSourceReader`) with GDI+ (`gdiplus.dll`) encoding for `png`, `jpg`/`jpeg`, `bmp`, `tiff`, and `gif` frames, composite storyboard contact sheets (`--contact-sheet`, `--grid`, `--timestamps`), 16x16 luma scene-change keyframes (`--scene-threshold`), geometric transforms (`--rotate`, `--flip`, `--grayscale`), and 16-bit PCM WAV track extraction (`--extract-audio`), all using strict `--` double-dash options.

### Verbatim Help Manual
DIR = docs/tools/VIDEO--HELP.md

---------------------------------------------------------------------------------------

## 19. `titan mp3 | titan audio` — Audio Metadata, Lyrics, Cover-Art & PCM WAV Extractor

### Architecture & Audio Extraction Capabilities
`AudioEngine` (`include/titan/engine/audio.hpp`, `src/engine/audio.cpp`) performs full binary parsing & extraction across `MP3`, `FLAC`, `WAV`, `OGG`/`OPUS`, and `M4A`/`MP4`/`AAC`:
- **`ID3v2.2`, `ID3v2.3`, `ID3v2.4` & `ID3v1.1` Tags:** `TIT2`, `TPE1`, `TALB`, `TPE2`, `TCOM`, `TCON`, `TYER`/`TDRC`, `TRCK`, `TPOS`, `TBPM`, `TSSE`, `COMM`, synchronized/unsynchronized lyrics (`USLT`/`ULT`), and embedded cover artwork (`APIC`).
- **`FLAC`, `WAV`, `OGG`/`OPUS` & `M4A`/`MP4`:** `STREAMINFO` + Vorbis Comments + `PICTURE`, `RIFF WAVE` `LIST/INFO`, `OggS` Vorbis/Opus comments + Base64 `METADATA_BLOCK_PICTURE` covers, and Apple `moov/udta/meta/ilst` (`covr`, `©lyr`).
- **Cover Artwork, Report & Media Foundation WAV Extraction:** Saves embedded cover art to `--covers <DIR>`, exports metadata/lyrics in `txt`, `md`, `csv`, `lrc`, or `json` (`--format`, `--output`), and decodes audio streams to 16-bit PCM WAV (`--wav`).

### Verbatim Help Manual
DIR = docs/tools/MP3--HELP.md

---------------------------------------------------------------------------------------

## 20. `titan format` — Multi-Language Code Formatter, Minifier & Syntax Validator (`JS`, `JSON`, `CSS`, `HTML`, `SQL`, `C++`)

### Architecture & Supported Languages
`FormatEngine` (`include/titan/engine/format.hpp`, `src/engine/format.cpp`) provides deterministic, zero-dependency lexical formatting, minification (`--minify`), and structural syntax validation (`--check`) across:
1. **`JSON` / `JSONC`:** Full structural validator (reports exact line & column on syntax error), pretty-printer, minifier, and recursive alphabetical object key sorter (`--sort-keys` / `-s`).
2. **`JavaScript` (`JS`, `MJS`, `CJS`) & `TypeScript` (`TS`, `JSX`, `TSX`):** Context-aware lexer handling strings (`'...'`, `"..."`, `` `...` `` template literals), regex literals, comments (`//`, `/*...*/`), control-flow (`if`/`for`/`while`/`switch`), object/array literals, and statement indentation.
3. **`CSS` / `SCSS` / `LESS`:** Selector, media query, declaration block, and semicolon/colon spacing formatter and minifier.
4. **`HTML` / `XML` / `SVG`:** Tag hierarchy indenter (automatically recognizes HTML5 void elements `<br>`, `<img>`, `<input>`, `<meta>`, `<link>`, etc.) and whitespace minifier.
5. **`SQL`:** Clause-level (`SELECT`, `FROM`, `WHERE`, `LEFT JOIN`, `GROUP BY`, `ORDER BY`, `LIMIT`) structural formatter and uppercase keyword normalizer.
6. **`C` / `C++` / `C#` / `Java`:** Preprocessor directive (`#include`, `#define`) and brace/statement indentation engine.

### Verbatim Help Manual
DIR = docs/tools/FORMAT--HELP.md

---------------------------------------------------------------------------------------

## 21. `titan agent | context | symbol | deps | audit | edit` — AI-Powered Agent Intelligence Suite

### Architecture & 5 Next-Generation AI-Agent Engines
`AgentEngine` (`include/titan/engine/agent.hpp`, `src/engine/agent.cpp`) gives AI coding agents (`Antigravity`, `Codex`, `Claude Code`, `Cursor`) five zero-index, microsecond-latency intelligence and surgical modification tools accessible both via `titan agent <subcommand>` and as direct top-level commands:

1. **`titan context <query> [dir]` (Smart AI Context Packager & Token Budget Enforcer):**
   - Automatically finds all AST definitions and call-site references for a symbol/keyword across the workspace, extracts the exact AST function/class code blocks (`[start_line:end_line]`) with `SHA-256` file hashes, calculates the exact LLM token estimate (`~4 chars/token`), and packs them within `--max-tokens <N>` (default: `4000`).
2. **`titan symbol <name> [dir]` (Zero-Index Cross-Project Symbol Resolver / Mini-LSP):**
   - Separates exact **Definitions** (`class`, `struct`, `enum`, `namespace`, `function` with `[start_line:end_line]` bounds) from **References / Call Sites** (`file:line` + code snippet) across C/C++, C#/Unity, JS/TS, Python, Rust, Go, and Java.
3. **`titan deps [file_or_dir]` (Dependency, Include/Import & Unity GUID Graph Analyzer):**
   - Extracts C/C++ `#include`, JS/TS `import`/`require`, C# `using`, and Unity `.meta`/`.prefab`/`.unity` `guid:` dependencies, with `--reverse <name>` to find every file that depends on a given header, module, or Unity asset GUID.
4. **`titan audit [dir]` (Codebase Security, Secret Scanner, Complexity Hotspot & Token Auditor):**
   - Scans the entire workspace in milliseconds to report:
     - **Hardcoded Secrets / Keys:** Private keys, AWS `AKIA...` keys, `ghp_` / `sk-` API tokens.
     - **Technical Debt:** `TODO`, `FIXME`, `HACK`, `BUG`, `XXX` comments with exact `file:line`.
     - **Complexity Hotspots:** Functions spanning $\ge 120$ lines (`file:start-end`).
     - **Language & Token Budget Breakdown:** Total files, lines, bytes, and estimated LLM tokens per extension.
5. **`titan edit <file> <start:end>` (Surgical Line-Range Block Editor with SHA-256 Optimistic Lock):**
   - Replaces, inserts (`--insert`), or deletes (`--delete`) lines `START:END` atomically using `--content "<code_block>"` or `--input <file>`, verifying `--expect-hash <sha256>` before writing and creating collision-proof `.orig.~N~` backups (`--backup`), or executes multi-file batch manifests atomically with `--batch <MANIFEST.json>` and `--validate <CMD>` via `titan tx`.

### Verbatim Help Manual
DIR = docs/tools/AGENT--HELP.md

---------------------------------------------------------------------------------------

## 22. `titan convert | analyze | validate | fix` — Structured Data, Qt Designer & Sublime Text Engine

Implemented in `src/engine/structured.cpp` (general formats, CLI) and `src/engine/sublime_qt.cpp` (Qt `.ui`, Sublime Text). All commands accept `--input/-i` (or positional), `-j/--json`, `-q/--quiet`; `convert` also `--output/-o`, `--from`, `--to`, `--force`; `fix` also `--dry-run/-n`, `--backup/-b`, `--output/-o`, `--report <file>`. `inspect-file` is an alias of `analyze`. Writes are atomic; `convert` refuses to overwrite its own input without `--force`.

Exit codes: `analyze`/`validate` 0 = valid, 1 = invalid, 2 = error. `fix` 0 = repaired/valid, 1 = safe repair impossible.

### Verbatim Help Manual
DIR = docs/tools/STRUCTURED--HELP.md

---------------------------------------------------------------------------------------

## 23. `titan name-files` — Windows Filename Inspection & Safe Batch-Renaming Engine

Implemented in `src/engine/name_files.cpp` (`include/titan/engine/name_files.hpp`). Windows-native filename case inspector and safe batch-renaming engine supporting non-destructive query modes, Windows wildcard/glob target expansion (`*.txt`, `dir\*.*`), and atomic pre-validated transform modes.

### Key Capabilities
- **Query Modes (Read-Only):**
  - `-upper`, `--upper-case`: Extract files with ALL UPPER CASE names.
  - `-lower`, `--lower-case`: Extract files with all lower case names.
  - `-title`, `--title-case`: Extract files with Title Case names.
  - `-extension`, `--extract-extension`: Extract and list file extensions (with `--unique` and `--count`).
- **Transform Modes (Safe Batch Rename):**
  - **Case Conversion:** `-to-upper`, `-to-lower`, `-to-title` (optional `--include-extension`).
  - **Text Insertion:** `-add-to` with `--char <text>` and `--place <prefix|suffix|position:N>`.
  - **Text Removal:** `-remove` with `--char <text>` (optional `--first`, `--ignore-case`).
  - **Numbering & Templating:** `-numbering`, `-rename` with `--prefix`, `--suffix`, `--number <tmpl>`, `--start <tmpl>`, `--char <sep>`.
  - **Extension Changing:** `-extension-change` with `--ext <*.old>` and `--to-ext <*.new>`.
- **Built-in Safety & Protection:**
  - **Pre-Flight Validation:** Two-phase execution plans all renames first and detects internal batch collisions and on-disk target collisions *before* any file is renamed.
  - **Windows Sanitization:** Automatically sanitizes invalid characters (`< > : " / \ | ? *`), trailing dots/spaces, and reserved Windows device names (`CON`, `PRN`, `AUX`, `NUL`, `COM1-9`, `LPT1-9`).
  - **UTF-8 Safe:** Never corrupts multi-byte sequences (Arabic, CJK, accents).
  - `--dry-run`: Preview all changes without modifying any file.
  - `--force`: Allow overwriting target files.
  - `--json`: Structured output for AI agents.

### Verbatim Help Manual
DIR = docs/tools/NAME-FILES--HELP.md

---------------------------------------------------------------------------------------

## 24. `titan read` — Agent-Oriented Universal File Reader & Linear-Time Regex Engine

Implemented in `src/engine/read.cpp` (`include/titan/engine/read.hpp`). Specialized agent-oriented text reader and searcher. Automatically decodes UTF-8, UTF-8 BOM, UTF-16, and legacy ANSI files, rejects binaries, and always emits valid UTF-8. The regex engine is strictly linear-time (Thompson NFA/DFA), eliminating any risk of catastrophic ReDoS backtracking.

### Key Capabilities
- **Encoding Independence:** Transparently handles UTF-8, UTF-16LE, UTF-16BE, and ANSI without external conversion.
- **Line Selection:** `--lines N | A-B | A- | -B | tail:K`, `--from N`, `--limit N`, `--all`.
- **Search & Regex:** `-string`, `-regex`, `-case-insensitive`, `-word`, `--only-matching`, `--context-lines N` (`-before`, `-after`).
- **Pre-Search Filters:** `-filter blank,nonblank,comments,nocomments,code,ascii,nonascii`, `-len <spec>`.
- **Output Shaping:** `-upper`, `-lower`, `-title`, `-u`/`--unique`, `-duplicate`/`--duplicates`, `-sort[=mode]`, `-num`/`--numbers`, `-count`/`--counts`, `--line-numbers`, `--json`.
- **Safety Caps:** Automatically limits output to 2,000 records or 1 MiB to prevent agent context overflow unless `--all` or `--limit` is specified.
- **AI Agent Operating Blueprint:** See `docs/AI_AGENT_OPERATING_BLUEPRINT.md` for deterministic 8-stage pipeline ordering, token-saving best practices (`-filter code`), and tool orchestration rules.

### Verbatim Help Manual
DIR = docs/tools/READ--HELP.md

---------------------------------------------------------------------------------------

## 25. `titan archive` — Native Universal Archive Suite (`ZIP/ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`, `7Z`, `RAR4`, `RAR5`)

### Architecture, Capabilities & Security Guards
Implemented in `src/engine/archive.cpp` (`include/titan/engine/archive.hpp`) with zero external dependencies (`zlib`, `zstd`, `libarchive`, `7zip` not required):
- **Full Read / Create / Extract / Verify (`ZIP/ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`):**
  - Native **RFC 1951 Deflate/Stored** (`ZIP`), **ZIP64 Extended Headers** (`--zip64`, >65,535 entries / >4 GiB), and **RFC 1952 GZIP** compression/decompression with CRC-32 & `ISIZE` validation.
  - Native **RFC 8878 Zstandard** (`ZSTD` / `.zst` and `TAR.ZST` / `.tar.zst`) compressor/decompressor with XXH64 checksum validation.
  - True streaming **POSIX `ustar` TAR** reader and writer supporting 255-byte paths (`name[100]` + `prefix[155]`), 12-byte base-256 binary sizes for large entries, recursive directory collection, and automatic `.tar.gz` / `.tar.zst` single-stream compression.
- **Native 7Z Extraction & Header Verification (`7Z`, `RAR4`, `RAR5`):**
  - **7Z:** Genuine `kHeader` (`0x01`) / `kEncodedHeader` (`0x17`) parser, `SubStreamsInfo`, UTF-16LE names, native extraction via `Copy`, `Deflate`, `LZMA1`, `LZMA2`, and `Zstd` codecs with strict bounds and CRC-32 verification (creation not supported).
  - **RAR4 / RAR5:** Binary magic signature detection (`detect`), container header inspection, archive cataloging (`list`), and block structure integrity checking (`test`).
- **Built-In Hardening & Safety Guards:**
  - **Zip-Slip Defense:** Rejects absolute paths, drive prefixes, and `..` traversal components before touching disk.
  - **Zip-Bomb & Resource Quota Guards:** Bounds entry counts, decompressed stream sizes, and per-file allocations to prevent exhaustion attacks.
  - **Collision & Hostile Path Protection:** `--no-overwrite` skips existing targets cleanly; Windows reserved device names (`CON`, `PRN`, `AUX`, `NUL`, `COM1..9`, `LPT1..9`) and illegal filename characters are sanitized/rejected; atomic writes guard archive creation (`--dry-run` previews without disk mutation).

### Live Format Capability Matrix (`titan archive caps`)
| Format | Read (`list`) | Extract (`-x`) | Create (`-c`) | Verify (`test`) | Notes |
| :--- | :---: | :---: | :---: | :---: | :--- |
| `ZIP` | ✅ | ✅ | ✅ | ✅ | RFC 1951 Deflate/Stored with ZIP64 (`--zip64`) & CRC-32 verification |
| `TAR` | ✅ | ✅ | ✅ | ✅ | Streaming POSIX `ustar` reader & writer (255-byte `prefix[155]`) |
| `GZIP` | ✅ | ✅ | ✅ | ✅ | RFC 1952 streaming compressor/decompressor with `ISIZE`/CRC-32 |
| `TAR.GZ` | ✅ | ✅ | ✅ | ✅ | GZIP-compressed POSIX `ustar` archive |
| `ZSTD` | ✅ | ✅ | ✅ | ✅ | RFC 8878 native Zstandard compressor/decompressor with XXH64 checksum |
| `TAR.ZST` | ✅ | ✅ | ✅ | ✅ | Zstandard-compressed POSIX `ustar` archive |
| `7Z` | ✅ | ✅ | ❌ | ✅ | Genuine header/`EncodedHeader` parser + `Copy`/`Deflate`/`LZMA`/`LZMA2`/`Zstd` extraction & CRC-32 verify |
| `RAR4` | ✅ | ❌ | ❌ | ✅ | Magic detection, header inspection & block metadata verification |
| `RAR5` | ✅ | ❌ | ❌ | ✅ | Magic detection, header inspection & block metadata verification |

### Verbatim Help Manual
DIR = docs/tools/ARCHIVE--HELP.md

---------------------------------------------------------------------------------------

## 26. `titan ast-search | ast-replace` — Structural AST Pattern Search & Rewrite Engine

### Verbatim Help Manual
DIR = docs/tools/AST--HELP.md

---------------------------------------------------------------------------------------

## 27. `titan query` — Structured Path/Filter Query & Mutation Engine

### Verbatim Help Manual
DIR = docs/tools/QUERY--HELP.md

---------------------------------------------------------------------------------------

## 28. `titan table` — Streaming SQL-Lite Analytics (`CSV`, `TSV`, `JSONL`)

> **Encoding Safety:** Input files and stdin (`-`) strip UTF-8 BOM and decode UTF-16LE/BE cleanly before header/column parsing.

### Verbatim Help Manual
DIR = docs/tools/TABLE--HELP.md

---------------------------------------------------------------------------------------

## 29. `titan lsp` — JSON-RPC 2.0 LSP Bridge & Zero-Index Fallback

### Verbatim Help Manual
DIR = docs/tools/LSP--HELP.md

---------------------------------------------------------------------------------------

## 30. `titan tx` — Multi-File Atomic Transaction Engine & Rollback Journal

### Verbatim Help Manual
DIR = docs/tools/TX--HELP.md

---------------------------------------------------------------------------------------

## 31. `titan inject` / `titan injection` — Surgical Code & Text Injection

### Purpose & Core Safety Rules
- **Strict Double-Dash CLI Contract:** Only `--<option>` flags are accepted (single-dash flags such as `-l`, `-i`, or `-h` exit with `2` and never touch disk). Use `--` before filenames starting with `-`.
- **Default Backup & Optimistic Lock:** Creates `.orig` (or `.orig.~N~`) backups automatically before any disk write unless `--no-backup` is passed. Supports `--dry-run`, `--expect-hash <SHA256>`, `--check-syntax`, and `--unique` idempotency.
- **Unicode & Encoding Integrity:** `--col` indexes 1-based Unicode codepoints (not raw UTF-8 bytes) and preserves UTF-8 BOM, UTF-16LE/BE encoding, and dominant `\r\n` vs `\n` line endings (`--newline auto|crlf|lf`).
- **Single-Block Formatting (`--format-block`):** Expands and formats **only** the injected payload without reformatting the surrounding file across C/C++/C#/Java, JS/TS, JSON/JSONC, CSS, HTML/XML/SVG, and SQL (safely rejects Python/unsupported languages with exit `2`).

### Verbatim Help Manual
DIR = docs/tools/INJECT--HELP.md

---------------------------------------------------------------------------------------

## 32. `titan run` / `titan ti` — Native TITAN (`.ti`) Text-Processing Scripting Language

### Purpose & Core Design
- **Zero-Dependency Native Execution:** Runs `.ti` multi-step text, CSV, JSON, and file automation pipelines directly inside `titan.exe` over `MemoryMappedFile`, `core::text::decode_bytes` (`UTF-8`, `UTF-8 BOM`, `UTF-16LE/BE`, `ANSI`), linear-time `core::Regex`, and `BackupManager::atomic_write`.
- **Self-Contained AI & User Discoverability:** Any external model or developer with only `titan.exe` on `PATH` (or via `titan mcp`) learns `.ti` syntax directly from the binary via `titan run --guide` (or `--spec` / `--json`), the quick syntax summary in `titan run -h`, and `guide: true` on `titan_run` MCP tool.
- **Full Functional & Control-Flow Support (`v2.0.3`):** `tita` declarations, destructuring (`tita [a, ...rest] = xs`, `tita {k, k2: v, ...rest} = m`), spread (`...`), default & rest parameters (`fn f(a, b = 10, ...rest)`), closures, recursion, arrow lambdas (`x => expr`, `(a, b) => expr`), `while`, `each k, v in map`, `match` / `switch`, optional chaining (`?.`, `?[...]`), null-coalescing (`??`), `import "file.ti"`, `save ... prepend`, `mkdir` + `save` dry-run simulation, `try / catch / throw` (with `Call stack:` traces on nested errors), ternary `cond ? a : b`, template literals `` `...${expr}...` ``, and built-ins (`insert`, `prepend`, `remove_at`, `pop`, `now`, `timestamp`, `timestamp_us`, `format_date`, `file_mtime`, `env`, `args`, `from_csv`, `to_csv`, `md_table`, `min`/`max`/`sum`/`mean` with list or 2+ args, `unique_by`, `count_by`, `sha256`, `base64_encode`, `base64_decode`, `regex_match`, `union`, `intersect`, `difference`, `pick`, `omit`, `from_entries`, `stdin`, `open stdin`, `exit`, `sleep`).
- **Two-Tier TITAN Bridge & Safety Guards:** Call TITAN commands directly inside `.ti` (`titan find src -ext cpp`, `titan archive create ...`, `titan core-utils sha256sum ...`) with automatic `List` expansion. Server/recursive commands (`mcp`, `lsp`, `run`, `ti`) are blocked; `--dry-run` (`-n`) blocks disk writes and mutating `titan` subcommands; `--check` validates syntax and static `import` paths without execution; `--max-steps` (default `20000000`, max `1000000000`) and depth caps (`256`) prevent infinite loops or stack exhaustion.

### Verbatim Help Manual
DIR = docs/tools/RUN--HELP.md

---------------------------------------------------------------------------------------

## 33. `titan dir` — Smart Directory Inspection, Classification & Diagnostics

### Purpose & Core Design
- Replaces slow PowerShell `Get-ChildItem` / `Measure-Object` pipelines with a native C++20 directory intelligence engine.
- **Path Display Modes:** Use `titan dir --full-paths` to print full canonical/resolved paths, `--names` for basenames only, and `--relative` for paths relative to the target directory. (For `titan find`, use `--full` or `--full-paths`.)

### Verbatim Help Manual
DIR = docs/tools/DIR--HELP.md

---------------------------------------------------------------------------------------

## 34. `titan create` — Batch File & Directory Creation Engine

### Verbatim Help Manual
DIR = docs/tools/CREATE--HELP.md

---------------------------------------------------------------------------------------

## 35. `titan copy` — Verified, Filter-Aware File & Directory Copy Engine

### Verbatim Help Manual
DIR = docs/tools/COPY--HELP.md

---------------------------------------------------------------------------------------

## 36. `titan move` — Crash-Safe File & Directory Move Engine

### Verbatim Help Manual
DIR = docs/tools/MOVE--HELP.md

---------------------------------------------------------------------------------------

## 37. `titan rename` — Collision-Safe Composable Batch Renaming Engine

### Verbatim Help Manual
DIR = docs/tools/RENAME--HELP.md

---------------------------------------------------------------------------------------

## 38. `titan info` — Fast Runtime Health, Binary & Guide Inspector

### Purpose & Core Design
- Prints TITAN's active version, platform, executable path, binary size, registered command count, `PATH` availability, presence of `TITAN_HELP.md` and `TITAN_LANGUAGE_GUIDE.md` in `%USERPROFILE%\.gemini`, and `.ti` built-in guide availability (`Status: OK`).

### Verbatim Help Manual
DIR = docs/tools/INFO--HELP.md

---------------------------------------------------------------------------------------

## 39. `titan system` — Native Windows Environment, Hardware, Disk, Network & Process Inspector

### Purpose & Core Design
- Zero-third-party-library native Win32 system intelligence tool across 39 commands covering persistent/process environment variables, `PATH` verification, OS/hardware/BIOS/battery/screen telemetry, drives/folders/temp audits, network adapters/ports, processes (with protected PID `0`/`4`/self refusal on `--kill`), Windows services, drivers, startup entries, and installed apps.
- Supports `-j` / `--json` (`JsonValue::envelope`) and smart typo suggestions on unknown sub-flags. (`--hotfixes` is intentionally excluded to avoid COM/WMI runtime overhead.)

### Verbatim Help Manual
DIR = docs/tools/SYSTEM--HELP.md

---------------------------------------------------------------------------------------

## 40. `titan delete` — Safe Windows File & Folder Deletion Engine

Safe Win32 file and folder deletion engine with protected-path guard, NTFS symlink/junction safety, Recycle Bin support, multi-pass secure wipe, age/size filters, and `--dry-run` preview.

### Verbatim Help Manual
DIR = docs/tools/DELETE--HELP.md

---------------------------------------------------------------------------------------

## 41. `titan dev` — Multi-Language Structural Code Analyzer & Symbol Extractor (20 Languages)

Native 20-language structural code analyzer, symbol lister, single-call symbol source extractor (`-x`), complexity/stats/imports/TODO reporter, and MCP tool (`titan_dev`).

### Verbatim Help Manual
DIR = docs/tools/DEV--HELP.md

---------------------------------------------------------------------------------------

## 42. `titan bench` — High-Precision Win32 Benchmark & Telemetry Runner (`--` ONLY)

### Architecture & Algorithmic Behavior
- Native C++20 / Win32 process benchmarking engine supporting `--shell cmd`, `--shell pwsh`, and `--shell none` (direct `CreateProcessW` with zero shell startup overhead).
- Captures wall-clock latency, user+kernel CPU time (`GetProcessTimes`), peak RSS memory (`GetProcessMemoryInfo`), percentiles (`p90`, `p95`, `p99`), IQR outlier counts, parameter sweeps (`--param`, `--param-range`), and lifecycle hooks (`--setup`, `--prepare`, `--cleanup`, `--conclude`).
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/BENCH--HELP.md

---------------------------------------------------------------------------------------

## 43. `titan git` — Zero-Dependency Native `.git` Repository Inspector (`--` ONLY)

### Architecture & Algorithmic Behavior
- Directly decodes `.git/HEAD`, `.git/refs/*`, `.git/packed-refs`, `.git/logs/*`, `.git/config`, `.git/index` (v2/v3/v4), and loose/packed objects with built-in RFC 1950/1951 inflate — zero `libgit2` and zero `git.exe` subprocesses.
- Supports `info`, `status`, `branches`, `tags`, `log`, `show`, `files`, `remotes`, `rev-parse`, plus native Myers $O(ND)$ `diff`, history `blame`, tree-blob `grep`, historical `cat`, `reflog`, and `stash`.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/GIT--HELP.md

---------------------------------------------------------------------------------------

## 44. `titan http` — Advanced Native Windows WinHTTP Client (`--` ONLY)

### Architecture & Algorithmic Behavior
- Dynamically loads Windows `winhttp.dll` at runtime with native Base64 `--basic` auth, `--bearer` tokens, URL query parameter encoding (`--query`), `--cookie`/`--cookie-jar` persistence, native `multipart/form-data` builder (`--form`), `--data-json`, retries, HTTP/2 negotiation (`--http2`), proxy support, and protected-path atomic downloads.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/HTTP--HELP.md

---------------------------------------------------------------------------------------

## 45. `titan ftp` — Native RFC 959/2428/3659 FTP & WinINet FTPS Client (`--` ONLY)

### Architecture & Algorithmic Behavior
- Combines a full native WinSock (`ws2_32.dll`) RFC 959/2428/3659 FTP engine (`EPSV`, `PASV`, active `PORT`, `MLSD` + Unix/IIS `LIST` parser, `REST` offset resume, `RNFR`/`RNTO`) with dynamic WinINet (`wininet.dll`) encrypted `FTPS` (`ftps://` / `--tls`) transport.
- Includes `--recursive` directory transfers, size-aware mirror `sync` (`--dry-run`, `--delete`), SHA-256 verification (`--verify`), protected-path refusal, and Zip-Slip remote path traversal guards.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/FTP--HELP.md

---------------------------------------------------------------------------------------

## 46. `titan doc` — Native Office, EPUB, RTF & PDF Document Extractor (`--` ONLY)

### Architecture & Algorithmic Behavior
- Extracts structured text, headings, tables, metadata, speaker notes, and headers across `DOCX`, `XLSX`, `PPTX`, `ODT`, `ODS`, `ODP`, `EPUB`, `RTF`, and native `PDF` (including `/FlateDecode` streams, PNG row predictors, `ToUnicode` CMaps, and `/Info` dictionaries) with zero external libraries.
- Converts Excel serial date cells cleanly to ISO `YYYY-MM-DD`, respects `--sheet`, `--slide`, and `--page` slices, filters with `--search`, and refuses encrypted PDFs or protected system `--output` paths cleanly.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/DOC--HELP.md

---------------------------------------------------------------------------------------

## 47. `titan reg` — Native Win32 Windows Registry Inspector, Diff & Exporter (`--` ONLY)

### Architecture & Algorithmic Behavior
- Read-only native Win32 Registry inspector supporting `query`, `keys`, `tree`, `search`, `.reg` v5.00 `export`, and key-to-key `diff`, with 32/64-bit view switching (`--wow64`), `REG_EXPAND_SZ` expansion (`--expand`), type filters, depth/limit caps, and protected-path atomic writes.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/REG--HELP.md

---------------------------------------------------------------------------------------

## 48. `titan normalize` — Batch Encoding, EOL, Indentation & Whitespace Normalizer (`--` ONLY)

### Architecture & Algorithmic Behavior
- Decodes UTF-16LE/BE/ANSI/UTF-8 BOM files cleanly into normalized UTF-8, converts EOLs (`--lf`/`--crlf`), enforces/strips EOF newlines, converts tab/space indentation (`--tabs-to-spaces`, `--spaces-to-tabs`), collapses consecutive blank lines (`--collapse-blank-lines`), strips stray ASCII control bytes (`--strip-control`), and emits Myers unified diffs (`--diff`) with `.orig` backups and protected-path guards.
- **Strict CLI Contract:** All options require double dashes (`--`); single-dash flags are rejected with exit code `2`.

### Verbatim Help Manual
DIR = docs/tools/NORMALIZE--HELP.md

---------------------------------------------------------------------------------------

## 49. `titan dissect` — Unified 20-Language Code & Text Dissection Super-Engine

### Architecture & Unified Workflow
`titan dissect` (`DissectEngine`, MCP tool: `titan_dissect`) unifies the core capabilities of `slice`, `read`, `dev`, `outline`, `context`, and `symbol` into a single cohesive, zero-dependency, 20-language structural & multi-encoding dissection engine. Enforces **strict double-dash (`--`) options ONLY** (single-dash flags are rejected with exit code `2` and an actionable hint).

### Verbatim Help Manual
DIR = docs/tools/DISSECT--HELP.md

---------------------------------------------------------------------------------------

## 50. `titan merge` — Streaming Multi-Format File Merger (`--` ONLY)

### Architecture & Unified Workflow
`titan merge` (`MergeEngine`) merges two or more files across `text`, `binary`, `lines`, `bytes`, `json`, `jsonl`, `csv`, `tsv`, `xml`, `html`, `srt`, `vtt`, and `m3u` with O(1)-RAM streaming for binary/line modes, 154+ strict `--`-only long options (supporting `--opt value`, `--opt=value`, and `--no-...` negation), splitting, templates, streaming `md5`/`sha1`/`sha256`/`sha512`/`crc32` hashing, `--verify`, manifests, file locking, and Windows long-path/Unicode safety.

### Verbatim Help Manual
DIR = docs/tools/MERGE--HELP.md
