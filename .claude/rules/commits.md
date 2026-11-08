# Commits

Only commit when Elton asks.

Use Conventional Commits: `type(scope): summary`, in lowercase and the imperative mood.

- Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `build`, `ci`.
- Scope is optional. Once code exists, use the domain area: `feat(reservations): ...`, `fix(allocation): ...`. For the Claude setup use `chore(claude): ...`.
- One logical change per commit. Name the commit after the decision or milestone, not after the individual edits.

No AI co-author trailer. Elton is the sole author, and AI usage is disclosed in `README.md` instead. `.claude/settings.json` turns off Claude Code's attribution line.

Commit a clean checkpoint before running a review skill, so its suggestions show up as a reviewable `git diff`.
