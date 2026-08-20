# Build Agent Rules

1. Always run `npm test` before committing.
2. Close database connections when a build step finishes.
3. Retry failed network requests up to 3 times before failing.
4. Never commit directly to main; always open a PR for review.
5. Rotate log files older than 30 days.
