## 45. `titan ftp` — Native RFC 959/2428/3659 FTP & WinINet FTPS Client (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan ftp <SUBCOMMAND> [ARGS...] [OPTIONS]

Native C++20 / Win32 RFC 959/2428/3659 FTP & WinINet FTPS client engine.
All options strictly require double dashes (--). Single-dash flags are rejected.

Subcommands:
  ls [URL|REMOTE_DIR]            List remote entries (MLSD with Unix/DOS LIST fallback)
  stat [URL|REMOTE_PATH]         Inspect remote server SYST/FEAT/PWD/SIZE/MDTM metadata
  get <URL|REMOTE> [LOCAL]       Download file (or directory with --recursive) atomically
  put <LOCAL> <URL|REMOTE>       Upload file (or directory with --recursive)
  cat <URL|REMOTE_FILE>          Stream remote file content directly to stdout
  mkdir <URL|REMOTE_DIR>         Create remote directory (or chain with --parents)
  rm <URL|REMOTE_FILE>           Delete remote file (or tree with --recursive)
  rmdir <URL|REMOTE_DIR>         Remove remote directory (or tree with --recursive)
  mv <SRC_URL_OR_PATH> <DST>     Server-side rename/move via RNFR + RNTO
  sync <SRC> <DST>               Mirror sync between local folder and FTP path
  raw <URL|CMD> [CMD]            Send raw FTP control command (e.g. NOOP, STAT)

Connection & Security Options (double-dash ONLY):
  --host <HOST>                  FTP server hostname/IP (if not passed in URL)
  --port <PORT>                  Server port (default: 21 for FTP, 990 for FTPS)
  --user <NAME>                  Username (default: anonymous)
  --pass <PASSWORD>              Password (default: titan@localhost)
  --tls                          Use TLS encrypted FTPS transport (WinINet)
  --insecure                     Allow self-signed/expired TLS certificates
  --passive                      Use passive mode EPSV/PASV (default)
  --active                       Use active mode PORT listener
  --ascii                        Use ASCII transfer mode TYPE A (default: binary TYPE I)
  --timeout <MS>                 Socket/transfer timeout in ms (default: 15000)
  --retry <N>                    Retry transient connection failures (default: 1)
  --retry-delay <MS>             Delay between retries in ms (default: 250)

Transfer & Output Options:
  --recursive                    Recursively list, download, upload, or delete
  --parents                      Create missing parent directories in mkdir/put
  --resume                       Resume partial downloads/uploads via REST offset
  --overwrite                    Overwrite existing destination files unconditionally
  --delete                       Delete extraneous target files during sync
  --direction <auto|up|down>     Override sync transfer direction
  --glob <PAT>                   Filter remote filenames by glob pattern
  --long                         Detailed table view for ls
  --verify                       Compute and verify SHA-256 checksum on downloads
  --max-bytes <N>                Max bytes for cat output (default: 67108864)
  --dry-run                      Preview get/put/rm/rmdir/mv/sync without writing
  --verbose                      Print FTP control trace to stderr
  --output <FILE>                Write text or JSON output atomically to file
  --json                         Emit structured TITAN JSON envelope
  --no-color                     Disable ANSI output styling
  --help                         Show this help message and exit
```

### Examples
```powershell
titan ftp ls ftp://user:pass@example.com/public --recursive --json
titan ftp sync ./dist ftp://user:pass@example.com/www --dry-run
```
