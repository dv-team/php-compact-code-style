# php-compact-code-style

This repository defines the compact PHP coding style we use across projects, pairing an editor configuration with a concise style guide and documentation structure.

## Status and Scope

- Baseline: follows PSR-12, with explicit overrides documented in the style guide. ([PHP Style Guide](./docs/php-style-guide.md))
- Scope: PHP files only; the editor rules apply to `*.php`. ([.editorconfig](./.editorconfig))
- Goals: readability, predictability, explicit types, clear responsibilities, and understandable APIs. ([Goals](./docs/php-style-guide.md#goals))

## Installation

- Copy `.editorconfig` into your project root. ([.editorconfig](./.editorconfig))
- Adopt the PHP style guide as the authoritative rules for PHP code. ([docs/php-style-guide.md](./docs/php-style-guide.md))
- Use the README template guidelines when writing project documentation. ([docs/readme-md-template.md](./docs/readme-md-template.md))

## Quick Start

```php
<?php

use InvalidArgumentException;

final class PageRenderer {
	private const DEFAULT_LOCALE = 'en';

	public function render(string $layoutId, ?string $locale = null): string {
		$loc = $locale ?? self::DEFAULT_LOCALE;
		if($layoutId === '') {
			throw new InvalidArgumentException('Missing layout ID.');
		}

		return $loc . ':' . $layoutId;
	}
}
```

## Usage

- Follow the formatting rules defined in `.editorconfig` (tabs, 120-char lines, K&R braces, spacing rules). ([.editorconfig](./.editorconfig))
- Apply the naming, structure, and behavior rules from the PHP style guide. ([docs/php-style-guide.md](./docs/php-style-guide.md))
- Document libraries using the README template structure and examples. ([docs/readme-md-template.md](./docs/readme-md-template.md))

## Documentation

### EditorConfig (PHP formatting)

- `*.php` files use LF, tabs with size 4, UTF-8, trimmed trailing whitespace, final newline, and max line length 120. ([.editorconfig](./.editorconfig))
- JetBrains formatting uses K&R braces, minimal wrapping, no alignment, alphabetic imports, short arrays, and trailing commas for multiline arrays/params/match arms. ([.editorconfig](./.editorconfig))
- Spacing: spaces around binary operators, space after commas, no spaces inside parentheses/brackets, and lowercase keywords/boolean/null. ([.editorconfig](./.editorconfig))
- Blank lines: 1 after functions/methods/imports, 1 around classes, 0 around constants/fields, 0 after PHP opening tag, allow single-line simple classes, and keep empty methods in one line. ([.editorconfig](./.editorconfig))

### PHP Style Guide (Java-inspired, PSR-12 baseline with overrides)

- Goals: readability, predictability, explicit types, clear responsibilities, low coupling, and understandable APIs. ([Goals](./docs/php-style-guide.md#goals))
- File rules: `<?php` only, no closing tag, one class/interface/enum per file, and a final newline. ([Basic Rules](./docs/php-style-guide.md#basic-rules))
- Indentation and formatting: tabs, 120-char max lines, braces always on, K&R brace style, single quotes unless interpolation, spaces around binary operators, and trailing commas for multiline lists. ([Basic Rules](./docs/php-style-guide.md#basic-rules), [Formatting and Syntax](./docs/php-style-guide.md#formatting-and-syntax))
- Code quality: S.O.L.I.D + DRY are required design principles. ([Code Quality](./docs/php-style-guide.md#code-quality))
- Naming: PascalCase classes/enums, camelCase methods/variables, `is/has/should/can` booleans, UPPER_SNAKE_CASE constants, UPPER_SNAKE_CASE enum cases, `Exception` suffix, and consistent interface suffix usage. ([Naming](./docs/php-style-guide.md#naming))
- Encapsulation: properties private by default, use `readonly` for immutables, keep visibility as restrictive as possible, and use `final` when inheritance is not intended. ([Visibility and Encapsulation](./docs/php-style-guide.md#visibility-and-encapsulation))
- Class order: constants, static props, instance props, static factories, constructor, public, protected, private, private static factories. ([Class Structure and Order](./docs/php-style-guide.md#class-structure-and-order))
- Namespaces/imports: PSR-4 paths, `use` statements alphabetic and grouped (built-in/vendor/project) with blank lines, and no leading backslashes. ([Imports, Namespaces, and Structure](./docs/php-style-guide.md#imports-namespaces-and-structure))
- Methods and parameters: strict types, avoid `mixed`, nullable only when needed, optional params last, no boolean flag params, small single-purpose methods. ([Methods and Parameters](./docs/php-style-guide.md#methods-and-parameters))
- Control flow: favor guard clauses, avoid `switch` when `match` fits, and avoid `else` cascades. ([Control Flow](./docs/php-style-guide.md#control-flow))
- Error handling: use exceptions, catch only to handle/translate, prefer domain-specific exceptions. ([Error Handling](./docs/php-style-guide.md#error-handling))
- Collections: prefer value objects/DTOs in public APIs, arrays for internal data with documented keys, and functional helpers when they improve readability. ([Collections and Arrays](./docs/php-style-guide.md#collections-and-arrays))
- Comments/PHPDoc: explain “why,” use PHPDoc for public non-trivial APIs or generic collections, include `@param`/`@return` for generic iterables and `@throws` for exceptions, avoid redundant docblocks. ([Comments and PHPDoc](./docs/php-style-guide.md#comments-and-phpdoc))
- Tests: small focused tests, verify behavior without locking internals. ([Tests and Examples](./docs/php-style-guide.md#tests-and-examples-brief))
- Project-specific: avoid deprecated APIs, keep domain free of infrastructure, JSON persistence without ORM, and UI aligned with GravCMS-style patterns. ([Project-Specific Notes](./docs/php-style-guide.md#project-specific-notes))

### README Guidelines for Libraries

- These are rough guidelines; each project should adapt sections to its own priorities. ([README.md Template](./docs/readme-md-template.md))
- Goals: explain what it does, show a fast first success, link to deeper docs, and set expectations on compatibility/stability/support. ([Goals of a README](./docs/readme-md-template.md#goals-of-a-readme))
- Recommended sections: title/description, status/compatibility, installation, quick start, usage, public API, configuration, error handling, testing, contributing/support, license. ([Recommended Structure](./docs/readme-md-template.md#recommended-structure-with-intent))
- Code examples: smallest working flow, top use cases, short and runnable, realistic values and error handling, multiple small examples, match current API/style. ([Code Examples](./docs/readme-md-template.md#code-examples-what-and-how))
- Interface docs: purpose, stability, constructor/factory behavior, method signatures/behavior, params/returns, exceptions, side effects, and PHPDoc for `@param`/`@return`/`@throws`. ([Documenting Interfaces](./docs/readme-md-template.md#documenting-interfaces-recommended))
- Additional docs to include: architecture, configuration, compatibility matrix, migration/breaking changes, changelog/versioning, security policy, contributing/code of conduct. ([What Else Should Be Documented](./docs/readme-md-template.md#what-else-should-be-documented))
- Documentation organization: keep links accurate, move growing topics into dedicated files, and use subfolders for subtopics. ([Links and Organization](./docs/readme-md-template.md#links-and-organization))

## Details

- [.editorconfig](./.editorconfig)
- [docs/php-style-guide.md](./docs/php-style-guide.md)
- [docs/readme-md-template.md](./docs/readme-md-template.md)
