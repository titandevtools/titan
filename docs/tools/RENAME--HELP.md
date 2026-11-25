## 37. `titan rename` — Collision-Safe Composable Batch Renaming Engine

### Verbatim Help Manual
```text
Usage: titan rename [OPTIONS] <TARGET...>

Transform Operations:
  --replace <PAT> <REP>, -E/--regex, --case <upper|lower|title|snake|kebab|camel>,
  --include-ext, --prefix <TEXT>, --suffix <TEXT>, --remove <TEXT>,
  --strip-spaces, --normalize-spaces, --ext <NEW_EXT>,
  --number/--numbering, --start <N>, --pad <WIDTH>, --step <N>, --format <FMT>,
  --template <PATTERN> ({stem}, {ext}, {num}, {parent}, {date}, {mtime}, {size}),
  --stem-only, --include-dirs

Scope, Ordering & Safety:
  -r/--recursive, --max-depth <N>, -g/--glob <pattern>, --exclude <p1,p2,...>,
  --sort <name|modified|size>, --undo/--rollback, --journal <PATH>,
  -n/--dry-run, --force, -q/--quiet, -v/--verbose, -j/--json
```
