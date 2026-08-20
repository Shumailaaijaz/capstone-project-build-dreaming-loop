# Build Agent Rules

1. Always run `npm test` before committing.
2. Close database connections in a `finally` block (or equivalent guaranteed-cleanup construct) immediately after each build or migration step, even if the step fails.
3. Retry failed network requests up to 3 times before failing.
4. Never commit directly to main; always open a PR for review.
