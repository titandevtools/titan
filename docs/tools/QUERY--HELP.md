## 27. `titan query` — Structured Path/Filter Query & Mutation Engine

### Verbatim Help Manual
```text
Usage: titan query [OPTIONS] EXPR [FILE]
       titan query [OPTIONS] --set PATH=VAL [--del PATH] FILE

Structured query and surgical mutation across JSON, JSONC, YAML, TOML, XML, INI.
Preserves 64-bit integer precision without float truncation.

Options:
  --set <PATH>=<VAL>   Set or create field/element value (repeatable)
  --del <PATH>         Delete field or array index (repeatable)
  --raw-str            Treat --set value literally as a string
  --format, -f <FMT>   Format override (json, jsonc, yaml, toml, xml, ini)
  -r, --raw-output     Emit strings without quotes
  -i, --in-place       Write mutations back to source file atomically
  -b, --backup         Create collision-proof backup before overwriting
  -n, --dry-run        Preview unified diff without writing
  -o, --output <FILE>  Write serialized document to output file
  -j, --json           Output uniform JSON envelope
```

### Practical Examples
```powershell
titan query ".items[] | select(.active == true) | .id" config.json -j
titan query --set ".server.port=9090" --del ".debug" -i -b config.yaml -j
```
