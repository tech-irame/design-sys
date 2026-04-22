# Sidebar Component — Editorial GRC

## Overview

Dark sidebar navigation panel. Background uses `brand-900` (#26064A) to anchor the brand identity. All content is white with varying opacity levels for hierarchy.

## Tokens

```css
--sidebar-bg:          var(--brand-900);    /* #26064A */
--sidebar-border:      rgba(255,255,255,0.08);
--sidebar-text:        rgba(255,255,255,0.85);
--sidebar-text-dim:    rgba(255,255,255,0.55);
--sidebar-text-muted:  rgba(255,255,255,0.4);
--sidebar-hover:       rgba(255,255,255,0.08);
--sidebar-active-bg:   rgba(255,255,255,0.08);
--sidebar-active-text: #FFFFFF;
--sidebar-active-bar:  #FFFFFF;
--sidebar-section:     rgba(255,255,255,0.55);
```

## Dimensions

| Property | Value |
|----------|-------|
| Width | 256px |
| Nav item height | 36px |
| Nav item font | 13px / weight 520 |
| Nav item active font | 13px / weight 600 |
| Section label font | 10px / weight 560 / uppercase / 0.08em tracking |
| Divider | 1px / rgba(255,255,255,0.08) / margin 6px 14px |
| Item margin | 1px 8px |
| Item padding | 0 14px |
| Item border-radius | 8px |

## Structure

```
sidebar (256px, brand-900 bg)
├── sb-logo
│   ├── sb-logo-icon (30x30, gradient brand-500→brand-400, rounded 8px)
│   ├── sb-logo-name (15px, weight 700, #FFFFFF)
│   └── sb-logo-sub (10.5px, weight 500, white/70%, with dropdown chevron)
│
├── sb-nav (scrollable)
│   ├── Ask IRA (12px, #FFFFFF, chat icon)
│   ├── Search (12px, #FFFFFF, search icon)
│   ├── Home (active state)
│   ├── Recents (clock icon)
│   ├── ── divider ──
│   ├── PROGRAMS (section label)
│   │   ├── Planning
│   │   ├── Process Hub
│   │   ├── Risk Register [14] (white badge with brand-600 text)
│   │   └── Control Library
│   ├── ── divider ──
│   ├── Dashboard
│   ├── Report
│   ├── Workflow Library
│   ├── AI Concierge
│   ├── ── divider ──
│   ├── Configuration
│   └── Admin
│
└── sb-footer
    └── sb-user (card: white/6% bg, white/8% border, rounded 8px)
        ├── sb-user-avatar (32x32, white bg, brand-600 text, weight 700)
        ├── sb-user-name (13px, weight 600, #FFFFFF)
        ├── sb-user-role (11px, white/55%)
        └── sb-user-more (three-dot icon, white/45%)
```

## Active State

- Background: `rgba(255,255,255,0.08)` — same as hover
- Text: `#FFFFFF` — full white
- Font weight: 600
- Left accent bar: 3px wide, `#FFFFFF`, flush left (`left: 0`), full height (`top: 0; bottom: 0`), `border-radius: 8px 0 0 8px`

## Logo Icon

- 30x30px, border-radius 8px
- Background: `linear-gradient(135deg, brand-500, brand-400)`
- Shadow: `0 2px 6px rgba(106,18,205,0.3)`
- Icon: Shield with cross (audit/GRC), 15x15px, white stroke

## User Profile Card

- Container: `rgba(255,255,255,0.06)` bg, `rgba(255,255,255,0.08)` border
- Avatar: 32x32, white bg, brand-600 text, weight 700, full rounded
- Hover: `rgba(255,255,255,0.10)` bg

## Badge (Risk Register count)

- Background: `#FFFFFF`
- Text: `var(--brand-600)`
- Font: 10.5px, weight 600
- Padding: 2px 7px
- Border-radius: 9999px (pill)

## Section Labels

- Font: 10px, weight 560
- Letter-spacing: 0.08em
- Text-transform: uppercase
- Color: `rgba(255,255,255,0.55)`
- Padding: 8px 16px 3px

## Dividers

- Height: 1px
- Color: `rgba(255,255,255,0.08)`
- Margin: 6px 14px
