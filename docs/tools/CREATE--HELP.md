## 34. `titan create` — Batch File & Directory Creation Engine

### Verbatim Help Manual
```text
Usage: titan create [OPTIONS] [--] <target> [target...]

Target Modes & Paths:
  -d, --dir, --folder           Create directories
  -f, --file                    Create files (default)
  -p, --parents                 Create missing intermediate parent directories
  --tree                        Enable nested hierarchy/tree creation (implies --parents)
  --base <dir>                  Resolve relative targets under <dir> (with canonical traversal guard)
  --from-list <file>            Read targets line-by-line (UTF-8/UTF-16, ignores # comments)

Numbering & Templates:
  -n, --number <N>, --prefix, --suffix, --infix, --sep <str>, --pad <digits>,
  --start <N>, --start-prefix <N>, --start-suffix <N>, --start-infix <N>, --step <S>,
  --template <fmt> ({stem}, {ext}, {num}, {date}, {time}, {uuid}, {rand}),
  --date <fmt>, --timestamp, --ext <.ext>, --stem-only, --case <lower|upper|title|keep>

Content, Encoding, Safety & Output:
  --empty/--touch, -c/--content <text>, --unescape, --from-file <path>, --raw, --stdin,
  --encoding <utf8|utf8-bom|utf16le|utf16be>, --newline <auto|lf|crlf>, --size <BYTES|K|M|G>,
  --dry-run, --fail-existing, --skip-existing, --overwrite, -b/--backup, --force, --atomic,
  -q/--quiet, -v/--verbose, -j/--json
```
