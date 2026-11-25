## 25. `titan archive` — Native Universal Archive Suite (`ZIP/ZIP64`, `TAR`, `GZIP`, `TAR.GZ`, `ZSTD`, `TAR.ZST`, `7Z`, `RAR4`, `RAR5`)

### Verbatim Help Manual
```text
TITAN Archive Engine -- High-Speed Native C++ Multi-Format Archive Suite

USAGE:
  titan archive [COMMAND] [OPTIONS] <ARCHIVE> [FILES...]

COMMANDS:
  list, -l, ls          List contents and metadata of an archive
  extract, -x           Extract archive files to destination
  create, -c            Create a new archive (ZIP/ZIP64, TAR, GZIP, TAR.GZ, ZST, TAR.ZST)
  test, -t, verify      Verify archive integrity and block CRC-32
  detect, -d            Detect archive format and magic signature
  caps, --capabilities  Display format capability registry

OPTIONS:
  -o, --output <DIR>    Extraction output destination directory (default: .)
  -l, --level <0-9>     Compression level (0=Stored, 1=Fast, 6=Default, 9=Max)
  -f, --format <FMT>    Force format (zip, tar, gzip, targz, zst, tarzst, 7z, rar, rar5)
  --zip64               Write ZIP64 extended headers even for small archives
  --no-overwrite        Skip extracting files that already exist on disk
  --dry-run             Preview extraction/creation without writing to disk
  -j, --json            Output full structured JSON results
  -q, --quiet           Suppress non-essential progress output
```

### Practical Examples
```powershell
# 1. Create a Zstandard-compressed TAR.ZST archive or ZIP64 archive
titan archive create build/backup.tar.zst src/ include/ -j
titan archive create build/bundle.zip --zip64 src/ -j

# 2. List archive entries in structured JSON
titan archive list build/backup.tar.zst -j

# 3. Verify archive CRC-32 / XXH64 / LZMA2 integrity without extracting
titan archive test build/bundle.7z -j

# 4. Safely extract into target directory without overwriting existing files
titan archive extract build/backup.tar.zst -o extracted/ --no-overwrite -j

# 5. Inspect archive format and display capability matrix
titan archive detect mystery.bin -j
titan archive caps
```
