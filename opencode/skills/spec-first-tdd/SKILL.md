---
name: spec-first-tdd
description: Use when implementing any feature, bugfix, or behavior change in sync-services. Adds two gates around TDD — behavioral spec and adversarial test review.
---

# Spec-First TDD Pipeline

## Overview

Two additional gates around the standard TDD cycle that prevent AI-written tests from being circular (testing what the code does instead of what it should do).

## Gate 1: SPEC (before any code or tests)

A behavioral spec file MUST exist before any code or tests.

1. Ask the human: "What behavior are we implementing? Let's write the spec first."
2. Create the spec at `docs/specs/<date>-<topic>.md` (create the directory if needed) using this template:

```markdown
## Feature: <name>

### Context

<1-2 sentences: why this change exists>

### Expected Behaviors

1. When <trigger>, then <outcome>
2. When <edge case>, then <outcome>
3. When <error condition>, then <outcome>

### Out of Scope

- <what this does NOT change>
```

3. The human writes the spec. Help them refine it, but the behaviors must come from them.
4. Commit the spec: docs: add spec for <feature>

*Do not write any code or tests until the spec file is committed.*

*CRITICAL: During the RED phase, do NOT read implementation source code.* Write tests from the spec and type definitions only. This breaks the circularity between "what the code does" and "what the tests verify."

## Gate 2: ADVERSARIAL REVIEW (after RED, before GREEN)

After tests are written and failing, invoke the adversarial-test-reviewer agent before writing implementation.

```
Invoke the adversarial-test-reviewer agent with the spec file path and test file path(s)
If verdict is FAIL: fix gaps (still blind to implementation), re-run reviewer
If verdict is PASS: proceed to GREEN
```

## Full Pipeline

```
SPEC (gate 1)              → Human writes behavioral spec
RED                        → AI writes failing tests from spec (blind to implementation)
ADVERSARIAL REVIEW (gate 2)→ Agent validates tests cover the spec
GREEN                      → AI writes minimal implementation
```

## Commit Convention

| Phase | Prefix | Example |
|-------|--------|---------|
| Spec | docs: | docs: add spec for batch retry logic |
| Tests (red) | test: | test: add tests for batch retry (red) |
| Implementation (green) | feat: or fix: | feat: implement batch retry (green) |
