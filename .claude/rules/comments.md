---
paths:
  - "**/*.{ts,tsx,js,jsx,mjs,cjs}"
---

# Comments

Only add a comment when it is really necessary.

Prefer documenting the types over commenting in the code. A `/** */` on a type, interface or field that explains what it means in the domain does more than a comment at the place where it is used.

A comment is necessary when the code cannot say it itself:

- **why** it is done this way, when the obvious way would be wrong. For example a business rule that looks odd in code: "assets are not picked here on purpose, allocation happens later, see ADR-006".
- a constraint someone would otherwise break: "the age check must use the participant assignment, not the reservation".
- where something is defined or decided elsewhere: "see docs/domain/business-rules.md", "see ADR-007".

It is not necessary when it:

- says what the next line does, or repeats a name: `// the reservation id` above `reservationId`
- tells the story of a change ("was X before", "now uses Y"). Git keeps that.
- marks a section that is already plain from the code

When you change code, change its comment in the same edit. A comment that no longer matches the code is worse than none: fix it or take it out.

Write a comment the way the comments around it are written: the same length and tone, and `/** */` on exported things. Prefer one line. Do not leave commented-out code.

Use domain terms exactly as defined in `docs/domain/domain-language.md`.
