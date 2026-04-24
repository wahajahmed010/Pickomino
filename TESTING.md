# Testing

## Framework
[pytest](https://pytest.org/) 8.x (pytest 9 is not supported).

## Test Suite
The test suite is maintained in a private submodule. Contributors requiring
access should contact the maintainer.

## Running Tests
Tests are run automatically via GitHub Actions on every push and pull request.
PRs from forks will not trigger CI — contact the maintainer for access.

## Pre-commit
A subset of checks runs via pre-commit hooks on every commit. Tests are not
part of the pre-commit suite.

## Coverage
95%+ test coverage is maintained and enforced in CI.

---

## Testing Philosophy
### Principle: Tests Verify Rules, Not Coverage
Coverage measures lines executed. It does not measure correctness. This project
had 96% coverage while hiding bugs in core game logic. Tests must assert that
game rules are correctly implemented.

### Rules Reference
Tests are derived from the official Pickomino rulebook:
[pickomino-rulebook.pdf](https://github.com/smallgig/Pickomino/raw/main/pickomino-rulebook.pdf)

Every rule in the rulebook should map to at least one test.

### Policy: Bug Fix = Failing Test First
Every bug fix must include a test that:
1. Fails on the current (buggy) code.
2. Passes after the fix.

A bug fix PR without a failing test is incomplete.

---

## Test Categories

### Fast Tests (pre-commit, push stage)
- Location: `test/`
- Purpose: Smoke tests — catch regressions quickly.
- Run time: Seconds.
- Assert basic invariants, input validation, no crashes.
- These do not verify game rules.

### Rules Tests
- Location: `test/`
- Purpose: Verify Pickomino game rules are correctly implemented.
- Each test name describes the rule it verifies.
- Example: `test_bust_returns_top_tile_and_removes_highest_from_table`

### Mutation Testing
- Tool: [mutmut](https://mutmut.readthedocs.io/)
- Purpose: Verify that tests actually detect code changes.
- If a mutation survives, the test suite has a gap.

---

## Naming Convention

```
test_<rule_or_behavior_described_in_plain_english>

Good: test_bot_stops_when_collecting_worm_reaches_tile
Bad:  test_step_valid_action
```
