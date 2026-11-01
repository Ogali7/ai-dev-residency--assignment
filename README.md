# AI Dev Residency Assignment

This repo holds my work for the Tech Fleet AI Development Residency, organized by week.

## Week 1: Claude Code Skills

Three Claude Code skills that help Claude review work for enterprise-ready quality: UX, accessibility, and security. Each skill follows the same pattern: a clear description of when to use it, ordered checks, a fixed set of headings, and a final verdict.

| Skill | What it reviews | Verdict |
|---|---|---|
| `design-handoff-qa` | UI designs (Figma files, screenshots, mockups) for handoff readiness: spacing, contrast, layer naming, missing states, and component consistency | Ready / Not ready for handoff |
| `accessibility-code-review` | Front-end code against WCAG 2.2 AA: structure, keyboard and focus, screen reader labels, forms, motion and touch, plus cognitive accessibility for people with ADHD | Accessible / Not accessible |
| `security-code-review` | Application code, with extra care for financial data: secrets and API keys, input handling, login, access control, data protection, and dependencies | Safe / Not safe to ship |

### Folder structure

```
Week 1/
├── SUBMISSION.md
└── skills/
    ├── design-handoff-qa/
    │   ├── SKILL.md
    │   └── references/
    │       └── wcag-contrast.md
    ├── accessibility-code-review/
    │   └── SKILL.md
    └── security-code-review/
        └── SKILL.md
```

### Installing the skills

Claude Code only loads skills from a `.claude/skills/` folder. To make these skills available in every session, copy the three folders from `Week 1/skills/` into your personal skills folder:

- Windows: `C:\Users\<your-name>\.claude\skills\`
- Mac or Linux: `~/.claude/skills/`

Then start a new Claude Code session, since skills load when a session starts.

### Using the skills

Ask Claude to list its skills to confirm they loaded. Claude decides when to use a skill by reading its description, so small or simple requests may get a general answer instead. For a full, consistent review, ask for the skill by name, for example:

- "Run the design-handoff-qa skill on this mockup."
- "Run the accessibility-code-review skill on this component."
- "Run the security-code-review skill on this API route."

These reviews support, but don't replace, testing with real assistive technology and professional security testing.
