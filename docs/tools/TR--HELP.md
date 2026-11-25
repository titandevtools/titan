## 15. `titan tr` — High-Speed L1-Table Character Translation, Squeeze & Delete

### Synopsis & Options
```text
Usage: titan tr [OPTIONS] SET1 [SET2] [FILE]

Options:
  -d                 Delete characters in SET1
  -s                 Squeeze multiple sequential occurrences of characters
  -c, -C             Complement SET1 (use all characters NOT in SET1)

Supports character ranges: 'a-z', 'A-Z', '0-9' and POSIX classes '[:lower:]', '[:upper:]', '[:digit:]', '[:space:]'
```
