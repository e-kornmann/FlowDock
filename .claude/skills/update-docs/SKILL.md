---
name: update-docs
description: Checks every doc (and, once code exists, every code comment) against the rules in .claude/rules. Moves duplicated information to its one home and replaces the copy with a link, fixes broken links and stale references, and removes unnecessary comments. Run by hand with /update-docs, optionally with a folder or file to limit it.
argument-hint: "[path - a folder or file; the whole repo when left out]"
disable-model-invocation: true
context: fork
agent: general-purpose
---

# Update docs

Bring the documentation in this repo in line with itself, with the code and with the rules. Scope: `$ARGUMENTS` if given. Otherwise: `README.md`, `CLAUDE.md`, `docs/`, `.claude/rules/`, `.claude/skills/`, `.gitignore`, and every code and config file once they exist. Leave out `node_modules`, `dist` and generated files. Never read `.env` or `*.local`: they hold secrets.

This is a hygiene pass, not a design review. It changes where things are written, never what was decided. Domain or architecture questions belong to `/architecture-review`.

## The rules

Read these first and apply them to everything you look at:

- `.claude/rules/documentation.md`: where each kind of information lives, and how docs link
- `.claude/rules/comments.md`: when a code comment is necessary, and how it is written

## Steps

1. List the files in scope. Work through them one folder at a time.
2. **Duplicates.** For each fact, check it lives only in its home from the table in `documentation.md`. When it also appears elsewhere, keep it in its home (merge in anything the copy had that the home lacked) and replace the copy with a link. A one-word mention that links to the home is fine; a restated definition, list or rule is not.
3. **Placement.** Content in the wrong home moves to the right one, for example a business rule written in an ADR's consequences that is missing from `business-rules.md`. Files outside the table: report them and suggest a home.
4. **Consistency of terms.** Domain terms must match `docs/domain/domain-language.md` exactly. Report synonyms ("booking", "item", "boat") and fix them where the meaning is unambiguous.
5. **Stale references.** Hard-coded ranges or lists that no longer match the folder ("ADR-001 through ADR-007", a list of diagrams), and paths or concepts that no longer exist. Rewrite them to point at the folder or the current name.
6. **Links.** Check every markdown link and every `see ...` path still resolves.
7. **Code comments** (once code exists): check each comment against the code it sits on. Rewrite wrong ones, remove unnecessary ones, leave correct ones exactly as they are. No style-only churn.
8. Change docs and comments only, never code and never a decision. When two docs contradict each other on substance (not wording), or a comment shows the code is wrong, do not pick a side: report it.

## Report

Finish with a short report:

- per file: what was moved, linked, rewritten or removed, with one line on the important ones
- links or paths that were broken, and what they point to now
- contradictions in substance that need Elton's decision
- files that have no home in the documentation table
