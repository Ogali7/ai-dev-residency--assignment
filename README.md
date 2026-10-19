# AI Dev Residency Assignment

This repo contains a Claude Code skill for reviewing UI designs before they go to engineering.

## design-handoff-qa skill

`design-handoff-qa` checks a design (a Figma file, screenshot, mockup, or exported frames) for handoff readiness. It works through five checks in order and ends with a verdict of **Ready for handoff** or **Not ready for handoff**.

The five checks:

1. **Spacing consistency**: spacing follows one scale (for example 4px or 8px), no one-off values, and elements that should align do.
2. **Color contrast**: text and UI components meet WCAG AA (or AAA if you ask for it).
3. **Layer naming**: layers have meaningful names, follow one convention, and there are no stray or hidden layers.
4. **Missing states**: empty, loading, and error states are designed for each screen, plus interaction states where they matter.
5. **Component consistency**: repeated elements use the same component and variants, with consistent typography, radii, shadows, and icon sizes.

Each finding names the location, the problem, and a suggested fix. Every category gets a heading, and categories with no problems say **No issues found**.

### Where it lives

```
.claude/skills/design-handoff-qa/
├── SKILL.md                      # The skill instructions and review process
└── references/
    └── wcag-contrast.md          # Contrast thresholds and how to calculate ratios
```

Because it sits in the project's `.claude/skills/` folder, Claude Code picks it up automatically when you work in this repo.

### How to use it in Claude Code

1. Open this repo in Claude Code.
2. Share the design with Claude: attach a screenshot or exported frames, or paste a link to the Figma file.
3. Ask for a review in plain language, for example:
   - "Review this design for handoff readiness."
   - "Do a design QA pass on this mockup."
   - "Check if this screen is ready for dev."

Claude will follow the five steps and return the report under the five headings.

If you only give Claude a flat image, it can't inspect layers. The layer naming section will say so instead of guessing.

### Contrast checks

The thresholds and calculation method are in [references/wcag-contrast.md](.claude/skills/design-handoff-qa/references/wcag-contrast.md). Ratios are not rounded up: 4.47:1 fails a 4.5:1 requirement.
