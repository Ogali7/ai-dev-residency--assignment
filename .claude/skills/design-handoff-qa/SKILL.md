---
name: design-handoff-qa
description: Reviews UI designs or mockups for handoff-readiness before they go to engineering. Use whenever someone asks to review a design, do a design QA pass, check a mockup, or check if a design is ready for dev.
---

# Design Handoff QA

Review the provided design (Figma file, screenshot, mockup, or exported frames) and decide whether it is ready to hand off to developers. Work through all five steps below in order. Do not skip a step, even if the design looks clean at a glance.

## Review process

### 1. Spacing consistency
- Check that padding, margins, and gaps follow a consistent scale (e.g. a 4px or 8px grid).
- Flag one-off values (e.g. 13px, 27px) and places where equivalent elements use different spacing.
- Check alignment: elements that should share an edge or baseline actually do.

### 2. Color contrast (WCAG)
- Check text against its background, and UI components (icons, input borders, focus rings) against adjacent colors.
- Use the thresholds in [references/wcag-contrast.md](references/wcag-contrast.md). The target is WCAG AA unless the user asks for AAA.
- For each failure, report the foreground and background colors, the measured ratio, and the required ratio.

### 3. Layer naming
- Flag default or meaningless layer names (`Frame 123`, `Rectangle 4`, `Group 7`, `Copy of…`).
- Check that names describe purpose (`header/nav`, `button/primary`) and follow one convention throughout.
- Flag hidden, empty, or stray layers left in the file.
- If only a flat image was provided and layers can't be inspected, say so under this heading instead of guessing.

### 4. Missing states
For every screen and interactive component, confirm the design covers:
- **Empty**: no data yet, zero results, first-time use.
- **Loading**: skeletons, spinners, or progress indicators.
- **Error**: failed requests, validation errors, permission or offline states.

Also note missing interaction states (hover, focus, active, disabled) where they matter.

### 5. Component consistency
- Check that repeated elements (buttons, inputs, cards, icons) use the same component and variants rather than detached or redrawn copies.
- Flag inconsistent typography, corner radii, shadows, or icon sizes between instances of the same element.
- Flag near-duplicate components that should be merged into one with variants.

## Output format

Group findings under exactly these five headings, in this order:

```
## Spacing consistency
## Color contrast
## Layer naming
## Missing states
## Component consistency
```

- Under each heading, list issues as bullets. Each bullet names the location (screen/frame/component), the problem, and a suggested fix.
- If a category has no problems, write **No issues found** under its heading. Never omit a heading.
- End with a one-line verdict: **Ready for handoff** or **Not ready for handoff**, with the number of blocking issues.
