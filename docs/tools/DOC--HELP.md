## 46. `titan doc` — Native Office, EPUB, RTF & PDF Document Extractor (`--` ONLY)

### Verbatim Help Manual
```text
Usage: titan doc [OPTIONS] [--] <DOCUMENT_PATH>

Native zero-dependency document extractor across DOCX, XLSX, PPTX,
ODT, ODS, ODP, EPUB, RTF, and PDF.
All options strictly require double dashes (--). Single-dash flags are rejected.

Options:
  --info                       Show structural summary & metadata only
  --meta                       Extract document metadata dictionary only
  --format <text|md|csv|json>  Output rendering format (default: text)
  --sheet <NAME|INDEX>         Select XLSX/ODS worksheet by name or 1-based index
  --all-sheets                 Extract every XLSX/ODS worksheet
  --slide <N|START:END>        Select PPTX/ODP slide range (1-based)
  --page <N|START:END>         Select PDF page range (1-based)
  --notes                      Include PPTX speaker notes
  --headers                    Include DOCX headers, footers, footnotes & comments
  --search <PATTERN>           Filter/search paragraphs, cells, slides, or pages
  --ignore-case                Case-insensitive --search matching
  --limit <N>                  Limit extracted paragraphs/rows/matches/pages
  --output <FILE>              Write extracted output atomically to file
  --json                       Emit structured TITAN JSON envelope
  --no-color                   Disable ANSI terminal styling
  --help                       Show this help message and exit
```

### Examples
```powershell
titan doc report.docx --format md --headers
titan doc book.pdf --page 1:5 --search 'architecture' --ignore-case --json
```
