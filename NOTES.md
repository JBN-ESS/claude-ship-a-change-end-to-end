# NOTES

## Plan
<!-- DRAFT: the plan approved in this session was for writing CLAUDE.md, not for the endpoint. Replace this with your own plan-mode run for the feature if you did one. -->
Add `PUT /users/:id` following the existing pattern: a new `updateUser(id, { name, email })` helper in `db/store.js`, and a `PUT /:id` handler in `routes/users.js` that validates input, calls the store, and returns 200, 400 or 404. No edits to the provided tests.

## Model
<!-- DRAFT: fill in what you actually chose and why. -->
The endpoint was implemented with Claude Sonnet 5.5. This is a small, well-specified change with tests that define "done", so a fast mid-tier model is enough. A larger model would add cost without changing the result.

## Commits
<!-- DRAFT: update to match what you actually commit. -->
Planned split, one logical change per commit:
1. Add `updateUser` to `db/store.js` (data layer).
2. Add `PUT /users/:id` with validation and 404 handling in `routes/users.js`.
3. Add `CLAUDE.md` and `NOTES.md` (docs).

## Review
<!-- DRAFT: no review has been run yet. Run one, then record what it caught or confirmed. -->
Not yet done. Points to check:
- Validation requires `name` and `email` to be non-empty strings (whitespace-only is rejected, and values are trimmed). The 400 check runs before the lookup, so an invalid body for an unknown id returns 400, not 404.
- A non-numeric id becomes `NaN`, matches no user, and returns 404.
- Email format is not validated, matching the existing `POST /users`.
- `updateUser` mutates the stored object in place, which is fine for the in-memory store.
