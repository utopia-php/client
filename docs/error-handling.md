# Error Handling

Both adapters throw PSR-18 exceptions. HTTP `4xx` and `5xx` responses are returned, not thrown, as required by PSR-18 — catch only transport-level failures here.

```php
<?php

use Psr\Http\Client\ClientExceptionInterface;
use Psr\Http\Client\NetworkExceptionInterface;
use Psr\Http\Client\RequestExceptionInterface;
use Utopia\Client\Exception\AdapterPreconditionException;
use Utopia\Client\Exception\ConnectionException;
use Utopia\Client\Exception\DnsException;
use Utopia\Client\Exception\InvalidResponseException;
use Utopia\Client\Exception\InvalidUriException;
use Utopia\Client\Exception\ProtocolException;
use Utopia\Client\Exception\ProxyException;
use Utopia\Client\Exception\TlsException;
use Utopia\Client\Exception\TimeoutException;

try {
    $response = $client->sendRequest($request);
} catch (TimeoutException $error) {
    // Transport timeout.
} catch (DnsException $error) {
    // DNS resolution failure.
} catch (TlsException $error) {
    // TLS handshake or certificate failure.
} catch (ProxyException $error) {
    // Proxy transport failure.
} catch (ProtocolException $error) {
    // HTTP protocol transport failure.
} catch (ConnectionException $error) {
    // Connection refused, reset, unreachable, or broken.
} catch (InvalidResponseException $error) {
    // Malformed or invalid HTTP response.
} catch (InvalidUriException | AdapterPreconditionException $error) {
    // Request or runtime precondition failure.
} catch (NetworkExceptionInterface $error) {
    // DNS, connection, timeout, or transport failure.
} catch (RequestExceptionInterface $error) {
    // Invalid request or invalid response.
} catch (ClientExceptionInterface $error) {
    // Any other PSR-18 client error.
}
```
