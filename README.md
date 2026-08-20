# capstone-project-build-dreaming-loop

A demo project for a "dreaming loop": a build agent that follows a fixed set of
rules while running nightly builds, and a separate process that periodically
scans the accumulated run history for repeated patterns or recurring issues.

## Structure

- `rules/build-agent-rules.md` — rules the build agent follows on every run
  (testing, DB connection cleanup, network retries, PR-based commits).
- `progress.md` — dated log of each nightly build run and its outcome.
- `dreaming-state.md` — tracks the last date the dreaming loop scanned up to,
  so each scan only looks at new entries since the previous run.

## How it works

1. The build agent runs nightly, following `rules/build-agent-rules.md`, and
   appends an entry to `progress.md` describing what happened.
2. The dreaming loop periodically reads the unscanned portion of
   `progress.md` (using `dreaming-state.md` to know where it left off),
   looks for repeated patterns (e.g. a recurring failure mode), and updates
   the rules or logs a finding if one is found.
3. `dreaming-state.md` is then advanced to the latest scanned date.
