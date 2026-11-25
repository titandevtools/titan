## 44. `titan http` — Advanced Native Windows WinHTTP Client (`--` ONLY)

### Verbatim Help Manual
```text
TITAN HTTP/HTTPS Client Engine (WinHTTP)

Usage:
  titan http [OPTIONS] <URL>
  titan http <GET|POST|PUT|PATCH|DELETE|HEAD|OPTIONS> <URL> [OPTIONS]

Native Windows WinHTTP engine with zero external dependencies.
All options strictly require double-dash (--) syntax.

Request Construction:
  --method <VERB>            HTTP method (default: GET, or POST with payload)
  --query <K=V>              Append URL-encoded query parameter (repeatable)
  --header <K: V>            Add custom request header (repeatable)
  --user-agent <UA>          Override User-Agent header
  --bearer <TOKEN>           Set Authorization: Bearer <TOKEN>
  --basic <USER:PASS>        Set Authorization: Basic (Base64 encoded)
  --cookie <K=V; ...>        Attach Cookie header pairs (repeatable)
  --cookie-jar <FILE>        Load matching cookies and persist Set-Cookie headers

Payloads & Multipart Uploads:
  --data <BODY>              Raw request body string
  --data-json <JSON>         JSON body (auto-adds Content-Type: application/json)
  --data-file <PATH>         Read raw request body from file
  --form <K=V | K=@FILE>     Build multipart/form-data payload (repeatable)

Transport, TLS, Retries & Proxy:
  --timeout <MS>             Send/receive timeout in ms (default: 15000)
  --connect-timeout <MS>     Connect timeout in ms (default: same as --timeout)
  --max-bytes <N>            Max response body bytes, e.g. 32MB (default: 32 MB)
  --no-redirects             Disable following HTTP 3xx redirects
  --max-redirects <N>        Maximum redirect hops (default: 10)
  --retry <N>                Retry count on transient transport/5xx/429 errors
  --retry-delay <MS>         Delay between retries in ms (default: 500)
  --proxy <URL>              HTTP proxy URL (e.g. http://[user:pass@]host:port)
  --insecure                 Skip TLS certificate validation (self-signed/expired)
  --http2                    Enable HTTP/2 protocol negotiation
  --fail                     Return exit code 1 on HTTP 4xx/5xx responses

Output & Telemetry:
  --include                  Print response status & headers before body
  --headers-only             Print only response status & headers
  --output <FILE>            Write response body atomically to file
  --verbose                  Print detailed request/response telemetry to stderr
  --no-color                 Disable ANSI terminal colors
  --json                     Emit structured TITAN JSON envelope
  --help                     Show this help message
```

### Examples
```powershell
titan http https://httpbin.org/get --include --json
titan http POST https://httpbin.org/post --data-json '{"project":"TITAN"}' --fail
```
