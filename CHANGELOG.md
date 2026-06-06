# Changelog

All notable changes to this project will be documented in this file.

This project follows semantic versioning.

## [Unreleased]

### Added

- Initial PSR-18 HTTP client wrapper: `Utopia\Client`.
- Immutable client defaults for headers, base URI, basic auth, and bearer auth.
- cURL adapter for regular PHP runtimes.
- Swoole coroutine adapter for coroutine runtimes.
- PSR-7 message implementations and PSR-17 factories under `Utopia\Psr7`.
- Request factories for JSON, XML, plain-text, form-encoded, query-string, raw-body, and multipart requests.
- Direct response helpers for JSON, XML, plain-text, form-encoded, and multipart decoding, plus `contentType()` for the parameter-stripped media type.
- End-to-end response streaming via `streamRequest()`, delivering the body to a sink chunk-by-chunk with bounded memory.
- Typed PSR-18 exception hierarchy (`NetworkException`/`RequestException` and their subtypes) thrown by both adapters.
- Immutable timeout helpers for total and connection timeouts.
- Portable TLS configuration helpers — `withSslVerification()`, `withCustomCA()`, `withCertificate()`, `withMinTlsVersion()` — and the `Utopia\Client\Tls` enum.
- `Utopia\Client\Decorator\Retry` decorator with a pluggable `Strategy` and a default best-practice `Backoff` strategy (idempotent methods only, transient transport failures and `429`/`502`/`503`/`504`, exponential backoff with jitter, `Retry-After` honoured).
- Opt-in W3C Trace Context propagation via `withTracePropagation()` (off by default): forwards the active `utopia-php/span` trace downstream as a `traceparent` header.
- `Utopia\Client\Decorator` base class for composing adapter decorators.
- PHP 8.4+ tooling with Pint, PHPStan level 10, Rector, PHPUnit, Composer audit, and GitHub Actions CI.
- Local PSR/RFC spec copies and translated testing requirements.
