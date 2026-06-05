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
- Request factories for JSON, form-encoded, query-string, raw-body, and multipart requests.
- Direct response helpers for JSON, form-encoded, and multipart response decoding.
- Immutable timeout helpers for total and connection timeouts.
- PHP 8.4+ tooling with Pint, PHPStan level 10, Rector, PHPUnit, Composer audit, and GitHub Actions CI.
- Local PSR/RFC spec copies and translated testing requirements.
