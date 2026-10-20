# Technical TODO

## Enforce architecture import boundaries

Add ESLint import boundaries when `src/shared`, `src/modules`, and `src/features`
have concrete consumers. Reference Postline Dashboard's foundation PR #17.

- Keep dependencies flowing from `app` to `features`, `modules`, and `shared`.
- Prevent `shared` from importing application, feature, or module code.
- Prevent modules from importing application or feature code; review cross-module
  and cross-feature access before choosing isolation rules.
- Handle missing layer directories gracefully instead of assuming they exist.
- Verify TypeScript alias resolution and add checks for allowed and rejected
  imports before enabling the rules.

Do not create empty layer folders just to satisfy the lint configuration.
