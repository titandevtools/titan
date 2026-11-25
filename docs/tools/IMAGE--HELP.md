## 17. `titan image` — Universal Image Metadata Extractor & Multi-Format Converter (27+ Formats)

### Verbatim Help Manual
```text
Usage:
  1. Extract Image Metadata:
     titan image [info|metadata] <file_or_dir...> [-r] [--hash] [-j]

  2. Convert Single Image or Batch Folder:
     titan image convert <input_file> <output_file> [-q <1-100>] [--resize <WxH>] [-j]
     titan image convert <file_or_dir> --to <FORMAT> [--from <FORMAT>] [-o <out_dir>] [-r] [-q <1-100>]
     titan image convert "JPG -> PNG" <folder_or_file> [-r] [-q <1-100>]

Options:
  --from <FMT>       Source image format filter for folder batch conversion (e.g. JPG, PNG, WEBP)
  --to <FMT>         Target image format (e.g. PNG, WEBP, AVIF, ICO, PDF, PSD, QOI, TGA, SVG)
  -o, --output <P>   Output file path or output directory for batch conversion
  -q, --quality <N>  Compression quality 1-100 for lossy encoders (default: 92)
  --resize <WxH>     High-quality bicubic resize during conversion (e.g. 1920x1080, 512x512)
  -r, --recursive    Process folders recursively
  --hash, --sha256   Compute SHA-256 and MD5 cryptographic hashes during metadata extraction
  -j, --json         Emit structured JSON output for AI Agents
```

### Practical Examples
```powershell
# 1. Extract complete metadata, EXIF tags, dimensions, DPI & SHA-256/MD5 hashes
titan image info sample.jpg --hash

# 2. Extract metadata for all images in a folder in structured JSON
titan image info .\assets -r --json

# 3. Convert a single JPG to PNG, QOI, PSD, ICO, or PDF
titan image convert photo.jpg photo.png
titan image convert photo.jpg photo.qoi
titan image convert photo.jpg document.pdf

# 4. Batch-convert all JPG images in the current folder to WEBP or PNG (Arrow Syntax!)
titan image convert "JPG -> WEBP" .\photos -q 90
titan image convert "PNG -> ICO" .\icons --resize 256x256

# 5. Batch-convert a folder using --from and --to flags into an output directory
titan image convert .\images --from PNG --to AVIF -o .\converted -j
```
