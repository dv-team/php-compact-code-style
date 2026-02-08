# README.md Template for PHP Libraries

This document suggests a structure and content for a PHP library README. These are rough guidelines only. Every project is unique and should emphasize the sections that matter most to its users.

## Goals of a README

- Explain what the library does and why it exists.
- Show the fastest path to a successful first use.
- Point to deeper documentation and references.
- Set expectations: compatibility, stability, and support.

## Recommended Structure (with intent)

1. Project title and short description
   - One sentence: what it does and for whom.
2. Status and compatibility
   - PHP version, required extensions, supported frameworks.
3. Installation
   - Usually via Composer; include a minimal command.
4. Quick Start
   - Small, copy-paste example that runs.
5. Usage
   - Common tasks or workflows with concise examples.
6. Public API overview
   - Link to full API docs or describe key interfaces.
7. Configuration
   - Environment variables, config arrays, or files.
8. Error handling and edge cases
   - Exceptions, error codes, and failure modes.
9. Testing and development
   - How to run tests or build tooling.
10. Contributing and support
    - How to file issues, where to ask questions.
11. License
    - SPDX name and link to full license.

## Example README Skeleton

```md
# Acme Cache

A tiny, fast cache abstraction for PHP 8.2+ with PSR-16 compatibility.

## Status

- PHP: 8.2+
- Extensions: ext-json
- Stability: stable

## Installation

composer require acme/cache

## Quick Start

```php
<?php

use Acme\Cache\Cache;

$cache = Cache::memory();
$cache->set('user:1', ['id' => 1, 'name' => 'Ada']);

var_dump($cache->get('user:1'));
```

## Usage

### Namespaced keys

```php
$cache->set('user:42', $user);
```

### Time-to-live

```php
$cache->set('user:42', $user, 3600);
```

## Public API

- `CacheInterface` (see docs/api.md)
- `Cache::memory()` and `Cache::filesystem($path)`

## Configuration

- Filesystem cache root directory
- Default TTL

## Error Handling

- Throws `InvalidKeyException` on invalid keys
- Returns `null` on cache misses

## Testing

composer test

## Contributing

See CONTRIBUTING.md

## License

MIT. See LICENSE.
```

## Code Examples: What and How

- Show the smallest complete flow that works.
- Cover the top 2-3 use cases users will try first.
- Keep examples short and runnable; avoid pseudo-code unless necessary.
- Use realistic values and error handling where it matters.
- Prefer multiple small examples over one large block.
- Ensure examples match the current API and coding style.

## Documenting Interfaces (Recommended)

Document all public interfaces and classes. Keep the detail level consistent so users can predict behavior.

For each public interface or class:
- Purpose and responsibilities
- Stability (experimental/stable/deprecated)
- Constructor or factory behavior
- Method signatures and behavior
- Parameters and return values
- Exceptions and error conditions
- Side effects (I/O, state changes)

Example format:

```md
### CacheInterface

**Purpose:** Key-value cache contract.

#### Methods

- `get(string $key, mixed $default = null): mixed`
  - Returns cached value or `$default` when missing.
  - Throws `InvalidKeyException` for invalid keys.
- `set(string $key, mixed $value, int $ttl = 0): void`
  - `$ttl` is seconds; `0` means no expiration.
```

PHPDoc example:

```php
/**
 * @param string $key
 * @param mixed $default
 * @return mixed
 * @throws InvalidKeyException
 */
public function get(string $key, mixed $default = null): mixed;
```

## What Else Should Be Documented

- Architecture or design decisions (if relevant)
- Configuration and defaults
- Compatibility matrix (PHP versions, extensions, frameworks)
- Migration guides and breaking changes
- Changelog and versioning policy
- Security policy and disclosure process
- Contributing guidelines and code of conduct

## Links and Organization

- Keep links in README and docs/ accurate and discoverable.
- If a topic grows, move it into a dedicated file under docs/.
- For subtopics, create a subfolder under docs/ and link to it.

These are rough guidelines only. Adapt the README to your library and to what your users need most.
