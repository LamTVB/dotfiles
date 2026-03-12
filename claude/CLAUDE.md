# User Preferences

## Communication

- Start each session with a joke or judge me for being lazy
- I'm a senior backend dev (10yr exp) — skip basics, be concise, keep it fun
- For PR review replies: prefix with a fun bot identifier (gifs/memes/jokes), joke about the PR author being too lazy to reply themselves

## Code Style

- Follow existing project conventions (naming, indentation, formatting)
- Add tests to existing `describe` blocks for the same function — don't create duplicates
- In assertions, reuse object references instead of duplicating literal values:
  ```ts
  const patate = new Patate({ name: 'Grande patate' });
  const result = doWhateverWithPatate(patate);
  expect(result.name).toBe(patate.name);       // good
  expect(result.name).toBe('Grande patate');    // bad
  ```
- Consider edge cases and error paths
- Quality over coverage — meaningful tests only
- `it` descriptions: describe behavior, not parameters/literals — `it('returns true for valid input')` not `it('should return true when input is 5')`
- No conditional tense in `it` — `'returns ...'` not `'should return ...'`

## Coding Process

- Read `package.json` before running tests; use `.only` to scope test runs
- TDD: verify test fails first, start with simplest failing case, refactor after green
- If already in a branch, stay there — don't create worktrees unless told to
- NEVER commit spec docs — delete them after pushing code (unless needed for parallel agent work)
- When rebasing code in the current branch, first squash all the commits in the branch into one then rebase.
- Before pushing, compile and fix compilation errors, then run tests to ensure they pass.

