# TITAN Programming Language (`.ti`) — Complete Learning & Engineering Guide

> **Runtime Engine:** `titan.exe` (100% Native C++20, Zero-Dependency)  
> **Architect:** Nourddine Bakour  
> **Audience:** Humans learning `.ti` from zero, and AI models writing `.ti` code with zero prior exposure.

---

## Part I: How Any AI Model or Developer Discovers `.ti` Immediately

If an AI assistant or developer encounters `.ti` for the first time with only `titan.exe` on `PATH`:

1. **Print the Full Built-In Language Spec Directly from the Binary:**
   ```powershell
   titan run --guide
   ```
   *(Valid flags: `--guide` or `--spec`; add `-j` for JSON output. Note: `--guids` with an `s` is invalid and returns exit code `2`.)*
2. **Discover via MCP (`titan mcp --stdio`):**
   Invoke tool `titan_run` with:
   ```json
   { "guide": true }
   ```
3. **Self-Healing Compiler Feedback:**
   Every syntax or runtime mistake prints exact `file:line:col` plus actionable hints (e.g., advising `tita` instead of `let`/`var`, `elif` instead of `else if`, or suggesting close variable names).
4. **PowerShell Quoting Tip:**
   On Windows PowerShell, inline `-c "..."` strings often have inner double quotes stripped by Windows argument parsing. For multi-line scripts or scripts containing double quotes, always write a `.ti` file and run `titan run script.ti`.

---

## Part II: Step-by-Step Curriculum (Beginner to Expert)

### Lesson 1: Variables (`tita`) & the Four String Forms
Always declare a new variable with `tita`. Mutate existing variables without `tita`:

```ti
tita title = "TITAN"
tita count = 10
count += 5              // now 15 (=, +=, -=, *=, /=, %= supported)
```

`.ti` gives you four distinct string literals tailored for text/code generation:

| Syntax | Escapes (`\n`, `\t`) | Interpolation | Best Use Case |
|---|---|---|---|
| `"..."` | Yes | Simple `"{var}"`, `"{obj.k}"`, `"{$1}"` | Standard log/status messages |
| `'...'` or `r"..."` | **No** (Raw) | **No** (Raw) | Windows paths & regex patterns |
| `"""..."""` / `r"""..."""` | Optional (`r"""` raw) | Simple in `"""` | Static multi-line blocks |
| `` `...${expr}...` `` | Yes | **Any full expression** (`${a + b}`, pipes, ternary) | HTML/CSS/JS/code templates |

**Example:**
```ti
tita user = "nourddine"
tita n = 3
print `Hello ${user | upper}: ${n} ${n == 1 ? "file" : "files"}`
// Output: Hello NOURDDINE: 3 files
```

---

### Lesson 2: Lists, Maps & Data Slicing (Exact Verified Outputs)

All indexing (`list[0]`, `slice`) is **0-based**. `slice(start, end)` is **end-exclusive**.

```ti
tita nums = [10, 20, 30, 40]
print nums | slice(1, 3) | to_json          // [20,30]
print zip([1, 2], ["a", "b"]) | to_json     // [[1,"a"],[2,"b"]]
print enumerate(["x", "y"]) | to_json       // [[0,"x"],[1,"y"]]
print chunk([1, 2, 3, 4, 5], 2) | to_json   // [[1,2],[3,4],[5]]
```

Maps support both `map["key"]` and `map.key`, and can use `has(m, "key")`, `keys(m)`, `values(m)`, `items(m)`, `merge(a, b)`, and `without(m, "key")`:

```ti
tita cfg = { host: "localhost", port: 8080 }
cfg.port = 9090
print keys(cfg) | join ", "                 // host, port
```

---

### Lesson 3: Conditionals, Loops & Error Handling

#### Conditionals (`if / elif / else`)
Always write `elif`, never `else if`:
```ti
tita score = 88
if score >= 90 {
    print "A"
} elif score >= 80 {
    print "B"
} else {
    print "C"
}
```

#### Loops (`each` and `while`)
```ti
// 1) Value iteration
each item in ["alpha", "beta", "gamma"] {
    if item == "beta" { continue }
    print item
}

// 2) Index + Value iteration over List
each i, color in ["#C9B00B", "#FAF7E8"] {
    print `${pad_left(i + 1, 2, "0")}: ${color}`
}

// 3) Key + Value iteration over Map
each k, v in { a: 1, b: 2 } {
    print `${k}=${v}`
}

// 4) While loop (bounded by --max-steps)
tita step = 0
while step < 3 {
    step += 1
}
```

#### Error Handling (`try / catch / throw / assert`)
`catch err` binds `err` as a **Map** containing `{ message, line, col, value }`:
```ti
try {
    assert(false, "invalid input")
} catch err {
    print `Caught at ${err.line}:${err.col}: ${err.message}`
}
```
*(Important: Safety caps like `--max-steps`, `max_output_bytes`, and out-of-memory cannot be caught.)*

---

### Lesson 4: Functions, Arrow Lambdas, Closures & Higher-Order Pipes

Named functions (`fn`) must be defined before calling and enforce exact argument counts. Closures capture outer variables by reference:

```ti
fn make_adder(base) {
    return x => base + x
}

tita add10 = make_adder(10)
tita nums = [1, 2, 3, 4, 5]

// Pipeline: filter odd numbers -> add 10 -> sum via reduce
tita total = nums
    | filter(x => x % 2 == 1)
    | map(x => add10(x))
    | reduce((acc, x) => acc + x, 0)

print total   // 11 + 13 + 15 = 39
```

**Verified Higher-Order Output Shapes:**
```ti
tita rows = [{d: "a", v: 1}, {d: "b", v: 2}, {d: "a", v: 3}]
print rows | group_by(r => r.d) | to_json
// {"a":[{"d":"a","v":1},{"d":"a","v":3}],"b":[{"d":"b","v":2}]}

print [{d: "a", v: 10}, {d: "b", v: 2}] | sort_by(r => r.v, "desc") | to_json
// [{"d":"a","v":10},{"d":"b","v":2}]
```

**Pipe Lambda Rule:** Unparenthesized arrow lambdas in a pipe stop at the next `|` (`xs | map x => x * 2 | sum`), whereas multi-parameter lambdas should be parenthesized (`reduce((a, b) => a + b, 0)`).

---

### Lesson 5: File I/O, CSV Auto-Typing & Regex Engine

- `open <path> [as text|lines|csv|json]`: Auto-decodes `UTF-8`, `UTF-8 BOM`, `UTF-16LE/BE`, and `ANSI`; rejects binary files.
- When reading `as csv`, `.ti` uses the header row as Map keys and **automatically parses numeric fields** into numbers!
  ```csv
  name,score
  Ann,95
  Bob,80
  ```
  ```ti
  tita rows = open "scores.csv" as csv
  print to_json(rows)
  // [{"name":"Ann","score":95},{"name":"Bob","score":80}]
  ```
- **Linear-Time Regex (`~`, `!~`, `match`, `match_all`, `filter`, `replace`):**
  ```ti
  tita s = "foo_1_2"
  print s | replace /[0-9]+/ with "X"    // foo_X_X (global regex replace)
  print s | replace "_1_" with "-Z-"      // foo-Z-2 (literal replace)
  ```
- **Safe Writing (`mkdir` & `save`):**
  ```ti
  mkdir("out/site")
  save content to "out/site/index.html" atomic backup
  ```
  `--dry-run` turns `save` and `mkdir` into safe previews without touching disk; check `if not dry_run { ... }` before reading back newly saved files.

---

### Lesson 6: Safe Tier-2 TITAN CLI Bridge

Any non-recursive TITAN subcommand runs directly inside `.ti` and **returns its captured stdout as a `string`**:

```ti
tita sha_line = titan core-utils sha256sum "data.csv"
tita cpp_list = titan find "src" -ext cpp | lines
titan archive create "bundle.zip" cpp_list
```

- `List` arguments are expanded automatically.
- Mutating commands obey `--dry-run` and the OS protected-path lock.
- Blocked inside `.ti`: `mcp`, `lsp`, `run`, `ti`.

---

## Part III: Complete Production Cookbook (3 End-to-End Recipes)

### Recipe 1: Server Log Audit & Error ID Extractor
```ti
tita lines_in = open input as lines
tita err_ids = lines_in
    | filter /ERROR/i
    | match_all /id=(\d+)/ $1
    | unique
    | sort "natural"

print `Found ${len(err_ids)} unique error IDs`
save join(err_ids, "\n") to "out/error_ids.txt" atomic backup
```

### Recipe 2: CSV Department Revenue Summary to JSON
```ti
tita sales = open "sales.csv" as csv
tita by_dept = sales | group_by(r => r.dept)
tita report = {}

each dept, items in by_dept {
    tita total = items | map(r => r.amount) | sum
    report[dept] = { count: len(items), total: total, avg: total / len(items) }
}

save to_json(report, true) to "out/revenue_summary.json" atomic
```

### Recipe 3: Dynamic Multi-File Code & Web Generator (HTML/CSS/JS)
```ti
tita out_dir = "dist/palette"
mkdir(out_dir)
tita colors = ["#C9B00B", "#E0D274", "#FAF7E8"]

tita css_vars = []
each i, hex in colors {
    add `  --shade-${pad_left(i + 1, 2, "0")}: ${hex};` to css_vars
}

tita css = `:root {\n${join(css_vars, "\n")}\n}\n`
save css to `${out_dir}/style.css` atomic
```

---

## Part IV: Complete Reference Tables

### CLI Flags (`titan run` / `titan ti`)
- `-c, --code <SCRIPT>`: Run inline script
- `-i, --input <FILE>`: Pre-bind `input` variable
- `--check`: Validate syntax & static `import` paths without executing code or writing files
- `-n, --dry-run`: Preview writes without modifying disk (`dry_run == true`)
- `-b, --backup`: Create collision-proof `.orig` backups (default on save)
- `--no-backup`: Disable `.orig` backup creation
- `--max-steps <N>`: Step limit (default `20,000,000`, max `1,000,000,000`)
- `--guide, --spec`: Print built-in `.ti` reference
- `-j, --json`: Structured JSON report
- `[script args...]`: Positional arguments after `<script.ti>` (or after `--`) are pre-bound to `args`

### Operator Precedence (Highest -> Lowest)
1. Member access / Optional Chaining / Indexing / Calls: `.`, `?.`, `[]`, `?[]`, `()`
2. Unary: `-`, `+`, `not`
3. Multiplicative: `*`, `/`, `%`
4. Additive: `+`, `-`
5. Pipe: `|`
6. Null-Coalescing: `??`
7. Pattern / String Checks & Comparisons: `~`, `!~`, `contains`, `starts_with`, `ends_with`, `<`, `<=`, `>`, `>=`, `==`, `!=`
8. Logical `and`, then Logical `or`
9. Ternary: `cond ? a : b` (right-associative)

### Built-In Standard Library Quick Index
- **Regex:** `match /re/ [$N]`, `match_all /re/ [$N]`, `regex_match(s, /re/)`, `filter /re/|"s"|fn`, `replace p with r`
- **Text/List:** `upper`, `lower`, `title`, `trim`, `ltrim`, `rtrim`, `lines`, `unique`, `unique_by(f)`, `count_by(f)`, `reverse`, `count`, `join`, `split`, `sort ["asc"|"desc"|"natural"]`, `sort_by(f [,"desc"])`, `take N`, `skip N`, `slice(s [,e])`, `insert(t, i, v)`, `prepend(t, v)`, `remove_at(xs, i)`, `pop(xs)`, `first`, `last`, `chunk(n)`, `flatten [d]`, `zip(other)`, `enumerate`, `index_of(x)`
- **Set Ops:** `union(a, b)`, `intersect(a, b)`, `difference(a, b)`
- **Higher-Order:** `map(f)`, `flat_map(f)`, `filter(f)`, `reduce(f [,init])`, `any([f])`, `all([f])`, `find(f)`, `find_index(f)`, `group_by(f)`
- **Stats/Types/JSON/CSV/MD:** `sum`, `mean`, `min`, `max` (list OR 2+ args: `min(a, b)`), `int`, `float`, `bool`, `str`, `len`, `type`, `to_json(v [,pretty])`, `from_json(s)`, `to_csv(rows [,hdrs])`, `from_csv(s [,has_hdr])`, `md_table(headers, rows)`
- **Maps:** `keys`, `values`, `items`, `from_entries(pairs)`, `pick(m, keys)`, `omit(m, keys)`, `merge`, `get(c, k [,def])`, `has(c, k)`, `without(m, k)`
- **Strings & Hashing (code-point safe):** `substr(s, start [,len])`, `repeat(s, n)`, `chars(s)`, `ord(s)`, `chr(n)`, `index_of(s, sub)`, `pad_left(s, w [,ch])`, `pad_right(s, w [,ch])`, `sha256(s)`, `base64_encode(s)`, `base64_decode(s)`
- **Date, Env & Automation:** `now()`, `timestamp()` (`"s"`, `"ms"`, `"us"`), `timestamp_us()`, `format_date(epoch [,fmt])`, `file_mtime(path)`, `env(name [,def])`, `stdin()`, `exit([code])`, `sleep(ms)`
- **Math & Range:** `abs`, `floor`, `ceil`, `round [d]`, `sqrt`, `pow(a,b)`, `clamp(x,lo,hi)`, `mod(a,b)`, `rand()`, `rand(min,max)`, `range(n)` / `range(s,e [,step])`
- **Paths & Built-in Engines:** `basename`, `dirname`, `extname`, `stem`, `join_path(...)`, `abs_path`, `exists`, `is_file`, `is_dir`, `file_size`, `list_dir`, `mkdir(p)`, `format`, `color`, `query`

### Modern Language Features (`v2.0.3` Additions)
- **Modularity & Save Prepend:** `import "lib/helpers.ti"` (relative resolution + cycle guard) and `save header to "file.txt" prepend atomic backup`.
- **Destructuring & Spread (`...`):** `tita [a, b, ...rest] = xs`, `tita {name, age: a, ...extra} = user`, `[...a, ...b]`, `{...defaults, ...overrides}`, and `fn_call(...args)`.
- **Default & Rest Parameters:** `fn greet(name, role = "dev", ...tags) { ... }`.
- **Optional Chaining & Null-Coalescing:** `user?.profile?.city ?? "Unknown"` and `post?.tags?[0] ?? "untagged"`.
- **Pattern Matching (`match` / `switch`):** `match status { 200 => print "OK", /^5/ => print "Err", _ => print "Other" }`.
- **Runtime Call Stack Traces:** Nested errors inside `fn` calls report full `Call stack:` frames (`at fn (file:line:col)`).

### Common Mistakes Checklist
| Wrong | Correct in `.ti` |
|---|---|
| `titan run --guids` | `titan run --guide` |
| `let x = 1` / `var x = 1` | `tita x = 1` |
| `else if cond { ... }` | `elif cond { ... }` |
| Expecting `catch err` to give string | Read `err.message` |
| Passing mutating `titan` bridge under `--dry-run` | Guard read-after-write with `if not dry_run` |

---

## Part V: Verbatim Built-in Reference (`titan run --guide`)

```text
TITAN (.ti) Language Self-Contained Reference (v2.0.3)
======================================================

1. Comments & Literals
   - Comments: // single line   |   /* multi-line block */
   - Types: null, true, false, Int64 (42, 0xFF, 0b101, 1_000), Double (3.14, 1e9), List [a, b], Map {"k": v}, Function
     List [...] and Map {...} literals may span multiple lines cleanly.
   - Strings: interpolated "..." (escapes: \n \t \r \\ \" \{ \} \xHH \uXXXX \u{1F600}) or raw '...' / r"..." (no escapes, no interpolation)
   - Interpolation inside "...": "{var}", "{obj.prop}", "{list[0]}", and capture groups "{$0}".."{$9}"
   - Multi-line strings: """line one
     line two {var}"""   (same escapes/interpolation as "...")   |   raw: r"""...""" (no processing)
   - Template literals (full expressions): `Total: ${a + b}, ${name | upper}, ${n > 1 ? "items" : "item"}`
     Backtick strings may span lines; escape with \` and \$ ; ${ } accepts ANY expression.
   - Indexing & Properties: list[0], map["key"], map.field, val.length, val.size

2. Variables, Destructuring & Lexical Scoping
   - Declare new variable in current block:  tita name = expr
   - Destructuring & spread:                 tita [a, b, ...rest] = xs  |  tita {name, age: a, ...rest} = user
                                             [...list_a, ...list_b]     |  {...defaults, ...overrides}
   - Reassign/mutate existing variable:      name = expr  |  += -= *= /= %=
   - Element/property assignment:            list[i] = x  |  map["k"] = x  |  a.b.c = x  |  xs[0].k += 1 (all nested & compound ops)
   - Value semantics:                        assignment copies Lists/Maps by value (use closures to share state);
                                             pop(xs) returns a NEW list without its last item (non-mutating).
   - Optional chaining & null-coalescing:    user?.address?.city ?? "Unknown"   |   post?.tags?[0] ?? "untagged"
   - Pre-bound built-in variables:           input (via -i), args (script CLI args List), dry_run (Bool)
   - Scoping is lexical: blocks, loop bodies and function bodies get their own scope; inner scopes see outer ones.

3. File I/O & Modularity
   - Open: open <path> [as text|lines|csv|json]   |   open stdin [as text|lines|csv|json]   |   stdin()
   - Save: save <val> to <path> [atomic] [backup] [append|prepend]   (no-op preview under --dry-run)
   - Import: import "helpers.ti"   (resolves relative to current script; cycle-guarded)

4. Regex & Comparisons (Linear-Time Thompson NFA / Pike VM)
   - Regex literal: /pattern/flags   flags: i (ignore-case), m (multiline), w (word)
     '/' inside a [...] character class needs no escape: /[^/]+/ ; division is chosen automatically after
     a value (x / 2, f(x) / 2, arr[0] / 2); a regex is expected after operators, '(', ',', '~', '=>', '?' ...
   - Counted quantifiers {m}, {m,}, {m,n} ARE supported (e.g. /#[0-9a-fA-F]{6}/).
   - Note: \1..\9 backreferences, lookarounds, and possessive ++/*+ are not supported
   - Operators: ~ /re/   !~ /re/   contains   starts_with   ends_with   == != < <= > >=   ??
   - Logic:     and   or   not  (and/or short-circuit left-to-right)   Ternary: cond ? a : b
   - Arithmetic: + - * / %  (% keeps the sign of the left operand; Int overflow and /0 are errors)
   - Captures:  $0..$9 updated by ~, !~, match /re/; use regex_match(s, /re/) for local {full, groups, start, end}

5. Control Flow & Statements
   - Loops:        each item in expr { ... break ... continue ... }
                   each i, item in list { ... }      (index + value)
                   each key, value in map { ... }    (single variable over a map iterates its keys)
                   while cond { ... }                (bounded by max_steps; break / continue work)
   - Conditionals: if cond { ... } elif cond { ... } else { ... }
   - Pattern Match: match status { 200 => print "OK", 404 => print "Not Found", _ => print "Other" }
   - Errors:       try { ... } catch err { ... }     err = {message, line, col, value}; 'catch' variable is optional
                   throw expr   |   error("msg")   |   assert(cond, "message")   |   exit(code)   |   sleep(ms)
                   Step-limit, output-limit, exit() and out-of-memory errors can NOT be caught.
   - Lists & Print: add expr to list_var   |   print expr
   - Replace expr: replace target pat with rep   (also usable in pipe: | replace pat with rep)

6. Functions, Lambdas & Closures
   - Declare:   fn add(a, b = 10, ...rest) { return a + b }  (supports defaults & trailing ...rest list)
   - Anonymous: tita sq = fn(x) { return x * x }        Arrow lambdas: x => x * x   |   (a, b) => a + b   |   () => 42
   - Call:      add(1, 2)   add(...args)   sq(5)   obj?.handler(3)   make_adder(1)(2)
   - Closures capture their defining scope by reference: counters, accumulators and callbacks work.
   - 'return' leaves the function (value optional); a top-level 'return' ends the script successfully.
   - Nested runtime errors include full Call stack traces with file:line:col.
   - In a pipe without parentheses a lambda body ends at the next '|':  xs | map x => x * 2 | sum
     Use parentheses for multi-argument lambdas:  xs | reduce((acc, x) => acc + x, 0)

7. Pipe Operations & Built-in Functions (expr | step [args...] or step(expr, ...))
   - Regex:     match /re/ [$N]   |   match_all /re/ [$N]   |   regex_match(/re/)   |   filter /re/ | "sub" | fn   |   replace p with r
   - Text/List: upper, lower, title, trim, ltrim, rtrim, lines, unique, unique_by(f), count_by(f), reverse, count, join [sep], split [delim]
   - Edit List/Str: insert(t, i, v), prepend(t, v), remove_at(xs, i), pop(xs), slice(start [, end]), take N, skip N
   - Order/Sets: sort ["asc"|"desc"|"natural"], sort_by(f [, "desc"]), union(a, b), intersect(a, b), difference(a, b),
                 first, last, chunk(n), flatten [depth], zip(other), enumerate, index_of(x)
   - Higher-order (callback receives item, and optionally index if it declares 2 parameters):
                  map(f), flat_map(f), filter(f), reduce(f [, init]), any([f]), all([f]), find(f), find_index(f),
                  group_by(f)  -> Map of key -> list.   A string names a built-in:  names | map "upper"
   - Stats/Types: sum, mean, min, max (accept list OR 2+ args: min(a, b)), int(v), float(v), bool(v), str(v), len(v), type(v), keys(map), has(c, k)
   - Maps:      values(m), items(m) -> [[k, v], ...], from_entries(pairs), pick(m, keys), omit(m, keys), merge(a, b), get(m, k [, def]), without(m, k)
   - Strings/Hash: starts_with(s, pre), ends_with(s, suf), contains(s, sub), substr(s, start [, len]), repeat(s, n),
                   chars(s), ord(s), chr(n), sha256(s), base64_encode(s), base64_decode(s)
   - Date/Env:  now(), timestamp() [ms; "s" for sec, "us" for micros], timestamp_us(), format_date(epoch, fmt), file_mtime(path), env(name [, default])
   - Math/Gen:  abs, floor, ceil, round [digits], sqrt, pow(a, b), clamp(x, lo, hi), mod(a, b), rand(), rand(min, max), range(...)
   - Padding:   pad_left(s, width [, ch]) | pad_right(s, width [, ch])  (Unicode-safe; element-wise on lists)
   - JSON/CSV/MD: to_json(v [, true=pretty]) | from_json(text) | to_csv(rows [, headers]) | from_csv(text [, has_header]) | md_table(headers, rows)
   - Paths (read-only): basename, dirname, extname, stem, join_path(a, b, ...), abs_path, exists, is_file, is_dir,
                file_size, list_dir (sorted names)
   - Filesystem writes: mkdir(path) -> Bool (creates parents; honors --dry-run and the protected-path lock)
   - Engines:   format ["minify"|"sort-keys"|lang], color ["hex"|"rgb"|"hsl"|"name"], query "EXPR"

8. Safe Tier-2 TITAN Bridge
   - Run any non-recursive command in-process: titan <subcommand> [args...]
   - Expands List variables automatically; skips mutating commands under --dry-run
   - Mutating bridged commands refuse protected system paths (same lock as 'save')
   - Blocked inside .ti scripts: mcp, lsp, run, ti

9. Safety Limits & Diagnostics
   - --max-steps N caps statements + loop iterations + function calls (default 20000000); max_output_bytes caps
     print output, strings and save payloads; parser nesting <= 256; list size <= 2000000; range <= 1000000.
   - Errors are reported as file:line:col with a fix hint, e.g. "Undefined variable 'nmae' (did you mean 'name'?)".
   - Sources are decoded from UTF-8 (BOM ok) or UTF-16; binary input is rejected.

10. Complete Examples
   tita rows = open input as lines | filter /ERROR/i
   tita ids = rows | match_all /id=(\d+)/ $1 | unique | sort "natural"
   print "Unique error IDs: {ids.length}"
   save ids to "error_ids.txt" atomic backup

   fn fact(n) { return n <= 1 ? 1 : n * fact(n - 1) }
   fn make_counter() { tita n = 0; fn inc() { n += 1; return n }; return inc }
   tita next = make_counter()
   next(); next()
   print `fact(10) = ${fact(10)}, counter = ${next()}`
   tita people = [{name: "Ann", age: 31}, {name: "Bob", age: 25}]
   print people | sort_by(p => p.age) | map(p => p.name) | join ", "
   each k, v in {a: 1, b: 2} { print "{k}={v}" }
   try { assert(len(people) > 5, "need more people") } catch err { print "caught: {err.message}" }
```
