## 19. `titan mp3 | titan audio` — Audio Metadata, Lyrics, Cover-Art & PCM WAV Extractor

### Verbatim Help Manual
```text
Usage: titan mp3 [OPTIONS] [--] <FILE|DIR...>
       titan audio [OPTIONS] [--] <FILE|DIR...>
       titan audio --input <PATH> [--covers DIR] [--wav FILE] [OPTIONS]

Native MP3 & audio metadata, lyrics, cover-art & PCM WAV extractor (MP3, FLAC, WAV, OGG/OPUS, M4A/AAC)

Metadata Options:
  -r, --recursive    Recursively scan directories for audio files (.mp3, .flac, .wav, .ogg, .m4a)
  --hash, --sha256   Include SHA-256 and MD5 cryptographic hashes
  -j, --json         Output structured JSON metadata

Audio Extraction Options (double-dash '--' ONLY):
  --input <PATH>     Input audio file or folder
  --recursive        Recursively scan folders
  --covers <DIR>     Extract embedded APIC/covr/FLAC/OGG album artwork to DIR
  --wav <FILE>       Decode audio stream via Media Foundation to 16-bit PCM WAV
  --from <TIME>      Timeline start timestamp for WAV/LRC slicing (500ms, 2.5s, 00:01:02)
  --to <TIME>        Timeline end timestamp for WAV/LRC slicing
  --format <FMT>     Export format: txt (def), md, csv, lrc, json
  --output <FILE>    Write extracted report/lyrics atomically to FILE
  --overwrite        Overwrite existing destination files
  --dry-run          Preview operations without writing files to disk
  --quiet            Suppress normal console output
```

### Practical Examples
```powershell
# 1. Extract complete MP3 stream parameters, ID3v2 tags, and cover art info
titan mp3 song.mp3 --hash

# 2. Scan a music library folder recursively and output JSON metadata
titan mp3 D:\Music -r --json

# 3. Extract embedded album artwork & full tag/lyrics report as JSON
titan audio --input song.mp3 --covers .\artwork --format json

# 4. Export embedded lyrics as .lrc or slice a timeline segment to PCM WAV
titan mp3 --input song.mp3 --format lrc --output song.lrc
titan audio --input track.m4a --from 1.5s --to 15s --wav clip.wav --json
```
