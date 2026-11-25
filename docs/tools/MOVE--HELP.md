## 36. `titan move` — Crash-Safe File & Directory Move Engine

### Verbatim Help Manual
```text
Usage: titan move [OPTIONS] <SRC...> <DEST>

Traversal & Filtering:
  -r/--recursive, --max-depth <N>, -g/--glob <pat>, --ext <e1,e2,...>, --exclude-ext <e1,e2,...>,
  --exclude <p1,p2,...>, --respect-gitignore, --text-files, --image-files, --audio-files,
  --video-files, --dev-files, --config-files, --archive-files, --min-size <SIZE>,
  --max-size <SIZE>, --recent <N[m|h|d]>, --older-than <N[m|h|d]>, --hidden, --prune-empty-dirs

Safety, Conflict & Integrity:
  --verify, --overwrite/--force, --skip-existing, -u/--newer-only, -b/--backup,
  --flatten, --create-dirs, --protected-guard, -n/--dry-run, -q/--quiet, -v/--verbose, -j/--json
```
