## 43. `titan git` — Zero-Dependency Native `.git` Repository Inspector (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan git [SUBCOMMAND] [ARGS...] [OPTIONS]

Zero-dependency native .git repository inspection engine (no libgit2, no git.exe).
All options strictly require double dashes (--). Single-dash flags are rejected.

Subcommands:
  info [DIR]                    Repository root, .git path, HEAD, counts & dirty summary (default)
  status [DIR]                  Working-tree vs .git/index status (modified, deleted, staged, untracked)
  branches [DIR]                Local (and remote with --all) branches from refs & packed-refs
  tags [DIR]                    Annotated and lightweight tags from refs/tags & packed-refs
  log [DIR]                     Commit history via native object parent walking or .git/logs/HEAD
  show <REV> [DIR]              Decode loose/packed commit, tag, tree, or blob object
  files [DIR]                   Decode tracked entries from .git/index (v2/v3/v4)
  remotes [DIR]                 Parse .git/config remotes (fetch/push URLs) & branch tracking
  rev-parse <REF> [DIR]         Resolve HEAD, branch, tag, or abbreviated OID to 40-char SHA-1
  diff [REV1 [REV2]] [OPTIONS]  Native Myers O(ND) unified diff (worktree, --staged, or commit-to-commit)
  blame <PATH> [OPTIONS]        Native line-by-line commit provenance tracking via object history
  grep <PATTERN> [OPTIONS]      Search tracked tree blobs at any revision (literal or --regex)
  cat <REV:PATH|PATH> [OPTIONS] Print any historical blob from a commit tree (or :PATH from index)
  reflog [DIR] [OPTIONS]        Inspect .git/logs/HEAD (or --ref <REF>) reflog entries
  stash [DIR] [OPTIONS]         List stashed entries from .git/logs/refs/stash & refs/stash

Options (double-dash ONLY):
  --dir <PATH>                  Repository directory (default: current directory)
  --limit <N>                   Limit output entries (default: 20 for log/reflog/stash, 200 for files/grep)
  --oneline                     Compact one-line commit format for log
  --all                         Include remote branches / walk all refs
  --untracked                   Include untracked working-tree files in status
  --grep <PAT>                  Filter log commits by message substring (case-insensitive)
  --author <PAT>                Filter log commits by author name/email (case-insensitive)
  --filter <GLOB>               Filter tracked file paths by glob pattern (*, ?)
  --stat                        Show per-commit or per-file diff statistics
  --staged, --cached            In diff: compare .git/index against HEAD
  --name-only                   In diff: print only changed file paths
  --path <PATH|GLOB>            Restrict diff/grep to matching path or glob
  --rev <REV>                   Target revision for blame, grep, or cat (default: HEAD)
  --ref <REF>                   Target ref for reflog (default: HEAD)
  --lines <START:END>           1-based line range for blame (e.g. 10:40)
  --context <N>                 Context lines around diff hunks (default: 3)
  --ignore-case                 Case-insensitive matching in grep
  --regex                       Linear-time Thompson NFA regex matching in grep
  --json                        Emit structured JSON envelope
  --output <FILE>               Write primary output (text or JSON) to a file
  --no-color                    Disable ANSI terminal colors
  --help                        Show this help message and exit
```

### Examples
```powershell
titan git info --dir G:\MyRepo --json
titan git diff HEAD~1 HEAD --stat --dir G:\MyRepo
titan git blame src/main.cpp --lines 1:40 --dir G:\MyRepo --json
titan git grep "timeout" --rev HEAD --regex --dir G:\MyRepo
titan git cat HEAD~1:README.md --dir G:\MyRepo
titan git reflog --limit 10 --dir G:\MyRepo --json
```
