## 35. `titan copy` — Verified, Filter-Aware File & Directory Copy Engine

### Verbatim Help Manual
```text
Usage: titan copy [OPTIONS] <SRC...> <DEST>

Traversal & Filtering:
  -r/--recursive, --max-depth <N>, -g/--glob <pat>, --ext <e1,e2,...>, --exclude-ext <e1,e2,...>,
  --exclude <p1,p2,...>, --respect-gitignore, --text-files, --image-files, --audio-files,
  --video-files, --dev-files, --config-files, --archive-files, --min-size <SIZE>,
  --max-size <SIZE>, --recent <N[m|h|d]>, --hidden, --empty-dirs

Conflict, Safety & Integrity:
  --overwrite, --skip-existing, -u/--newer-only, --size-diff, -b/--backup,
  --verify, --atomic, --flatten, --create-dirs, -n/--dry-run, -q/--quiet, -v/--verbose, -j/--json
```
