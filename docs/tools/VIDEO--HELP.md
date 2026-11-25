## 18. `titan video` — Video Metadata, Frame, Contact-Sheet & WAV Extractor

### Verbatim Help Manual
```text
Usage: titan video [OPTIONS] [--] <FILE|DIR...>
       titan video --input <FILE> [--out-dir DIR | --contact-sheet IMG | --extract-audio WAV] [OPTIONS]
       titan video --strip-metadata --input <FILE> (--output <FILE> | --in-place) [OPTIONS]

Native video metadata inspector, lossless metadata stripper & Media Foundation / GDI+ frame extractor.

Metadata Options:
  -r, --recursive        Recursively scan directories for video files (.mp4, .mkv, .webm, .mov, .avi, .m4v)
  --hash, --sha256       Include SHA-256 and MD5 cryptographic hashes
  -j, --json             Output structured JSON metadata

Lossless Metadata Stripping Options (MP4/MOV/M4V, MKV/WebM, AVI — double-dash '--' ONLY):
  --strip-metadata       Strip identifying metadata losslessly without re-encoding
  --clean-metadata       Alias for --strip-metadata
  --input <FILE>         Input video file
  --output <FILE>        Write cleaned video atomically to destination file
  --in-place             Strip in-place with collision-proof .orig backup by default
  --no-backup            Skip .orig backup when using --in-place
  --keep-timestamps      Preserve container creation/modification timestamps
  --overwrite            Overwrite existing destination file
  --dry-run              Analyze and report without modifying disk
  --quiet                Suppress normal text output
  -j, --json             Emit structured JSON telemetry (bytes removed, stripped items, backup, SHA-256)

Frame & Audio Extraction Options (double-dash '--' ONLY):
  --input <FILE>         Input video file
  --out-dir <DIR>        Directory for extracted video frames
  --contact-sheet <IMG>  Render extracted frames into a composite grid image
  --grid <COLSxROWS>     Contact sheet grid layout (default: 4x3)
  --timestamps           Draw timestamp labels onto contact sheet tiles
  --scene-threshold <F>  Extract frames only on visual scene change (0.01..1.0)
  --at <T1,T2,...>       Exact timestamp(s) (500ms, 1.5s, 00:01:02.500)
  --every <TIME>         Extract 1 frame every interval
  --from <TIME>          Start timestamp window
  --to <TIME>            End timestamp window
  --count <N>            Max or evenly-spaced frame count (1..10000)
  --format <FMT>         Image format: png (def), jpg, bmp, tiff, gif
  --quality <1-100>      JPEG quality (default: 90)
  --max-width <PX>       Proportional downscale max width
  --max-height <PX>      Proportional downscale max height
  --rotate <DEG>         Rotate frames clockwise (0, 90, 180, 270)
  --flip <MODE>          Flip frames (none, h, v, hv)
  --grayscale            Convert frames to grayscale
  --extract-audio <WAV>  Extract video audio stream as 16-bit PCM WAV
  --prefix <STR>         Output frame filename prefix (default: frame)
  --output <FILE>        Write report text or JSON to file
  --probe                Inspect Media Foundation stream dimensions/FPS/duration
  --overwrite            Overwrite existing destination files
  --dry-run              Plan without writing output files
  --quiet                Suppress normal text output
```

### Practical Examples
```powershell
# 1. Inspect a video file's codecs, resolution, FPS, audio stream, and duration
titan video movie.mp4

# 2. Scan an entire media directory recursively and emit JSON with SHA-256 hashes
titan video D:\Videos -r --hash --json

# 3. Generate a 4x3 contact sheet with timestamp badges
titan video --input clip.mp4 --contact-sheet sheet.png --grid 4x3 --timestamps --json

# 4. Extract keyframes on scene changes with 90-degree rotation and grayscale
titan video --input clip.mp4 --out-dir .\frames --scene-threshold 0.15 --rotate 90 --grayscale

# 5. Extract video audio track as uncompressed PCM WAV
titan video --input clip.mp4 --extract-audio soundtrack.wav --json

# 6. Losslessly strip identifying metadata (udta/meta/ilst/XMP/timestamps) into a clean copy
titan video --strip-metadata --input raw.mp4 --output clean.mp4 --overwrite --json

# 7. Strip MKV/WebM or AVI metadata in-place with automatic collision-proof .orig backup
titan video --clean-metadata --input recording.mkv --in-place --json
```
