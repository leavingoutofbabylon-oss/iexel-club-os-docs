# Sprint Definition of Done

**Last verified:** 2026-07-24

---

## Overview

A feature or fix is considered **Done** when all of the following criteria are met.

---

## Code

- [ ] Code is written following the standards in `standards/`
- [ ] PHPCS passes with no new errors or unjustified suppressions
- [ ] No `var_dump`, `print_r` or debug output left in code
- [ ] All new public methods have PHPDoc comments

---

## Security

- [ ] All inputs are sanitised
- [ ] All outputs are escaped
- [ ] All database queries are prepared
- [ ] Capability checks are in place
- [ ] Nonces are verified on all form submissions

---

## Tests

- [ ] Unit tests are written for new service methods
- [ ] All tests pass locally and in CI

---

## Documentation

- [ ] Relevant documentation is updated (see [CODE_REVIEW_CHECKLIST.md](CODE_REVIEW_CHECKLIST.md))
- [ ] `MODULE_STATUS.md` reflects the current state of the module

---

## Review

- [ ] Pull request has been reviewed and approved by at least one team member
- [ ] All review comments have been addressed

---

## Deployment

- [ ] Feature is merged to `main`
- [ ] Release Readiness page passes on a test installation
- [ ] Feature has been demonstrated to the product owner (for significant features)
