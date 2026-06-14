# PHP Style Guide (Java-inspired)

Baseline: follows PSR-12. Any rule explicitly stated below overrides PSR-12.

This style guide is conceptually aligned with Java conventions (clear encapsulation, CamelCase, strict typing), not PSR standards. The goals are readability, predictability, and clean code.

## Related Documents

- `readme-md-template.md` for README structure guidelines and examples
- `../AGENTS.md` for documentation organization rules

## Goals

- Consistent, easy-to-navigate codebase (Clean Architecture).
- Explicit types, clear responsibilities, low coupling.
- Understandable APIs: descriptive names, predictable behavior.

## Basic Rules

- **Think before coding**. State your assumptions out loud. If the request is ambiguous, ask. If a simpler approach exists, push back. Stop when you are confused, name what is unclear, do not just pick one interpretation and run.
- **Simplicity first**. Write the minimum code that solves the problem. No speculative abstractions. No flexibility nobody asked for. The test: would a senior engineer call this overcomplicated.
- **Surgical changes**. Touch only what the task requires. Do not improve neighboring code. Do not refactor what is not broken or what was not asked for to change. Every changed line should trace back to the request.
- **Goal-driven execution**. Turn vague instructions into verifiable targets before writing a line. "Add validation" becomes “write tests for invalid inputs, then make them pass.”

- Every file starts with `<?php` and has no closing `?>`.
- One element per file: exactly one class/interface/trait/enum per file.
- Use tabs for indentation, no spaces. Max line length: 120 characters (details below).
- Always use braces, even for single-line `if`/`for`/`while`.
- Prefer single quotes for strings; double quotes only when interpolation/escaping is needed.
- A final newline at the end of each file.

## Code Quality

- Follow **S.O.L.I.D**:
  - Single Responsibility: each class/component owns one clearly defined task.
  - Open/Closed: extend by adding implementations, without changing existing code paths.
  - Liskov Substitution: subclasses must not violate base class behavior and must be interchangeable.
  - Interface Segregation: prefer small, focused interfaces over large catch-all interfaces.
  - Dependency Inversion: high-level logic depends on abstractions (interfaces), not concrete implementations.
- Apply **DRY**: avoid repeated logic or structure; extract shared functionality (e.g., services/helpers) instead of copy-paste; required for new and refactoring work.
- Readability matters: prefer code that is easy to scan and understand over code that is merely more explicit or verbose.
- Vertical density matters within the established style rules: do not compress code by violating formatting rules or by collapsing control flow into line noise. Favor semantically dense code that fits more understandable logic into roughly one editor viewport (about 40 lines on a typical 1440p screen) without making it harder to scan.
- Do not extract helper methods unless they are necessary for reuse, a real abstraction boundary, runtime safety, or a meaningful readability gain. Do not fragment local logic into tiny methods just to make a method shorter.

## Naming

- Classes/enums: PascalCase, e.g. `PageRenderer`, `UserService`.
- Methods/functions: camelCase, start with verbs, e.g. `renderPage()`, `findById()`.
- Variables/properties: camelCase, descriptive, no abbreviations like `idx`, `tmp`, `cfg` (except very local contexts).
- Booleans: prefix `is/has/should/can`, e.g. `isPublished`, `hasChildren`.
- Constants: UPPER_SNAKE_CASE, e.g. `DEFAULT_LOCALE`.
- Enums: enum name in PascalCase, cases in UPPER_SNAKE_CASE (Java-like).
- Interfaces: `...Interface` is allowed in this project (legacy), or no suffix; stay consistent.
- Exceptions: end with `Exception`, e.g. `InvalidSlugException`.

## Visibility and Encapsulation

- Properties are `private` by default. Access via methods or readonly properties.
- Use `readonly` for immutable properties (where possible, PHP 8.1+).
- Keep methods as restrictive as possible: `private` > `protected` > `public`.
- Use `final` for classes/methods when inheritance is not intended.

## Class Structure and Order

1. Constants
2. Static properties
3. Instance properties
4. Public static factories (e.g., `fromArray()`)
5. Constructor
6. Public methods
7. Protected methods
8. Private methods
9. Private static factories

Note: static members before instance members. Group related methods.

## Imports, Namespaces, and Structure

- Namespace matches the folder structure, e.g. `PageWeaveCMS\Infrastructure\Rendering` for `src/Infrastructure/Rendering` (PSR-4).
- `use` statements: alphabetically sorted, grouped (PHP built-in, vendor, project-internal), one block per group with a blank line between.
- No leading backslashes in code. Always import and reference by short name (e.g., `\DateTimeInterface` becomes `use DateTimeInterface;`, and `\InvalidArgumentException` becomes `use InvalidArgumentException;`).

## Formatting and Syntax

- Indentation (Tabs vs. Spaces): We choose tabs for all PHP files. Tabs respect personal preference because
  indentation width is configurable in virtually every editor. They also keep indentation stable: you cannot
  accidentally end up with 3 spaces in a 4-space world. Use tabs for indentation, and reserve spaces only
  for alignment within a line when needed.
- Positioning of Curly Braces: The opening curly brace stays on the same line as the statement that opens the
  block (K&R). Indentation communicates block depth; the closing brace sits on its own line so the end of a
  block is immediately visible at a glance.
  ```php
  if($condition) {
      //...
  } else {
  	  //...
  }
  ```
- Line Length: 120 characters is the maximum. Modern monitors are far wider than they were 20 years ago,
  and a 120-column line remains comfortable while allowing clearer, more expressive code.
- Spaces around binary operators: `=`, `===`, `+`, `.` etc.
- One space after `,` in parameter lists and arrays.
- Trailing commas in multi-line arrays/function calls are allowed and encouraged.

## Methods and Parameters

- Strict types for parameters and return values; avoid `mixed`.
- Nullable only when semantically required (`?Type`).
- Optional parameters at the end; no boolean flag parameters (use specialized methods or options objects instead).
- No "magic" implicit side effects; methods stay focused and single-purpose, but do not introduce extra helper methods without a concrete need.

## Control Flow

- Use guard clauses (early returns) instead of deep nesting.
- Avoid `switch`, prefer `match` when appropriate.
- Avoid `else` cascades when guard clauses improve clarity.

## Error Handling

- Use exceptions instead of error codes/`false` sentinel values.
- Catch only if you can actually handle/translate; otherwise rethrow.
- Use domain-specific exceptions instead of generic `RuntimeException`.

## Collections and Arrays

- Prefer value objects/DTOs over unstructured arrays in public APIs.
- Arrays are fine for internal, temporary data; document expected keys.
- Iteration: use `array_map/filter/reduce` when it improves readability; otherwise use clear `foreach` loops.

## Comments and PHPDoc

- Comments explain "why," not "what." The code explains the "what."
- Use PHPDoc for public methods/classes with non-trivial logic, external contracts, or generic collections.
- Use `@param`/`@return` for generic arrays/iterables and `@throws` for exceptions.
- When the only goal is to express static-analysis knowledge, prefer precise annotations such as `@var`, `@phpstan-type`, and `@phpstan-import-type` over adding helper methods whose main purpose is to prove a type or array shape, as long as runtime safety is not weakened.
- No redundant docblocks (e.g., when types are already clear from the signature).

## Tests and Examples (Brief)

- Keep public APIs stable; do not lock internal details via tests.
- Small, focused tests. One test case verifies one behavior.

## Project-Specific Notes

- For newly generated code, watch for `@deprecate` and avoid `@deprecated` classes; use documented alternatives.
- Follow Clean Architecture strictly: domain knows no infrastructure.
- JSON persistence without an ORM. Repositories encapsulate I/O.
- UI similar to GravCMS, but code is strictly typed and modular.
- Existing places with the `...Interface` suffix remain for now (project convention).

---

Example (excerpt):
```php
<?php

namespace PageWeaveCMS\Infrastructure\Rendering;

use InvalidArgumentException;
use PageWeaveCMS\Domain\Entity\Page;
use Twig\Environment as TwigEnvironment;

final class PageRenderer {
	private const DEFAULT_LOCALE = 'de';

	public function __construct(private readonly TwigEnvironment $twig) {}

	public function render(Page $page, ?string $locale = null): string {
		$loc = $locale ?? self::DEFAULT_LOCALE;
		//Guard Clause
		if($page->layoutId === '') {
			throw new InvalidArgumentException('Missing layout ID.');
		}

		//...
		return $this->twig->render('layouts/default.twig', [
			'page' => $page->toArray(),
			'sections' => ['content' => ''],
		]);
	}
}
```
