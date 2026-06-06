# Streaming Responses

`streamRequest()` delivers the response body to a sink callback chunk-by-chunk as
it arrives, so large downloads, Server-Sent Events, and LLM token streams are
consumed with bounded memory — the whole body is never held at once. It returns a
response carrying the status and headers; the body is empty because the body was
handed to the sink. Both adapters support it.

```php
<?php

$response = $client->streamRequest($request, function (string $chunk): void {
    echo $chunk;
});

echo $response->getStatusCode();
```

The sink runs as each chunk arrives, which means it also applies backpressure: the
transfer does not read ahead while the sink is still working. To stop early, throw
from the sink.

```php
<?php

// Parse a line-delimited (NDJSON / SSE) stream as it streams in.
$buffer = '';

$client->streamRequest($request, function (string $chunk) use (&$buffer): void {
    $buffer .= $chunk;

    while (($newline = strpos($buffer, "\n")) !== false) {
        $line = substr($buffer, 0, $newline);
        $buffer = substr($buffer, $newline + 1);
        // handle $line
    }
});
```

Notes:

- Use `sendRequest()` for normal requests — it buffers the body and returns a
  fully decodable response (`->json()`, `->form()`, `->multipart()`).
- `streamRequest()` returns only once the stream ends. For an unbounded stream
  (e.g. SSE), set the transport timeout to no-limit (`CURLOPT_TIMEOUT_MS => 0` on
  cURL, `timeout => -1` on Swoole) and stop by throwing from the sink.
- The Swoole adapter must run inside a coroutine, like `sendRequest()`.
