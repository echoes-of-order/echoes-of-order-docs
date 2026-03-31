# Automated API Testing

**Status:** On hold

## Problem / Idea

I explored automatically testing API contracts (e.g. by generating or updating tests when controllers or contracts change) and checking before commit whether dependent packages had changed, so that regressions and contract drift are caught early.

## Points Considered

- What to automate: contract tests, smoke tests, or full integration tests; triggers (pre-commit, CI).
- Coupling to external or shared packages: when and how to detect changes in those packages and re-run or update tests.
- Trade-offs: maintenance of test harnesses and fixtures vs. benefit; impact on development speed.
- Priority vs. other work: infrastructure and core architecture were higher priority at the time of the exploration.

## Outcome

**On hold.** Automated API testing was deferred in favor of other infrastructure and architecture work. It may be revisited when the core stack is stable and the cost/benefit is clearer.
