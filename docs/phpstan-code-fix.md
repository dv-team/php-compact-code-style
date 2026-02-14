# PHPStan code fixing rules

## Rules

- Run **phpstan** and fix the issues reported.
- Look at the `composer.json` to see how to run **phpstan** to check the integrity of the code.
- Never alter files in the composer vendor folder typically found at `vendor/`.
- Also look for the minimum supported PHP version in the `composer.json` file and only use features that are available in that version.

### Phase 1

- Use only comment annotations, no code changes (exception = php supported types). If that is not enough to solve the problem, then skip the issue at that point. 
- Use `/** @var ... */` for example and also `@phpstan-type ...` as well as `@phpstan-import-type` to define types.
- Prefer to use actual types over comment annotations (like `: void` over `/** @return void */`). Do not use `@return` when it's just adressing a type also available in the minimum supported PHP version.
- Prefer defining types where they first enter the project realm.
- Try not to use `mixed` as a type. Look here code is used and where code is coming from and make plausible assumptions about what the code is doing. Only if this is all not helpful, then use `mixed`.

### Phase 2

- After trying to fix the issues reported by **phpstan** without changing actual code, try to fix the code itself only subtile changes.
  - You are allowed to add if statements and type casts.
  - You are not allowed to add new functions or classes at this point.