## 47. `titan reg` — Native Win32 Windows Registry Inspector, Diff & Exporter (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan reg <SUBCOMMAND> <KEY_PATH> [ARGS...] [OPTIONS]

Read-only native Win32 Windows Registry inspector, diff & .reg exporter.
All options strictly require double dashes (--). Single-dash flags are rejected.

Subcommands:
  query <KEY>                    Inspect registry key values (default)
  keys <KEY>                     List subkeys under KEY
  tree <KEY>                     Render indented registry subkey & value hierarchy
  search <KEY> <PATTERN>         Search subkey/value names and string data
  export <KEY> --output <FILE>   Export key/values to standard .reg v5.00 format
  diff <KEY1> <KEY2>             Compare values between two registry keys

Supported Root Hives:
  HKCU (HKEY_CURRENT_USER), HKLM (HKEY_LOCAL_MACHINE),
  HKCR (HKEY_CLASSES_ROOT), HKU (HKEY_USERS), HKCC (HKEY_CURRENT_CONFIG)

Options (double-dash ONLY):
  --value <NAME>                 Read a single named value
  --type <KIND>                  Filter by type (SZ, EXPAND_SZ, DWORD, QWORD, BINARY, MULTI_SZ)
  --wow64 <32|64>                Access 32-bit or 64-bit registry view
  --expand                       Expand environment variables in REG_EXPAND_SZ
  --recursive                    Recurse into subkeys
  --depth <N>                    Max recursion depth (1..32, default: 8)
  --limit <N>                    Max returned entries (1..50000, default: 2000)
  --ignore-case                  Case-insensitive search
  --output <FILE>                Write output or .reg export atomically to file
  --json                         Emit structured TITAN JSON envelope
  --help                         Show this help
```

### Examples
```powershell
titan reg query 'HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion' --value ProductName --json
titan reg export 'HKCU\Environment' --output env_backup.reg
```
