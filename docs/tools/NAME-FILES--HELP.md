## 23. `titan name-files` — Windows Filename Inspection & Safe Batch-Renaming Engine

### Verbatim Help Manual
```text
Usage: titan name-files [OPTIONS] [--] <FILES or DIRECTORIES...>

Windows filename inspection and batch-rename engine.
Supports both query (read-only) and transform (renaming) modes.

Query modes (never modify disk):
  -upper, --upper-case, --uper-case        List files whose name is ALL UPPER CASE
  -lower, --lower-case                     List files whose name is all lower case
  -title, --title-case                     List files whose name is Title Case
  -extension, -externsion, --extract-extension
                                            List/extract file extensions
    --unique                                 With -extension: list distinct extensions only
    --count                                  With -extension: show counts per extension

Transform modes (combinable in one pass; applied in this order:
remove, case, add, rename/numbering, extension):
  -to-upper, --to-upper-case               Convert filename (stem) to UPPER CASE
  -to-lower, --to-lower-case                Convert filename (stem) to lower case
  -to-title, --to-title-case                Convert filename (stem) to Title Case
    --include-extension                      Also apply the case transform to the extension

  -add-to, --add-to-file-name              Insert text into the filename
    --text <text>                            Text to insert
    --place <prefix|suffix|position:N>       Where to insert it (default: suffix, N counts characters)

  -remove, --remove-from-file-name         Remove text from the filename
    --remove-text <text>                     Text (substring) to remove
    --first                                  Remove only the first occurrence
    --ignore-case                            Case-insensitive match while removing

  -numbering, --numbering-file-name        Add a sequence number to each filename
  -rename, --rename-file-name              Rename using a prefix/suffix/number template
    --prefix <text>                          Text placed before the name
    --suffix <text>                          Text placed after the name
    --number <digits>   (or -number-001)     Numbering start/padding template
    --start <digits>    (or -start-000)      Starting number/padding template
    --sep <text>        (or -sep-_)          Separator between parts (default: _)

  --char <text> (or -char-X) is accepted as a shorthand for --text, --remove-text or --sep
  when exactly one of -add-to, -remove or -rename/-numbering needs it.

  -extension-change, -extention-change, --change-extention-type, --change-extension-type
                                            Change file extensions
    --ext <*.ext>                            Only affect files with this current extension
    --to-ext <*.ext>                         New extension to apply

Safety & scope:
  --yes                       Required to actually rename (otherwise a preview is shown)
  --dry-run                   Preview planned renames and exit with 0
  --recursive                 Include files in subdirectories
  --include-dirs              Also include directories as renameable entries
  --force                     Allow overwriting an existing regular file at the target name
  --stop-on-error             Abort the batch on the first rename failure
  --rollback                  Abort on the first failure and undo renames already done
  --undo-log <file>           Append every performed rename to <file>
  --undo <file>               Revert the renames recorded in an undo log (needs --yes)
  --allow-system              Allow operating inside protected system locations
  --quiet                     Suppress per-file output
  --json                      Structured JSON output for AI agents

Exit codes: 0 ok, 2 error, 3 preview only (nothing applied), 4 completed with skipped conflicts.

Notes:
  * Nothing is renamed until every planned name is validated: collisions within the
    batch and with existing files on disk are detected and skipped before any rename.
  * Directory arguments are scopes; they are renamed only with --include-dirs and
    never when given as '.', '..' or a drive root. Children are renamed before parents.
  * Filenames are sanitized for Windows (reserved characters, device names, trailing
    dots/spaces, 255 UTF-16 unit limit). Text options reject control characters and
    text-direction overrides.
  * File CONTENT is never read or modified; only filenames are changed.
```

### Practical Examples
```powershell
# 1. List all files whose stem is uppercase in the current folder (supports Windows globs)
titan name-files -upper .
titan name-files -upper *.txt

# 2. Extract unique file extensions and their occurrence counts
titan name-files -extension --count .

# 3. Preview converting all filenames to lowercase (dry run)
titan name-files -to-lower --dry-run .

# 4. Apply converting filenames to lowercase with confirmation
titan name-files -to-lower --yes .

# 5. Batch add prefix "backup_" to all files with undo log
titan name-files -add-to --text "backup_" --place prefix --undo-log renames.log --yes .

# 6. Revert all renames recorded in the undo log
titan name-files --undo renames.log --yes

# 7. Add zero-padded sequential numbers starting from 001 with custom separator
titan name-files -rename --prefix "doc" --number 001 --sep "-" --yes .

# 8. Change all .jpeg extensions to .jpg safely with rollback on error
titan name-files -extension-change --ext "*.jpeg" --to-ext ".jpg" --rollback --yes .
```
