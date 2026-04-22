# Design Tokens — Editorial GRC

## Brand Colors

| Token | Value | Usage |
|-------|-------|-------|
| brand-50 | #F7F0FF | Light tint, pill bg, hover states |
| brand-100 | #EDDEFE | Subtle borders, backgrounds |
| brand-200 | #DCBBFD | Decorative borders, scrollbar thumb |
| brand-300 | #C393FA | Wave decoration strokes |
| brand-400 | #A366F0 | Gradient end, wave strokes |
| brand-500 | #8838DE | Logo gradient start, hover CTA |
| brand-600 | #6A12CD | Primary action: CTA buttons, links, badge text |
| brand-700 | #550FA5 | On-surface text (AA compliant) |
| brand-800 | #3B0B72 | Active CTA press state |
| brand-900 | #26064A | Sidebar background, dark surfaces |
| brand-950 | #170330 | Deepest dark |

## Canvas / Surface

| Token | Value | Usage |
|-------|-------|-------|
| canvas | #FCFAFD | Page background (brand-600 at ~2%) |
| paper-0 | #FFFFFF | Card backgrounds, hero |
| card-border | #F0EAF6 | Subtle card borders |

## Ink (Text)

| Token | Value | Usage |
|-------|-------|-------|
| ink-400 | #9A8FAE | Muted labels, sublabels |
| ink-500 | #6B5D82 | Secondary text, section labels |
| ink-600 | #4A3D62 | Body text secondary |
| ink-700 | #332848 | Body text |
| ink-800 | #1F1433 | Default body text |
| ink-900 | #0F0720 | Display headings, max contrast |

## Semantic

| Token | Value | Usage |
|-------|-------|-------|
| risk | #B42318 | Critical, Error, destructive |
| compliant | #15803D | Low, Compliant, Success |
| mitigated | #B45309 | Medium, Warning |

## Typography

| Role | Font | Size | Weight | Notes |
|------|------|------|--------|-------|
| Display | Source Serif 4 | 38-46px | 380-440 | Hero headings, KPI values |
| UI default | Inter | 13px | 520 | Nav items, body |
| UI active | Inter | 13px | 600 | Active nav, card titles |
| Label | Inter | 10-11px | 560 | Section headers, uppercase |
| Mono | JetBrains Mono | 10px | 400 | Kbd shortcuts, code |

## Spacing

- Grid: 8pt
- Nav item height: 36px
- Nav item margin: 1px 8px
- Divider margin: 6px 14px
- Section label padding: 8px 16px 3px
- Card padding: 20px 22px 16px

## Radius

| Token | Value |
|-------|-------|
| r-xs | 4px |
| r-sm | 6px |
| r-md | 8px (default) |
| r-lg | 12px (cards) |
| r-xl | 16px (hero) |
| r-full | 9999px (pills, avatars) |

## Hero

- Background: `linear-gradient(135deg, #FFFFFF 0%, #F7F0FF 40%, #EDDEFE 100%)`
- Border: `1px solid var(--brand-200)`
- Radius: 16px
- Heading: Source Serif 4, 38px, weight 440, ink-900
- Eyebrow: 10.5px, weight 560, uppercase, brand-600
- Wave decoration: brand-300/400 SVG strokes at varying opacities

## KPI Cards

- Background: paper-0
- Border: `1px solid var(--card-border)`
- Radius: 12px
- Label: uppercase, 10.5px, ink-500
- Value: Source Serif 4, 44px, weight 380, ink-900, tabular-nums
- Active card: 2.5px brand-600 bottom border
- Trend up: compliant (#15803D)
- Trend down: risk (#B42318)

## Pills

- Background: brand-50
- Text: brand-700
- Height: 20px
- Padding: 0 8px
- Radius: 9999px
- No border, no icon
