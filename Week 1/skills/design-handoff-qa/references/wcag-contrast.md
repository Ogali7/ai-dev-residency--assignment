# WCAG Contrast Ratios

Reference for step 2 of the design handoff QA. Ratios come from WCAG 2.1/2.2.

## Minimum ratios

| Content | AA | AAA |
|---|---|---|
| Normal text | 4.5:1 | 7:1 |
| Large text | 3:1 | 4.5:1 |
| UI components and graphical objects (SC 1.4.11) | 3:1 | — |

**Large text** means at least 18pt (24px) regular, or at least 14pt (~18.66px) bold.

UI components include input borders, focus indicators, icons that convey meaning, and the parts of charts needed to understand them. AAA sets no separate requirement for these.

## Exemptions
- Disabled (inactive) controls
- Purely decorative elements
- Logos and brand wordmarks
- Text that is part of a picture with significant other visual content

## How to calculate

Contrast ratio = (L1 + 0.05) / (L2 + 0.05), where L1 is the relative luminance of the lighter color and L2 of the darker one.

Relative luminance for an sRGB color:
1. Divide each channel by 255 to get R, G, B in 0–1.
2. For each channel c: if c ≤ 0.04045, use c / 12.92; otherwise use ((c + 0.055) / 1.055) ^ 2.4.
3. L = 0.2126 × R + 0.7152 × G + 0.0722 × B.

Ratios range from 1:1 (same color) to 21:1 (black on white). Don't round up: 4.47:1 fails a 4.5:1 requirement.

## Quick examples
| Foreground | Background | Ratio | Normal text |
|---|---|---|---|
| #000000 | #FFFFFF | 21:1 | AAA |
| #767676 | #FFFFFF | 4.54:1 | AA |
| #959595 | #FFFFFF | 2.99:1 | Fails |
