---
name: accessibility-code-review
description: Reviews front-end code (HTML, CSS, JavaScript, React, Vue, or similar) for accessibility problems against WCAG 2.2 AA, plus cognitive accessibility for people with ADHD and other attention or memory differences. Use this whenever someone asks for an accessibility review, an a11y check, a WCAG audit, or asks if their app, page, form, or component is accessible. Also use it after building or changing any user interface, even if the user did not mention accessibility.
---

# Accessibility Code Review

Review the provided code and decide whether it is accessible. Work through all six checks below in order. Do not skip a check, even if the code looks fine at a glance. Read the actual code; do not guess about files you have not opened.

## Review process

### 1. Structure and meaning (semantic HTML)
- Buttons are `<button>`, links are `<a href>`. Flag clickable `<div>` or `<span>` elements.
- The page has one `<h1>`, and headings go in order without skipping levels.
- Landmarks are used: `<header>`, `<nav>`, `<main>`, `<footer>`.
- The page has a meaningful `<title>` and a `lang` attribute on `<html>`.
- Lists use `<ul>`/`<ol>`, and data tables use `<table>` with `<th>`.

### 2. Keyboard and focus
- Everything that can be clicked can also be reached and used with Tab, Enter, Space, and arrow keys where expected.
- Focus order follows the visual order. Flag positive `tabindex` values.
- A visible focus outline exists. Flag `outline: none` with no replacement.
- Dialogs and menus trap focus while open, close with Escape, and return focus to the button that opened them.
- Focused elements are not hidden behind sticky headers or footers.

### 3. Screen reader labels
- Images have `alt` text that describes their purpose. Decorative images use `alt=""`.
- Icon-only buttons have an accessible name (`aria-label` or visually hidden text).
- Custom components expose the right role and state (for example `aria-expanded`, `aria-checked`, `aria-selected`).
- ARIA is used only when native HTML can't do the job. Flag ARIA that contradicts the element.
- Status updates (saved, error, item added) are announced with `aria-live` or `role="status"`.

### 4. Forms and errors
- Every input has a visible `<label>` connected to it. Placeholder text alone is not a label.
- Common fields use `autocomplete` (name, email, address, credit card).
- Errors say what went wrong and how to fix it, appear next to the field, and are linked with `aria-describedby`.
- Errors are not shown with color alone.
- Users are not asked to re-enter information they already gave in the same flow.
- Login does not require solving puzzles or remembering codes without allowing paste or a password manager.

### 5. Motion, timing, and touch
- Animations respect `prefers-reduced-motion`.
- Nothing flashes more than three times per second.
- Time limits can be turned off, adjusted, or extended.
- Auto-playing or auto-advancing content can be paused.
- Tap targets are at least 24 by 24 CSS pixels.
- Text and interactive colors set in code meet WCAG AA contrast (4.5:1 for normal text, 3:1 for large text and UI parts).

### 6. Cognitive accessibility (ADHD-friendly)
These go beyond the WCAG minimum. Report them as recommendations, not failures.
- Each screen has one clear main action. Flag screens that compete for attention.
- Wording is short and plain. Flag jargon and long instructions.
- Progress is saved automatically so users can leave and come back.
- Long tasks are split into small steps with a progress indicator.
- Destructive or costly actions (delete, pay, transfer) ask for confirmation and can be undone where possible.
- Notifications, badges, and pop-ups are limited and can be turned off.
- Help and contact options appear in the same place on every screen.

## Output format

Group findings under exactly these six headings, in this order:

```
## Structure and meaning
## Keyboard and focus
## Screen reader labels
## Forms and errors
## Motion, timing, and touch
## Cognitive accessibility
```

- Under each heading, list issues as bullets. Each bullet names the file and line (or component), the problem, the WCAG success criterion number where one applies (for example 2.4.7), and a suggested code fix.
- Mark each issue as **Blocking** (fails WCAG AA) or **Should fix** (best practice or cognitive recommendation).
- If a category has no problems, write **No issues found** under its heading. Never omit a heading.
- End with a one-line verdict: **Accessible** or **Not accessible**, with the number of blocking issues.
- Note that an automated code review cannot replace testing with a real screen reader and keyboard, and suggest the user do that before launch.
