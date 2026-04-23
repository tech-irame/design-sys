# DESIGN.md — Editorial GRC

A design system for a governance, risk, and compliance SaaS platform. Written
for AI coding agents (Claude, Cursor, Windsurf) and humans. Drop this file
into a project root and reference it when building UI.

> **North-star check**: "Would Anthropic ship this?" If a surface reads as
> calm, deliberate, and trustworthy — yes. If it reads busy, shouty, or
> corporate — redesign.

---

## 1. Visual Theme & Atmosphere

**Editorial GRC.** Serious but never stodgy. Precise, deliberate, quiet.
Two canvases by role: a cool near-white `#FCFAFD` for app chrome
(dashboards, data, workflows) and a warm `#FAF7F2` paper for long-form
reports — so narrative surfaces retain editorial character while the
working app reads modern and calm. A dark `brand-900` sidebar anchors
the shell. The brand purple (`#6A12CD`) is the signature, treated as a
real character beat — not a token accent and not a reason for decoration.

**Mood words**: editorial, precise, deliberate, data-first, quietly AI-native.

**What this is**:
- Long-form audit reports that feel like *The New Yorker* with a risk table.
- Dashboards that read as a newsroom CMS — dark chrome, cool canvas,
  serif numerics doing real work.
- AI responses that feel like a thoughtful analyst wrote them, not a chatbot.
- Data density as a feature, not a crisis.

**What this is not**:
- Enterprise navy. Glowing dark techy. Startup-cool gradient soup.
- Infographic pastels. Playful SaaS with rounded emoji mascots.
- Chat-bubble AI with avatar circles and "AI is typing…" skeuomorphism.
- 90s SaaS: thick borders, heavy shadows, gray-on-gray, all-caps banners.

**Voice of the UI**: sentence-case, confident, declarative. Say "Risk
assessment," not "RISK ASSESSMENT." Say "View all" not "VIEW ALL →".
Prefer short complete sentences over truncated labels. When a table column
header is a noun, it gets capitalized like a name ("Owner", "Severity").
When an empty state speaks, it speaks in full sentences — "No risks match
these filters. Clear filters or broaden your query." — not "Nothing here."

---

## 2. Color Palette & Roles

Colors are organized as **primitive → semantic → component**. Only touch
primitives when extending the system. Most UI should pull from semantic
tokens (e.g., `--color-surface`, `--color-text`, `--color-danger`).

### Brand purple (derived from `#6A12CD`)

| Token         | Hex       | Role                                                   |
|---------------|-----------|--------------------------------------------------------|
| `brand-50`    | `#F7F0FF` | Tinted surfaces, hover tiles                           |
| `brand-100`  | `#EDDEFE` | Pill background, info banner                           |
| `brand-200`  | `#DCBBFD` | Illustration accent, chart tint                        |
| `brand-300`  | `#C393FA` | Chart series on light mode                             |
| `brand-400`  | `#A366F0` | Hover on primary button                                |
| `brand-500`  | `#8838DE` | Secondary accent                                       |
| **`brand-600`** | **`#6A12CD`** | **Anchor — buttons, links, large display**     |
| `brand-700`  | `#550FA5` | **On-surface body text (AA-safe)**                     |
| `brand-800`  | `#3B0B72` | Pressed, dense-data accent                             |
| **`brand-900`** | **`#26064A`** | **Anchor — display ink, dark-mode surface**    |
| `brand-950`  | `#170330` | Dark-mode canvas base                                   |

> **Accessibility note**: `brand-600` on `paper-50` is ~4.0:1 — OK for large
> display and button backgrounds with white text, NOT for small body copy.
> For text on light surfaces use `brand-700` (~7.2:1). On the app `canvas`
> (`#FCFAFD`) `brand-600` gains a hair more contrast (~4.2:1) — same rule.

### App canvas (chrome surfaces)

The working app sits on a cool canvas — brand-600 laid over white at ~2%.
Cards on this canvas use a purple-tinted border (`canvas-border`) rather
than the warm paper border, so elevation reads as intentional, not
accidentally mismatched.

| Token             | Hex        | Role                                          |
|-------------------|------------|-----------------------------------------------|
| `canvas`          | `#FCFAFD`  | **App canvas** — dashboards, data views, workflows |
| `canvas-elevated` | `#FFFFFF`  | Cards, modals, popovers on canvas             |
| `canvas-border`   | `#F0EAF6`  | Card / divider on canvas (brand-600 at ~8% on white) |

### Warm neutrals ("paper & ink") — report surfaces

| Token       | Hex       | Role                                                   |
|-------------|-----------|--------------------------------------------------------|
| `paper-0`   | `#FFFFFF` | Cards on tinted surfaces (shared with `canvas-elevated`) |
| `paper-50`  | `#FAF7F2` | **Report canvas** — reader mode, PDFs, narrative long-form |
| `paper-100` | `#F3EEE5` | Subtle report surface, zebra banding                    |
| `paper-200` | `#E8E1D2` | Divider on warm surface                                |
| `paper-300` | `#D6CCB7` | Muted illustration baseline                            |
| `ink-300`   | `#C2B9CB` | Placeholder text                                       |
| `ink-400`   | `#9A8FAE` | Secondary text                                         |
| `ink-500`   | `#6B5D82` | Meta, caption                                          |
| `ink-600`   | `#4A3D62` | Body on tinted surface                                 |
| `ink-700`   | `#332848` | Strong body                                            |
| `ink-800`   | `#1F1433` | Headings                                               |
| `ink-900`   | `#0F0720` | Display, highest-contrast ink                          |

**Dark mode inverts**: app + report canvases unify to `#12081E`, ink
`#F1EDE3`, surfaces lifted with `brand-900` tints rather than pure black.
Paper tokens retain their warm hex values (they're only visible in printed
exports and in the light-mode reader).

### Sidebar (dark shell) — tokens

The sidebar is anchored to `brand-900` in every theme. All typography and
surface states compose from a white-opacity scale. **Do not use raw
`rgba(255,255,255, …)` literals in app code** — compose from these tokens
or add a new one through governance.

| Token                      | Value                         | Role                              |
|----------------------------|-------------------------------|-----------------------------------|
| `sidebar-bg`               | `brand-900` (`#26064A`)       | Sidebar canvas                    |
| `sidebar-border`           | `rgba(255 255 255 / 0.08)`    | Right divider, section rules      |
| `sidebar-text`             | `rgba(255 255 255 / 0.85)`    | Default nav label                 |
| `sidebar-text-dim`         | `rgba(255 255 255 / 0.55)`    | Section labels, subtitles         |
| `sidebar-text-muted`       | `rgba(255 255 255 / 0.45)`    | Menu affordances (⋯, chevron)     |
| `sidebar-surface`          | `rgba(255 255 255 / 0.06)`    | Profile card, inactive accent     |
| `sidebar-surface-hover`    | `rgba(255 255 255 / 0.08)`    | Nav item hover                    |
| `sidebar-surface-active`   | `rgba(255 255 255 / 0.12)`    | Nav item active (distinct from hover) |
| `sidebar-accent`           | `#FFFFFF`                     | Active left bar, logo mark, badge bg |

> **Active distinct from hover**: active background is `/ 0.12`, hover is
> `/ 0.08`. The 3px left accent bar and weight-600 label are redundant
> signals on top, not the only signals.

### Semantic (GRC-specific, not generic)

| Role         | Light     | Dark      | Usage                                       |
|--------------|-----------|-----------|---------------------------------------------|
| `risk`       | `#B42318` | `#F97066` | Critical severity, destructive actions      |
| `high`       | `#C2410C` | `#FB923C` | High severity                               |
| `mitigated`  | `#B45309` | `#FBBF24` | Mitigated risk, medium severity             |
| `compliant`  | `#15803D` | `#4ADE80` | Compliant, low severity, success            |
| `evidence`   | `#0369A1` | `#38BDF8` | Evidence links, citations, sources          |
| `info`       | `#6A12CD` | `#A366F0` | Informational, brand-adjacent notes         |
| `draft`      | `#6B5D82` | `#9A8FAE` | Draft, not-started, muted                   |

> **Rule**: never use pure red/amber/green. The custom GRC scale (crimson /
> burnt-orange / old-gold / moss) is colorblind-safer and doesn't read as
> consumer-web.

### Data-viz (8-color categorical, colorblind-safe)

Pick in order. Don't exceed 5 series on a single chart without explicit
design review.

1. `#6A12CD` brand violet
2. `#C2410C` burnt orange
3. `#0369A1` sky blue
4. `#15803D` moss green
5. `#B45309` old gold
6. `#9333EA` secondary violet
7. `#0891B2` cyan
8. `#B42318` crimson

**Diverging scale (risk heatmaps, 4-stop)**:
`#15803D → #FBBF24 → #C2410C → #B42318` (low → critical).

**Sequential scale (utilization, 5-stop)**:
`#F7F0FF → #DCBBFD → #A366F0 → #6A12CD → #3B0B72`.

**Data-viz accessibility** (full spec in §18):

- **Color is never the only channel.** Every chart encodes on at least
  two of: color · position · shape/pattern · text (value label or
  legend). Required combinations per chart type live in §18.1.
- **SVG charts** get a `role="img"` (or `role="group"` when
  interactive) + `aria-labelledby` pointing at the chart's `<figcaption>`.
- **Every chart** is accompanied by a `<details><summary>View as table</summary><table>…</table></details>`
  fallback — the `<table>` is the source of truth for screen readers.
- Under `prefers-contrast: more`, severity colors layer a pattern
  overlay (diagonal stripes for Critical, cross-hatch for High, etc.
  — see §18.4).

### Color opacity scale

Alpha tokens applied to ink or brand when semantic color alone is too loud
or when building overlays. Prefer solid discrete tokens (above) for most UI;
use opacity only when a solid token can't represent the need (disabled
states, modal scrims, row-hover tints, illustration layers).

| Token        | Alpha | Use                                                    |
|--------------|-------|--------------------------------------------------------|
| `alpha-100`  | 1.0   | Primary text, primary background, solid fills         |
| `alpha-80`   | 0.80  | Secondary text, subtle emphasis on primary tokens     |
| `alpha-50`   | 0.50  | Disabled text, muted foreground, muted border         |
| `alpha-20`   | 0.18  | Background tints, light surfaces, row hover, overlay  |
| `alpha-10`   | 0.10  | Extra-subtle hover tint, chart baseline, gridlines    |
| `alpha-scrim`| 0.40  | Modal/dialog backdrop behind overlays                 |

Compose as `var(--ink-900) / <alpha>` in Tailwind v4 (`text-ink-900/80`) or
`color-mix(in oklab, var(--ink-900) 80%, transparent)` in raw CSS.

---

## 3. Typography Rules

### Faces

| Role       | Default (OSS)          | Upgrade (paid, optional)       |
|------------|------------------------|--------------------------------|
| Display    | **Source Serif 4** Variable | Tiempos Headline, GT Sectra |
| Body / UI  | **Inter** Variable     | Söhne                          |
| Mono       | **JetBrains Mono** Variable | Söhne Mono, Berkeley Mono |

All faces are variable, self-hosted (or delivered through a font CDN with
subsetting). Tabular numerics are enabled globally on `.numeric` and inside
`<table>`, `<td>`, `<th>`.

### Scale (1.25 major-third, tuned — px / rem / line-height / letter-spacing / weight / face)

Root font-size is `16px`, so `1rem = 16px`. Use `rem` in code for
accessibility (respects user font-size preference); `px` listed here for
Figma / design-tool parity.

| Token         | Size px | Size rem | Line ht | Tracking  | Weight | Face       |
|---------------|---------|----------|---------|-----------|--------|------------|
| `display-2xl` | 72      | 4.500    | 1.05    | −0.03em   | 320    | Display    |
| `display-xl`  | 56      | 3.500    | 1.07    | −0.025em  | 380    | Display    |
| `display-lg`  | 44      | 2.750    | 1.10    | −0.020em  | 420    | Display    |
| `display-md`  | 36      | 2.250    | 1.15    | −0.015em  | 480    | Display    |
| `display-sm`  | 28      | 1.750    | 1.20    | −0.010em  | 520    | Display    |
| `heading-xl`  | 24      | 1.500    | 1.25    | −0.005em  | 600    | Inter      |
| `heading-lg`  | 20      | 1.250    | 1.30    |  0        | 600    | Inter      |
| `heading-md`  | 17      | 1.063    | 1.40    |  0        | 600    | Inter      |
| `heading-sm`  | 15      | 0.938    | 1.45    |  0.005em  | 620    | Inter      |
| `body-lg`     | 17      | 1.063    | 1.65    |  0        | 400    | Inter      |
| `body`        | 15      | 0.938    | 1.60    |  0        | 400    | Inter      |
| `body-sm`     | 13      | 0.813    | 1.55    |  0        | 440    | Inter      |
| `label`       | 12      | 0.750    | 1.30    |  0.02em (uppercase) | 560 | Inter |
| `code`        | 13      | 0.813    | 1.55    |  0        | 420    | JetBrains  |
| `code-sm`     | 12      | 0.750    | 1.50    |  0        | 460    | JetBrains  |
| `numeric`     | inherit | inherit  | inherit | (tabular) | 520    | Inter      |

### Rules

- **Serif is a character beat, not a default.** Use display-* only for
  narrative headers (reports, dashboards, AI responses, section hero).
  Primary page chrome, tables, and forms are all Inter.
- **All numbers in tables, KPIs, and risk figures** use `numeric` (tabular
  nums + Inter 520). Proportional digits are forbidden in data contexts.
- **Uppercase labels** are reserved for `label` token only — never apply
  `text-transform: uppercase` to anything else.
- **Line length cap**: body prose maxes out at 66ch; report reader mode
  goes to 72ch with a serif body option.

### Icon sizes

| Token       | Size px | Size rem | Stroke | Use                              |
|-------------|---------|----------|--------|----------------------------------|
| `icon-sm`   | 14      | 0.875    | 1.5px  | Compact rows, inline with `body-sm`, pills |
| `icon-md`   | 16      | 1.000    | 1.5px  | Default — buttons, inputs, tabs  |
| `icon-lg`   | 20      | 1.250    | 1.75px | Primary nav, page header, lg button |
| `icon-xl`   | 24      | 1.500    | 1.75px | Hero surfaces, empty-state illustration |
| `icon-2xl`  | 32      | 2.000    | 2px    | Marketing, onboarding            |

All icons are from [Lucide](https://lucide.dev), rendered as SVG with
`stroke-linecap: round` and `stroke-linejoin: round`. Never mix stroke and
filled icon libraries. Never tint icons with `fill` — use `color` and let
SVGs inherit `currentColor`.

---

## 4. Component Stylings

Components are **shadcn-themed** (Radix primitives + Tailwind v4). These are
the defaults; derivations should preserve tokens, not override them.

### Button

```
// Primary
height: 40px (md), 32px (sm), 48px (lg)
padding: 0 16px
radius: 8px
background: brand-600
color: paper-0
font: heading-md weight 600
transition: background 150ms standard, transform 75ms standard

hover   → brand-500
active  → brand-800, translateY(0.5px)
focus   → ring 4px brand-600/24 (glow-brand)
disabled→ brand-600/40, pointer-events: none
loading → spinner in paper-0, label preserved (not replaced)
```

**Variants**: `primary` (above), `secondary` (paper-0 bg, ink-800 text, 1px
`paper-200` border), `ghost` (transparent bg, ink-700 text, brand-50 hover),
`destructive` (risk bg, paper-0 text), `link` (text-only, brand-700,
underline on hover).

### Input / Textarea

```
height: 40px (md)
padding: 10px 12px
radius: 8px
background: paper-0
border: 1px paper-200
color: ink-900
placeholder: ink-300
font: body

hover   → border paper-300
focus   → border brand-600, ring 3px brand-600/20
error   → border risk, ring 3px risk/20
disabled→ background paper-100, color ink-400
```

Never use a shadow for input focus. The brand ring is the signal.

**The shadcn Form + RHF + Zod contract.** Any form over three fields
must use this pattern. It wins accessibility (label ↔ input ↔ message
association), type safety, and consistent server-error landing in one
surface. Full spec in §17.4 — the short version:

```tsx
<Form {...form}>
  <FormField
    control={form.control}
    name="riskId"
    render={({ field }) => (
      <FormItem>
        <FormLabel>Risk ID</FormLabel>
        <FormControl><Input {...field} /></FormControl>
        <FormDescription>Use the registry ID, not the display name.</FormDescription>
        <FormMessage />
      </FormItem>
    )}
  />
</Form>
```

Rules (full details §17.4):
- Always `FormLabel` (renders `<label htmlFor>`) — never placeholder-only.
- Always `FormMessage` for errors (renders with `role="alert"` and
  `aria-errormessage`). Custom validation text outside `FormMessage`
  does not announce.
- Always Zod schema via `zodResolver` — don't hand-roll validators.
- On submit failure, focus moves to the first invalid field; the form
  header gets a `role="alert"` summary listing the fields.

### Card

```
background: paper-0
border: 1px paper-200
radius: 12px
padding: 24px (default), 16px (compact)
shadow: none

hover (interactive cards only)
  → border paper-300, shadow sm
```

**Variants**: `outlined` (default above), `elevated` (shadow md, no border),
`muted` (paper-100 background, no border), `feature` (brand-50 background,
brand-200 border — for highlighted AI suggestions or KPIs).

### Table / DataGrid

```
typography: body-sm (compact) or body (comfortable)
row height: 32px compact, 44px comfortable
cell padding: 6px 12px (compact), 12px 16px (comfortable)
header: label token on paper-100, ink-600
zebra: alternating paper-50 / paper-100 (or off)
hover: row background paper-100
selected: row background brand-50, left border 2px brand-600
numeric cells: text-align right, numeric font
```

- Use sticky first column when >5 columns and horizontal scrolling is likely.
- Use column group headers for risk matrices (Q1 / Q2 / Q3 / Q4).
- Every table ships with a compact toggle; default is comfortable.

### Badge / Pill — no border, no icon

Pills are flat: tinted background + semantic text. **No border. No glyph.**
The text label itself is the source of truth (so colorblind users rely on
words, not icon/color).

```
height: 20px (sm), 24px (md), 28px (lg)
padding: 0 8px (sm), 0 10px (md), 0 12px (lg)
radius: 999px
font: label
background: [semantic]-50  (or alpha tint in dark mode)
color: [semantic]-700 on light / [semantic] on dark
border: none
```

Two taxonomies share the same style:

**Status pills** (generic, used for form validation, toasts, system banners):
`Default` (draft neutral), `Success`, `Error`, `Warning`, `Info`, `Disabled`.

**GRC severity pills** (domain-specific, for risk rows, findings, audit
results): `Critical`, `High`, `Medium`, `Low`, `Info`. Same visual treatment
as status pills — no border, no icon, strong label text.

Because no glyph distinguishes severity, **severity labels must always be
spelled out** (`Critical`, not `C`; `High`, not `H`). Charts and heatmaps
still carry redundant encoding (color + position + tooltip text).

### Dialog / Drawer

- Overlay: `ink-900` at 40% opacity + 4px backdrop-blur.
- Surface: paper-0, 16px radius, shadow xl, max-width 560px (md) or 720px (lg).
- Header: display-sm serif for narrative dialogs ("Delete audit?"), heading-md
  sans for task dialogs ("Edit control").
- Close button is a ghost icon-button, top-right, 16px from edge.

### AIResponse (signature pattern)

```
container: rounded-xl, 1px gradient border
  (linear-gradient 135deg, brand-600 0%, brand-400 50%, #E879F9 100% at 24% opacity)
background: paper-0 with brand-50 tint (rgba(106,18,205,0.03))
padding: 24px
min-height: 120px

header: optional meta row — "Answered in 1.2s · 4 sources"
body: body-lg, ink-800, 66ch max
citations: mono code-sm inside brand-50 pills, clickable to source
tool calls: collapsible section, mono code-sm, monospace grid
streaming cursor: 2px wide, brand-600, blinking at 1.2s cycle
thinking dots: three brand-400 dots, pulsing spring easing, 900ms stagger
```

The AIResponse is **not a chat bubble**. No avatar. No "AI said" tag.
It's presented as considered prose with citations. Think: a column in a
well-designed news app. If multiple responses stack, separate with a
16px paper-200 rule, not a new bubble.

### Empty state

- Illustration optional; if present use `paper-300` linework only (no color).
- Title: heading-lg serif if the surface is narrative, heading-md sans
  otherwise.
- Body: body, ink-500, 2 sentences max.
- CTA: secondary button for the primary action.

### Skeleton (loading placeholder)

```
background: paper-100 (light) / ink-700 (dark)
radius: inherit from the element it stands in for
       (text skeleton r-sm; avatar skeleton r-full; card skeleton r-lg)
animation: shimmer — linear-gradient sweeps left→right, 1.6s cubic-bezier
           (0.4, 0, 0.2, 1), infinite. Disabled under `prefers-reduced-motion`.
aria: wrap in <div role="status"><span className="sr-only">Loading …</span></div>
```

**When to skeleton vs spin**:

- **Skeleton** for any surface larger than a button — cards, rows,
  tiles, charts, chat messages, artifact panels.
- **Spinner** only inside a button, input, or an inline `16–20px`
  status marker.
- **Never** skeleton for <150ms expected loads — the flicker is worse
  than nothing.

See §10.14 for sizes.

---

## 5. Layout Principles

### Grid

- 8pt base, 4pt sub-grid allowed for icon-aware alignments.
- Content container: 1200px max for dashboards, 960px for reports (reader
  mode), 1440px for data-heavy tables.
- Column gaps: 24px on dashboards, 16px on compact tables, 32px on reports.

### Spacing scale

`0, 2, 4, 6, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128` (px).
Everything snaps to this. Never introduce a new step without governance.

### Density

- **Comfortable** (default): row 44px, cell pad 12/16px, body type.
- **Compact**: row 32px, cell pad 6/12px, body-sm type.
- Density is a user preference, stored in `localStorage`. Density toggle
  lives in the sidebar logo-row kebab menu (global) OR per-table toolbar
  (local override). Every table, data grid, and list supports both — not
  a feature of the component.

### App shell

- Left sidebar (256px expanded, 64px collapsed). Collapses at <1024px.
- No top header bar — global chrome lives in the sidebar; page context
  lives in the first row of each page.
- Content panel: `canvas` (`#FCFAFD`), **32px page padding** (8pt grid).
- First content row: page header (see `Page header` below).

### Sidebar

Dark shell anchored to `brand-900`. All typography and surface states
compose from the `sidebar-*` tokens defined in §2. **Do not write raw
white-alpha literals** in app code.

```
width: 256px (expanded) · 64px (collapsed at <1024px)
background: var(--sidebar-bg)
border-right: 1px var(--sidebar-border)
display: flex · column · full height
```

**Structure** (top → bottom):

1. **Logo row** — 30×30 mark (linear-gradient `brand-500 → brand-400`,
   radius 8, `shadow-sm` tinted with `brand-600 / 0.30`), wordmark
   `heading-sm` (15px/700) in `sidebar-accent`, subtitle 10.5px/500 in
   `sidebar-text-dim` with dropdown chevron in `sidebar-text-muted`.
   Bottom border 1px `sidebar-border`. Padding 18px 16px 16px.

2. **Top actions** — "Ask IRA" (chat icon), "Search" (search icon).
   `.sb-item` treatment. 12px, `sidebar-accent` text.

3. **Primary nav** — Home (active), Recents. Standard `.sb-item`.

4. **Programs group** — section label "PROGRAMS" (10px/560, uppercase,
   0.08em tracking, `sidebar-text-dim`). Sub-items: Planning, Process
   Hub, Risk Register (with white pill badge `14` — `sidebar-accent` bg,
   `brand-600` text), Control Library.

5. **Main nav** — Dashboard, Report, Workflow Library, AI Concierge.

6. **Bottom nav** — Configuration, Admin.

7. **User profile** — card container `sidebar-surface` bg +
   `sidebar-border` 1px. Avatar 32×32 `sidebar-accent` bg, `brand-600`
   text, weight 700. Name 13px/600 `sidebar-accent`. Role 11px
   `sidebar-text-dim`. Menu affordance (⋯) `sidebar-text-muted`.

**Nav item (`.sb-item`) — default**:
```
height: 36px
padding: 0 14px
margin: 1px 8px
radius: 8px
font: 13px Inter, weight 520
color: var(--sidebar-text)          /* 85% white */
transition: background 150ms standard
```

**Hover**:
```
background: var(--sidebar-surface-hover)  /* 8% white */
color: var(--sidebar-accent)              /* 100% white */
```

**Active** — distinct from hover (no ambiguity):
```
background: var(--sidebar-surface-active) /* 12% white */
color: var(--sidebar-accent)              /* 100% white */
font-weight: 600
left accent bar: 3px, var(--sidebar-accent), top:0 bottom:0 left:0
  border-radius: 8px 0 0 8px
```

**Dividers**: 1px `sidebar-border`, margin 6px 14px.

**Badge** (e.g., Risk Register count): `sidebar-accent` bg, `brand-600`
text, 10.5px/600, padding 2px 7px, pill-radius.

### Page header — topbar replacement

With no topbar, each page owns its own header as the **first content row**.
This isolates dashboard chrome from report chrome from registry chrome,
and lets long-form narrative pages skip it entirely and flow straight
into a hero.

**Structure** (left → right, in one flex row):

- **Breadcrumb** — `Programs · Risk Register · Operational` (`body-sm`,
  `ink-500`, `/ ` separator in `ink-300`). Collapses middle segments to `…`
  at ≥4 items (see §10.7).
- **Title** — `display-sm` serif for narrative pages (reports, dashboards);
  `heading-xl` sans for registry/task/settings pages.
- **Context chips** (optional) — period, status, owner. Flat pills:
  `brand-50` bg + `brand-700` text, dismissible via chevron or ×.
- **Page actions** (right-aligned) — export / filter / primary CTA. Max 3
  visible; overflow to a `ghost` dropdown (⋯).

**Size**: 72px tall on dashboards (serif title breathes), 56px on registry
/ task pages. Sticky below `lg` when the page scrolls.

**Bottom rule**: 1px `canvas-border`. Narrative pages (reports,
AI-Concierge responses) omit the rule and flow straight into the hero.

**What moved where** (topbar → new home):

| Old topbar slot   | New home                                        |
|-------------------|-------------------------------------------------|
| Brand logo        | Sidebar logo row                                |
| ⌘K global search  | Sidebar "Search" top action                     |
| Notifications     | AI Concierge inbox · inline page banners        |
| User avatar       | Sidebar user profile card (bottom)              |
| Breadcrumbs       | Page header (first content row)                 |
| Page title        | Page header                                     |
| Page actions      | Page header (right-aligned)                     |
| Context switcher  | Page header context chips OR sidebar dropdown   |
| Density toggle    | Sidebar logo-row kebab OR per-table toolbar     |

### Report reader

- 960px max-width container, `paper-50` canvas.
- Body column: 66ch width, centered.
- Serif body option toggled per reader preference — remembers across reads.
- Section headers: display-md serif, 80px top margin, 24px bottom.
- First paragraph of section 1 gets a drop-cap (3 lines tall, Source Serif
  weight 320, `brand-700`).

### Dashboard

- 12-column grid at ≥1280px, 8-column at ≥768px, stack below.
- KPI tiles span 3 columns (12-col) or 2 (8-col).
- Primary chart card spans 8 or full-width; secondary charts 4 wide.
- AI Q&A surface is always accessible from ⌘K or a sticky bottom-right FAB
  — never the only way to reach it.

---

## 6. Depth & Elevation

Elevation is expressed through **borders first, shadows sparingly, tint
never**. Cards sit on paper; they don't float on air.

| Level   | Use                             | Definition                                               |
|---------|--------------------------------|----------------------------------------------------------|
| `z-0`   | Canvas                         | No border, no shadow                                     |
| `z-1`   | Card resting                   | 1px `paper-200` border, no shadow                        |
| `z-2`   | Card hover / interactive       | 1px `paper-300` border, `shadow-sm`                      |
| `z-3`   | Popover, dropdown              | No border, `shadow-md`, brand-50 focus ring when active  |
| `z-4`   | Dialog, drawer                 | `shadow-xl`, overlay behind                              |
| `z-5`   | Toast                          | `shadow-lg`, auto-dismiss 5s default                     |
| `z-6`   | Command palette                | `shadow-xl`, brand-100 top-border hairline               |

Shadows — decomposed (x / y / blur / spread / color), DTCG composite form
for direct Tokens Studio → Style Dictionary ingestion:

| Token         | X    | Y    | Blur | Spread | Color                       | Notes               |
|---------------|------|------|------|--------|-----------------------------|---------------------|
| `shadow-xs`   | 0    | 1    | 0    | 0      | `rgb(15 7 32 / 0.04)`       | Hairline underline  |
| `shadow-sm.1` | 0    | 1    | 2    | 0      | `rgb(15 7 32 / 0.05)`       | Soft drop           |
| `shadow-sm.2` | 0    | 0    | 0    | 1      | `rgb(15 7 32 / 0.03)`       | Ring                |
| `shadow-md.1` | 0    | 4    | 12   | 0      | `rgb(15 7 32 / 0.06)`       | Soft lift           |
| `shadow-md.2` | 0    | 1    | 2    | 0      | `rgb(15 7 32 / 0.05)`       | Contact             |
| `shadow-lg.1` | 0    | 12   | 32   | 0      | `rgb(15 7 32 / 0.08)`       | Float               |
| `shadow-lg.2` | 0    | 4    | 12   | 0      | `rgb(15 7 32 / 0.05)`       | Contact             |
| `shadow-xl.1` | 0    | 24   | 48   | 0      | `rgb(15 7 32 / 0.12)`       | Modal               |
| `shadow-xl.2` | 0    | 12   | 24   | 0      | `rgb(15 7 32 / 0.06)`       | Contact             |
| `glow-brand`  | 0    | 0    | 0    | 4      | `rgb(106 18 205 / 0.24)`    | Focus only          |

Composite tokens layer two shadows (`.1` + `.2`) — in DTCG and CSS this is
a single `box-shadow` value with comma-separated layers. Style Dictionary
emits them accordingly.

Dark mode override:

| Token         | X    | Y    | Blur | Spread | Color                     |
|---------------|------|------|------|--------|---------------------------|
| `shadow-*`    | (same geometry) | | | | `rgb(0 0 0 / 0.40)` at all levels |
| `inset-lift`  | 0    | 1    | 0    | 0      | `rgb(255 255 255 / 0.04)` |

Dark-mode cards also carry the `inset-lift` token as an inset shadow so
surfaces remain perceptible against near-black.

---

## 7. Do's and Don'ts

### Do

- **Use serif for narrative hierarchy.** Report hero, dashboard hero, AI
  response header, section breaks in long-form content.
- **Use tabular nums on every number.** Risk scores, KPIs, table cells,
  audit findings counts.
- **Use explicit label text for severity.** Never rely on color alone.
  `Critical` / `High` / `Medium` / `Low` are always spelled out. Charts
  add position/tooltip as redundant encoding beyond color.
- **Snap to the 8pt grid.** If something needs 14px, use 12 or 16.
- **Reserve `brand-600` for signal.** Primary buttons, selected state,
  focus ring, links. Don't paint containers with it.
- **Write UI copy in full sentences** with a period. "No results match
  these filters." — not "No results."
- **Prefer borders to shadows** for card elevation. Shadow only when you
  need genuine spatial lift (popovers, dialogs, toasts).
- **Respect `prefers-reduced-motion`.** Replace all motion with opacity-only
  or instant transitions.
- **Ship compact density.** Every table must work at row-height 32. Power
  users live there.
- **Show AI thinking honestly.** Pulse dots during generation; cursor while
  streaming; timestamp when done. Don't fake streaming on static text.
- **Add `cursor: pointer`** to every clickable surface — cards, rows,
  pills-as-filters, file uploads. The pointer is a promise. `<button>`
  and `<a>` already carry it; manual `onClick` handlers don't.
- **Label every icon-only button** with `aria-label`. The Lucide icon
  gets `aria-hidden="true"`. See §17.2 for the full ARIA table.
- **Reach for the native element first.** `<button>`, `<a>`, `<nav>`,
  `<main>`, `<table>`, `<label for>` — before any `div` + `role`.
- **Skeleton anything larger than a button.** Spinners inside buttons
  and tiny inline status markers; skeletons for cards, rows, tiles,
  charts, chat messages. See §10.14.

### Don't

- **Don't use pure red/amber/green for severity.** Use the custom GRC
  scale (crimson / burnt-orange / old-gold / moss) — colorblind-safer and
  doesn't read as consumer-web.
- **Don't put the brand purple on body text over light.** It's
  borderline-AA. Use `brand-700` for text; reserve `brand-600` for
  backgrounds and large display.
- **Don't use emoji in UI copy.** Use Lucide icons.
- **Don't use drop-shadows decoratively** on cards, buttons, or sidebars.
  Shadow is for true lift (popovers, dialogs), not for "making things pop."
- **Don't animate for decoration.** Motion is a state-transition signal.
  No hover-bounce. No scroll-reveals. No marquee.
- **Don't stack more than three brand colors on a screen.** More than
  three reads as loud.
- **Don't center body paragraphs.** Left-aligned or justified (for reports).
  Centered is for hero moments only.
- **Don't use tooltips to hide critical information.** If a value needs
  explaining, explain it inline.
- **Don't write "AI is typing…".** That's chatbot clutter. Use the pulse
  indicator and move on.
- **Don't create a new component when a primitive composed does the job.**
  A "RiskPill" is just a `Badge` with a severity variant.
- **Don't shift layout on hover.** Transition `color`, `background`,
  `border`, `box-shadow`, `opacity` — never `width`, `height`,
  `padding`, `margin`, or `scale` that changes layout. Sibling
  elements must not move when one is hovered.
- **Don't use `outline: none` without replacement.** If you need to
  remove the default outline (because you're drawing your own focus
  ring), you own the replacement. `focus-visible:ring-…` from the
  glow-brand token is the default.
- **Don't raw `z-index`.** Every z-index must resolve to a token from
  §17.7. No `z-[9999]`, no `z-50` sprinkled on a card.
- **Don't reach for `div role="button"`** when `<button>` exists.
  `role` is a fallback, not a first choice. See §17.1.
- **Don't disable the submit button to "hint" at validation.** Let it
  submit, catch the errors, focus the first invalid field. Disabling
  hides *why* the user can't continue.

---

## 8. Responsive Behavior

### Breakpoints

| Name  | Min width | Typical device          |
|-------|-----------|-------------------------|
| `sm`  | 640px     | Large phone (landscape) |
| `md`  | 768px     | Tablet                  |
| `lg`  | 1024px    | Small laptop            |
| `xl`  | 1280px    | Desktop                 |
| `2xl` | 1536px    | Large desktop           |

### Rules

- **Sidebar** collapses to icon-only at `<lg` (1024px). Below `md` it
  becomes a drawer summoned from a menu button.
- **Page header** (the topbar replacement) keeps breadcrumb, title, and
  primary action above `md`. Below `md`, breadcrumb collapses to a
  back-chevron; context chips fold into an overflow sheet opened from
  an (⋯) icon-button.
- **Dashboards** stack to a single column below `md`. KPI tiles go 2-per-
  row below `md`, full-width below `sm`.
- **Tables** gain a horizontal scroll region below `lg` with the first
  column sticky. Below `md`, offer a "view as cards" toggle and show each
  row as a card for scannability.
- **Reports** reduce max-width to 100% below `md` with 16px padding.
  Drop-cap disables below `sm`.
- **AI Q&A**: at `≥lg`, right-side panel (480px). At `<lg`, full-screen
  sheet (bottom-up on mobile).
- **Touch targets**: minimum 44×44px on all interactive elements below
  `md`. Use `py-2.5` minimum on buttons.
- **Typography**: display-2xl scales to display-xl at `<md`, display-xl
  to display-lg, and so on down one step. Body sizes don't change.

---

## 9. Agent Prompt Guide

### Quick reference

- **App canvas** (dashboards, data, workflows): `#FCFAFD` (light), `#12081E` (dark).
- **Report canvas** (narrative reader, PDFs): `#FAF7F2` (light), `#12081E` (dark).
- **Sidebar** (always dark, every theme): `#26064A` (`brand-900`). Text `rgba(255,255,255,0.85)`, dim `/0.55`, muted `/0.45`. Hover bg `/0.08`, active bg `/0.12`, accent `#FFFFFF`.
- **Page header replaces topbar**: breadcrumb → title (`display-sm` serif on narrative pages, `heading-xl` sans on task/registry) → context chips → right-aligned actions. 32px page padding.
- **Primary button**: `background: #6A12CD; color: #FFFFFF; height: 40px; radius: 8px; font: Inter 600 15px`.
- **Body text on canvas**: `color: #1F1433` (ink-800). Never pure black.
- **Link**: `color: #550FA5` (brand-700), underline on hover only.
- **Focus ring**: `0 0 0 4px rgba(106, 18, 205, 0.24)`.
- **Card on app canvas**: `background: #FFFFFF; border: 1px solid #F0EAF6; radius: 12px; padding: 24px`.
- **Card on report canvas**: same geometry, border `#E8E1D2` (`paper-200`).
- **Serif display**: `font-family: "Source Serif 4", Georgia, serif; font-weight: 420; letter-spacing: -0.02em`.
- **Mono**: `font-family: "JetBrains Mono", "SF Mono", Consolas, monospace`.

### Ready-to-use prompts

**"Build me a risk summary card"**
```
Card (outlined variant), 320×220px.
Header row: label "ENTERPRISE RISK" (Inter 560, 12px, uppercase, ink-500).
Metric: display-lg serif "78" in ink-900, followed by " / 100" in ink-400
(inline, subdued).
Trend row: "↑ 12%" in compliant-700 with arrow icon.
Severity breakdown: four horizontal rows with severity pill + count,
  aligned right.
Footer CTA: "View all risks →" as link-variant button, brand-700.
```

**"Build me an AI response card"**
```
Container: rounded-xl, 1px gradient border
  (linear-gradient 135deg, #6A12CD, #A366F0, #E879F9 at 24% opacity),
  background #FFFFFF with rgba(106,18,205,0.03) tint, 24px padding.
Meta row: "Answered in 1.2s · 4 sources" in ink-500 body-sm, then 8px gap.
Body: body-lg (17px Inter 400 line-height 28), max 66ch.
Citations: inline pills, mono code-sm (13px JetBrains 420), brand-50 bg,
  brand-700 text, 4px radius, clickable.
Tool calls: collapsible panel below body, mono, paper-100 background.
```

**"Build me a compliance dashboard header"**
```
Section: py-32 px-32, canvas (#FCFAFD).
Left column:
  label (uppercase caption): "Q1 2026 · Operational Risk".
  display-xl serif title: "Operational Risk Assessment".
  body-lg ink-600 intro paragraph, max 66ch:
    "A review of control effectiveness across 14 business units, with
     findings prioritized by impact and remediation velocity."
Right column (auto-aligned): KPI tiles — Risk Score, Open Findings,
  Control Coverage, Last Audit.
Below: 12-col grid of charts and tables.
```

**"Build me a pill"** (status or severity — same visual treatment)
```
Height 24px (md) or 20px (sm) or 28px (lg).
Radius 999px. Padding 0 10px (md).
Font: label (12px Inter 560, uppercase, tracking 0.02em).
Background: [semantic]-50 tint (e.g., #FEECEB for error/critical).
Color: [semantic]-700 (e.g., #8F1A12 for error/critical) on light mode.
Border: NONE. Icon: NONE.
Label: full word — "Critical", "Success", "Error", "Info" — never abbreviated.
```

**"Build me a data table"**
```
Full-width TanStack Table. Header in label token on paper-100.
Row: 44px height comfortable or 32px compact (user preference).
Zebra banding: paper-50 / paper-100.
Hover: row background paper-100. Selected row: brand-50 background,
  2px brand-600 left border.
Numeric columns: text-align right, numeric font (tabular).
Sort glyph: Lucide ChevronUp/Down in ink-500, next to active column header.
Filter bar: sticky top of table, paper-0 bg, 1px paper-200 bottom border.
Pagination: right-aligned, "1–50 of 142 · ‹ ›".
```

**"Build me the IRA three-panel chat page"** — see §12.1
```
Layout: sidebar (app shell) + history panel (280) + conversation (flex)
        + artifact panel (420–520 collapsible).
History panel: paper-0 bg inside the canvas, 1px paper-200 right border,
  [+ New Chat] primary button sticky top, Pinned group, then Today /
  Yesterday / Last 7 days / Earlier. Each session row 56px.
Conversation: user message = "You" label + body-lg, no bubble.
  IRA message = AIResponse (§4) with gradient border. Clarifications
  render inline as secondary-variant chips.
Input bar: 72px, paper-0 bg, 1px paper-200 top border, Paperclip +
  textarea + Send (⌘↵).
Artifact panel: fixed tabs in order — Plan · Code · Sources · Result.
  Only show tabs with content. Sticky footer action row.
```

**"Build me the risk register"** — see §13.2.4
```
Page header (§5): breadcrumb "Governance › Risk Register", heading-xl
  sans title, page actions "+ Add risk" (primary) + "Export" (ghost) +
  "Heatmap" (secondary, opens side panel).
Filter bar (§11.4): search + severity chips + owner + process + status
  + advanced.
AI banner (once): brand-50 bg, Sparkles icon, "IRA found 4 new risks
  since your last review." + View secondary button.
Data table: columns ID (mono R-0087) · Title · Process · Severity
  (pill spelled out) · Likelihood · Impact · Score (tabular) · Owner
  · Status. 44px comfortable rows. Selected row: brand-50 bg + 2px
  brand-600 left border.
Detail: slide-over editor (§15.7), 720px, tabs Overview · Controls ·
  Evidence · Audit trail.
```

**"Build me the command palette"** — see §11.1
```
Overlay: ink-900/0.40 + 4px backdrop-blur.
Container: 640px, r-xl, paper-0 bg, shadow-xl + 1px brand-100 top
  hairline.
Input: 56px, Search icon 20px ink-500 left, body-lg ink-900, placeholder
  "Search risks, controls, reports… or ask IRA anything."
Sections (dividers 1px paper-200): Pages · Entities · Ask IRA (always
  last). Each starts with a label-token section header.
Ask IRA row: Sparkles icon, "Ask IRA: <query>" body-lg brand-700,
  right-pointing chevron. Promotes above Entities when query is NL-ish.
Footer: 36px paper-50 bg, body-sm ink-500, "↵ to open · ⌘↵ new tab · esc".
```

**"Build me the workflow library card"** — see §13.4.1
```
Card (outlined), 280×200, r-lg.
Icon tile 40×40 r-md brand-50 bg + brand-600 Lucide icon.
Title heading-sm, 2-line clamp.
Description body-sm ink-600, 3-line clamp.
Meta row: category pill (flat) + "Used 143 times" body-sm ink-500.
Hover: shadow-sm, border paper-300.
```

**"Build me a finding row"** — see §13.3.4
```
Data row height 44px. Columns:
  ID (mono F-0321, ink-500) · Severity pill (spelled out) · Title
  (body weight 540, 1-line clamp) · Source pill (Test / AI / Manual) ·
  Status (Open / Remediation / Closed / Accepted risk) · Owner (avatar
  + name) · Due (tabular date) · Days open (tabular).
Row click: opens right slide-over (§15.7) 720px with AI-authored
  narrative body if source=AI (AIResponse style, no chat bubble),
  remediation mini-kanban, evidence links, linked entities as
  EntityChips (§15.2).
```

**"Build me the AI progressive loader"** — see §12.5
```
One row below the user message. Steps stack vertically with 4px gap:
  ●○○  Understanding query…         (pending, body ink-400)
  ●●○  Planning analysis…           (active, body weight 540 ink-900,
                                     3 brand-600 dots staggered 400ms)
  ✓   Writing code…                 (done, strike-through ink-500,
                                     14px CheckCircle2 compliant)
On completion collapse the whole block to a single body-sm ink-500
meta line: "Answered in 3.1s · 2 steps · 847 rows" — which becomes
the AIResponse (§4) header.
```

### Refusal list

If a generated UI includes any of the following, redo it:

- Pure `#FF0000`, `#FFA500`, `#00FF00` — use the GRC semantic scale.
- Drop-shadow on a button.
- `text-transform: uppercase` on anything other than `label` token.
- Emoji in UI copy (🎉, 👋, 🚀, etc.).
- Truncated labels with `...` when full text fits.
- Centered body paragraphs outside of hero moments.
- A chat-bubble AI response with avatar circle.
- Pastel gradients used as backgrounds on content cards.
- Pure black `#000000` for text or backgrounds.
- **Pills with borders or icons/glyphs** — pills are flat: tint + label.
- **Abbreviated severity labels** (`C`, `H`, `M`, `L`) — always spelled out.

### When to deviate

The design system is opinionated, not dogmatic. Deviate when:

- The user-experience cost of strict adherence exceeds the consistency benefit.
- A domain requirement (regulatory color coding, auditor convention) demands
  a specific signal.
- An accessibility need surpasses the system's default (e.g., AAA on
  public-sector reports).

Document the deviation in the component's JSDoc so the next agent sees why.

---

## 10. Component State Reference

Exhaustive per-component state matrices, sizes, and composition variants.
Keep this section authoritative when building React components; the shorter
stylings in §4 are summaries.

Every component inherits the global focus ring (`glow-brand`) and respects
`prefers-reduced-motion`. Every disabled state drops to 50% alpha of its
default label/fill and disables pointer events.

### 10.1 Button

**Sizes** (px / rem):

| Size | Height | Padding X | Min-width (icon-only) | Font      | Icon  | Radius |
|------|--------|-----------|------------------------|-----------|-------|--------|
| sm   | 32 / 2.00    | 12 / 0.75 | 32 / 2.00 | `body-sm` (13) | `icon-sm` (14) | `r-md` (8) |
| md   | 40 / 2.50    | 16 / 1.00 | 40 / 2.50 | `heading-md` (15 / 600) | `icon-md` (16) | `r-md` (8) |
| lg   | 48 / 3.00    | 20 / 1.25 | 48 / 3.00 | `heading-md` (17 / 600) | `icon-lg` (20) | `r-md` (8) |

Icon-only buttons are square (`height × height`). Icon-with-label gap: 8px.

**Variants × states** (all states): `default`, `hover`, `focus`, `active`,
`loading`, `disabled`.

| Variant     | Default                                           | Hover                     | Active                 | Disabled                     |
|-------------|---------------------------------------------------|---------------------------|------------------------|------------------------------|
| primary     | bg `brand-600`, text `paper-0`                   | bg `brand-500`            | bg `brand-800`, ty+0.5 | bg `brand-600/50`, text `paper-0/70` |
| secondary   | bg `paper-0`, text `ink-800`, border `paper-200` | border `paper-300`, bg `paper-50` | bg `paper-100`   | bg `paper-100`, text `ink-400`, border `paper-200` |
| ghost       | bg transparent, text `ink-700`                   | bg `brand-50`, text `brand-700` | bg `brand-100`    | text `ink-400`               |
| destructive | bg `risk`, text `paper-0`                        | bg `#9B1E14`              | bg `#7A1710`           | bg `risk/50`                  |
| link        | text `brand-700`                                  | text `brand-800`, underline | text `brand-900`    | text `ink-400`                |

Focus: all variants add `glow-brand` ring (4px `brand-600/24`).
Loading: spinner (16/20/24px by size) in fg color; label stays visible;
pointer-events disabled.

**Icon placement variants**:
- `icon-left`: `[icon 16px] [label]` with 8px gap
- `icon-right`: `[label] [icon 16px]` with 8px gap
- `icon-only`: square, aria-label required
- `none`: text only

### 10.2 Checkbox & Radio

**Size**: 16×16 (`1rem`) checkbox. 16×16 radio (round). Stroke 1.5px, radius
`r-xs` (4) for checkbox, `full` for radio.

| State     | Checkbox                                                        | Radio                                           |
|-----------|------------------------------------------------------------------|-------------------------------------------------|
| default   | border `paper-300`, bg `paper-0`                                 | border `paper-300`, bg `paper-0`                |
| hover     | border `ink-400`                                                 | border `ink-400`                                |
| focus     | + `glow-brand` ring                                              | + `glow-brand` ring                             |
| checked   | bg `brand-600`, border `brand-600`, check glyph `paper-0` 1.5px | bg `paper-0`, border `brand-600`, inner dot 6px `brand-600` |
| indeterminate | bg `brand-600`, border `brand-600`, dash glyph                | (n/a)                                           |
| disabled  | bg `paper-100`, border `paper-200`, opacity 50%                 | bg `paper-100`, border `paper-200`, opacity 50%|
| error     | border `risk`, bg `risk/10`                                      | border `risk`, bg `risk/10`                     |

Label sits to the right, 8px gap, `body` size, `ink-800` color. Helper/error
text below label at `body-sm`, `ink-500` (helper) or `risk` (error).

### 10.3 Dropdown (menu)

Dropdown is an action menu (user menu, row-actions, overflow). Built on
Radix `DropdownMenu`.

**Trigger** — any button variant; common pattern is `ghost` + `icon-only`
(three-dot menu) or `secondary` + `icon-right` (⌄ chevron).

| State    | Trigger                                    | Menu surface                                     | Item                                  |
|----------|--------------------------------------------|--------------------------------------------------|---------------------------------------|
| default  | `ghost` button default                      | hidden                                           | (n/a)                                 |
| focus    | + `glow-brand` ring                         | hidden                                           | (n/a)                                 |
| open     | bg `brand-50`, text `brand-700`             | `paper-0` bg, `r-lg`, `shadow-md`, 4px pad       | `body` text, 8×12 pad, `r-sm`         |
| selected | —                                           | —                                                | bg `brand-50`, text `brand-700`, `check` icon right |
| disabled | opacity 50%, pointer events off             | —                                                | text `ink-400`, pointer events off    |

Menu min-width 192px, max-width 320px. Items have 32px min-height. Group
headers use `label` token. Separator 1px `paper-200`.

### 10.4 Select (form field)

Select is a single-choice form input. Built on Radix `Select`.

| State    | Trigger (the field)                                             | Popover                                        | Option                              |
|----------|-----------------------------------------------------------------|------------------------------------------------|-------------------------------------|
| default  | 40px h, border `paper-200`, text `ink-900`, chevron-down right | hidden                                         | (n/a)                               |
| focus    | border `brand-600`, ring `brand-600/20` (3px)                   | hidden                                         | (n/a)                               |
| open     | border `brand-600`, chevron rotates 180°                         | `paper-0`, `r-md`, `shadow-md`, max-h 320, scroll | highlighted row uses `brand-50` bg |
| filled   | text `ink-900`, border `paper-200`                              | —                                              | —                                   |
| selected | check icon (optional) + highlighted row                          | —                                              | bg `brand-50`, text `brand-700`    |
| error    | border `risk`, ring `risk/20`                                    | —                                              | —                                   |
| disabled | bg `paper-100`, text `ink-400`, border `paper-200`               | —                                              | —                                   |

Placeholder: `ink-300` text. When empty, show placeholder; when set, show
value in `ink-900`.

### 10.5 Date picker

Single date + range variants. Built on Radix `Popover` + `react-day-picker`
(or `@internationalized/date` if we need full locale rigor).

| State    | Trigger input                                             | Popover calendar                                                   |
|----------|-----------------------------------------------------------|--------------------------------------------------------------------|
| default  | same as Select trigger, shows `Select date` placeholder   | hidden                                                             |
| open     | border `brand-600`                                         | `paper-0` surface, `r-lg`, `shadow-lg`, 16px pad                  |
| selected | text `ink-900` with formatted date (`Apr 28, 2026`)        | selected day: `brand-600` bg, `paper-0` text, `r-md`               |
| range    | `Apr 28 → May 10, 2026`                                    | range: `brand-50` bg between endpoints, endpoints `brand-600`      |
| disabled | bg `paper-100`, text `ink-400`                             | disabled dates: `ink-300`, struck-through on hover                 |
| today    | —                                                          | ring `brand-600/30` around the current day                          |

Calendar cell: 32×32, `body-sm` numeric, hover `paper-100`. Month nav:
`ghost` icon-button `ChevronLeft`/`ChevronRight`. Year select: `Select`
pattern embedded in header.

### 10.6 Tabs

Underline tabs (primary pattern) and segmented tabs (secondary pattern).

**Underline tabs**:

| State    | Tab                                                            |
|----------|----------------------------------------------------------------|
| default  | text `ink-600`, 2px transparent bottom border                 |
| hover    | text `ink-800`                                                 |
| active   | text `brand-700`, 2px `brand-600` bottom border               |
| focus    | + `glow-brand` ring on the tab hit-area                        |
| disabled | text `ink-400`, opacity 50%, pointer events off                |

Height 44px (comfortable) / 36px (compact). Padding 0 12px. Gap between
tabs: 4px. Bottom border of the tablist: 1px `paper-200`.

**Segmented tabs** (for density-compact toolbars):

| State    | Tab                                                            |
|----------|----------------------------------------------------------------|
| default  | bg transparent, text `ink-700`                                 |
| hover    | bg `paper-100`                                                 |
| active   | bg `paper-0`, text `ink-900`, `shadow-xs`                     |
| focus    | + `glow-brand` ring                                            |
| disabled | opacity 50%                                                    |

Container: bg `paper-100`, `r-md`, 2px pad. Tab: 32px h, `body-sm`, 4px pad.

### 10.7 Breadcrumb

| State    | Item                                           |
|----------|------------------------------------------------|
| default  | text `ink-500`, `body-sm`, separator `/ ` in `ink-300` |
| hover    | text `ink-800`                                 |
| current  | text `ink-900`, weight 540, no link            |

Truncate long items with `…` at 24ch. Collapse middle items with a `…`
ellipsis button (Radix `DropdownMenu` below) when the trail exceeds 4 items.

### 10.8 Disabled states — composite surfaces

| Surface      | Disabled treatment                                                       |
|--------------|--------------------------------------------------------------------------|
| Tab          | text `ink-400`, opacity 50%, pointer-events off                          |
| Nav item     | text `ink-400`, icon `ink-400`, no hover bg, tooltip `"Coming soon"` if user hovers |
| Card (interactive) | opacity 60%, cursor `not-allowed`, hover effects disabled          |
| Any button   | see §10.1 disabled row                                                    |
| Any form input | see §10.10 Input disabled                                              |

Global principle: disabled = muted foreground at 50% alpha, frozen pointer
events, no hover/active response.

### 10.9 Toast notification

Built on `sonner`. Fixed position bottom-right (comfortable) or top-right
(dense surfaces). Width 380px. Auto-dismiss 5s (info/success), 8s (warning),
persistent (error, until dismissed). All have a close (×) icon-button.

| Variant   | Surface                           | Icon (Lucide)         | Text                                  |
|-----------|-----------------------------------|-----------------------|---------------------------------------|
| default   | bg `ink-900`, text `paper-0`     | —                     | `body-sm`                             |
| success   | bg `compliant-50`, text `compliant` | `CheckCircle`      | `body-sm` ink-900 title, ink-700 body |
| error     | bg `risk-50`, text `risk`         | `AlertCircle`         | same                                  |
| warning   | bg `mitigated-50`, text `mitigated` | `AlertTriangle`    | same                                  |
| info      | bg `evidence-50`, text `evidence` | `Info`                | same                                  |
| dismissed | (animating out)                   | —                     | slide-right + fade 200ms emphasized   |

Radius `r-lg` (12). Shadow `shadow-lg`. 1px border matching the tint's
`*-100` color (subtle, NOT the pill's no-border treatment — toasts benefit
from a slight outline to separate from dense backgrounds). Icon sits
top-left; close ×  top-right.

> Note: Toasts are the **one place** where an icon is retained for category
> at a glance — they're ephemeral and out-of-reading-flow. Pills stay
> text-only.

### 10.10 Pills — no border, no icon

See §4. Sizes:

| Size | Height | Padding X | Font                         |
|------|--------|-----------|------------------------------|
| sm   | 20     | 8         | `label` at 11px              |
| md   | 24     | 10        | `label` at 12px (default)    |
| lg   | 28     | 12        | `label` at 13px              |

**State × variant matrix** (shared by status + severity taxonomies):

| State     | Default       | Success       | Error         | Warning       | Info          | Disabled       |
|-----------|---------------|---------------|---------------|---------------|---------------|----------------|
| bg        | `draft-50`    | `compliant-50`| `risk-50`     | `mitigated-50`| `evidence-50` | `paper-100`   |
| text      | `draft`       | `compliant`   | `risk`        | `mitigated`   | `evidence`    | `ink-400`      |

GRC severity mapping (same visual treatment, different label text):
Critical → Error tint; High → Warning tint (stronger — `high-50` / `high`);
Medium → Warning muted; Low → Success; Info → Info.

### 10.11 Input

**Sizes**:

| Size | Height | Padding | Font      | Icon |
|------|--------|---------|-----------|------|
| sm   | 32 / 2.00 | 8/10    | `body-sm` | 14   |
| md   | 40 / 2.50 | 10/12   | `body`    | 16   |
| lg   | 48 / 3.00 | 12/16   | `body-lg` | 18   |

**States**:

| State      | Border        | Background    | Text         | Notes                                |
|------------|---------------|---------------|--------------|--------------------------------------|
| default    | `paper-200`   | `paper-0`     | `ink-900`    | placeholder `ink-300`                |
| hover      | `paper-300`   | `paper-0`     | `ink-900`    |                                      |
| focus      | `brand-600`   | `paper-0`     | `ink-900`    | + 3px ring `brand-600/20`            |
| filled     | `paper-200`   | `paper-0`     | `ink-900`    | same as default but with value set   |
| error      | `risk`        | `risk-50`     | `ink-900`    | + 3px ring `risk/20` on focus        |
| success    | `compliant`   | `compliant-50`| `ink-900`    | + 3px ring `compliant/20` on focus   |
| disabled   | `paper-200`   | `paper-100`   | `ink-400`    | no hover/focus response              |
| read-only  | `paper-200`   | `paper-50`    | `ink-800`    | selectable text, no caret            |

**Composition variants**:

- **with label** — `label` token (12px uppercase) above, 6px gap.
- **with helper text** — `body-sm` `ink-500` below, 4px gap.
- **with error text** — `body-sm` `risk` below, 4px gap, `AlertCircle`
  icon 14px inline left of text.
- **with icon left** — icon at 14/16/18 (by size) `ink-500`, left pad 40/44/52 instead of 10/12/16.
- **with icon right** — same geometry, right-aligned, common for search clear (×), password toggle, date picker trigger.
- **with placeholder** — `ink-300`, same font as value; disappears on input.

### 10.12 Modal / Dialog

Built on Radix `Dialog`. Overlay: `ink-900/40` + 4px backdrop-blur.

**Sizes**:

| Size       | Max width | Min height | Padding      | Use                             |
|------------|-----------|------------|--------------|---------------------------------|
| sm         | 400 / 25.0 | 160        | 24/20/16     | Confirmations, quick forms      |
| md         | 560 / 35.0 | 240        | 32/24/24     | Default — edit forms            |
| lg         | 720 / 45.0 | 320        | 40/32/32     | Detail views, record editors    |
| xl         | 960 / 60.0 | 480        | 48/40/40     | Complex workflows, multi-step   |
| fullscreen | 100vw     | 100vh      | 48/64/48     | Immersive editing, reports      |
| auto       | max-content, up to 90vw | auto | inherits   | Content-fit (e.g., image lightbox) |

Structure:

- **Header**: title (`display-sm` for narrative / `heading-md` for task) +
  optional subtitle in `ink-500`; close × top-right as icon-only ghost.
- **Body**: padding per size; body font; 16px gap between fields.
- **Footer**: right-aligned action row, primary CTA rightmost, secondary
  left of it. Destructive actions use `destructive` variant.

Radius `r-xl` (16). Shadow `shadow-xl`. Animation: fade 200ms + scale
0.96 → 1 standard ease, reverse on close.

### 10.13 Icon library

Source: **Lucide** (`lucide-react`). Tree-shakable. Stroke-based (pairs
well with the editorial/serif atmosphere — no filled glyphs).

**Recommended GRC icon set** (keep to this short catalog unless a new
surface truly needs more):

| Category          | Icons                                                                   |
|-------------------|-------------------------------------------------------------------------|
| Risk & severity   | `Shield`, `ShieldAlert`, `ShieldCheck`, `AlertCircle`, `AlertTriangle`, `AlertOctagon` |
| Compliance        | `CheckCircle2`, `XCircle`, `MinusCircle`, `Clock`, `CalendarCheck`      |
| Audit & evidence  | `ClipboardCheck`, `ClipboardList`, `FileText`, `FileCheck`, `Paperclip`, `Link2` |
| Data & reporting  | `BarChart3`, `LineChart`, `PieChart`, `TrendingUp`, `TrendingDown`, `Download`, `Upload`, `Filter`, `Search` |
| Navigation & UI   | `ChevronDown`, `ChevronRight`, `ChevronLeft`, `ChevronUp`, `MoreHorizontal`, `MoreVertical`, `X`, `Menu`, `Settings2` |
| Action            | `Plus`, `Minus`, `Edit3`, `Trash2`, `Copy`, `Send`, `Share2`, `RefreshCw` |
| AI                | `Sparkles`, `Wand2`, `Bot`, `Zap`, `MessageSquare`, `Brain`            |
| People & access   | `User`, `Users`, `UserCheck`, `UserX`, `Lock`, `Unlock`, `Key`         |
| Time & workflow   | `History`, `CalendarDays`, `ArrowRight`, `ArrowLeft`, `CornerDownRight`|
| Sources           | `BookOpen`, `Database`, `Cloud`, `GitBranch`, `Layers`                 |

Sizes: use §3.4 icon-size tokens. All icons inherit `currentColor`. Never
set `fill=` on a Lucide SVG.

### 10.14 Skeleton

Loading placeholder. Not a decorative element — it's an accessibility
primitive. Must match the height and approximate width of what it stands
in for, so page layout doesn't jump when real content arrives.

**Sizes** (match the content they replace):

| Use                                    | Dimensions                               | Radius  |
|----------------------------------------|------------------------------------------|---------|
| Text line (`body`)                      | h-4 (16px), width varies 40–100%          | `r-sm` (6) |
| Text line (`body-sm`)                   | h-3.5 (14px), width varies                | `r-sm`  |
| Heading (`heading-md`)                  | h-5 (20px), width 40–70%                  | `r-sm`  |
| Display (`display-sm`)                  | h-8 (32px), width 40–60%                  | `r-sm`  |
| Avatar (32)                             | 32×32                                     | `r-full` |
| Avatar (40)                             | 40×40                                     | `r-full` |
| Pill                                    | h-6 (24px), width 64px                    | `r-full` |
| Input                                   | h-10 (40px), full-width                   | `r-md` (8) |
| KPI tile block                          | 240×140                                   | `r-lg` (12) |
| Card block                              | matches the card it replaces              | `r-lg`  |
| Chart area                              | matches the chart viewport                | `r-lg`  |
| Table row (comfortable)                 | h-11 (44px), per-column widths            | `r-sm`  |
| Table row (compact)                     | h-8 (32px)                                | `r-sm`  |

**Appearance**:

- Base: `paper-100` (light) / `ink-700` (dark).
- Shimmer: linear-gradient from base through `paper-0/60` (light) /
  `ink-600` (dark) back to base, 1.6s standard ease, infinite
  translate-x from −100% to 100%. Disabled under
  `prefers-reduced-motion`.

**Composition recipes**:

- **Card skeleton**: header line (h-5, 60%) + 2 body lines (h-4, 100%
  and 80%) + 1 sub-metric line (h-3.5, 40%). Gap 12.
- **Row skeleton**: one cell per column; `flex-1` or explicit widths
  matching the real column.
- **Chart skeleton**: axis lines (§2 alpha-10) + a muted `paper-100`
  silhouette following the expected shape.
- **Chat message skeleton**: `AIResponse`-shell with gradient border +
  3 body-lg text lines (100% / 80% / 60%).

**Accessibility**:

- Wrap the skeleton region in `<div role="status">` with a
  visually-hidden `<span className="sr-only">Loading …</span>`
  describing what's coming ("Loading risks", "Loading Q1 dashboard").
- Skeleton elements themselves carry `aria-hidden="true"`.
- When the real content arrives, remove the skeleton **and** update
  the status message to "Loaded" or move focus to the new heading if
  appropriate.

---

## 11. Cross-cutting patterns

These patterns live above every page and apply system-wide. When building
any new page, assume these are present — don't reinvent them.

### 11.1 Command palette (⌘K)

The **only** global search surface. Invoked by `⌘K` / `Ctrl+K` or via the
sidebar "Search" top-action. One input, three result kinds, zero modes.

```
width: 640px (md), 720px (lg viewport)
radius: r-xl (16)
surface: paper-0 (light) / ink-800 (dark)
shadow: shadow-xl + 1px brand-100 top-border hairline (signals this is
        the global action surface, not a generic popover)
overlay: ink-900 / 0.40 + 4px backdrop-blur
padding: 0 (input touches edges); sections get 8px vertical pad
max-height: 70vh (scrolls)
```

**Anatomy** (top → bottom):

1. **Input row** — 56px tall, no border, `Search` icon 20px `ink-500` on
   the left, 16px gap, `body-lg` `ink-900` typed text, placeholder
   "Search risks, controls, reports… or ask IRA anything."
   Escape clears; Enter routes.
2. **Result sections**, stacked with a 1px `paper-200` divider between.
   Each section starts with a `label`-token section header in `ink-500`
   at 8px top-pad.
   - **Pages** — static routes. Icon-left from §10.13; label `body`;
     secondary route text `body-sm` `ink-500` right-aligned.
   - **Entities** — risks, controls, engagements, reports, sessions,
     workflows, evidence. Same row pattern plus a severity pill on the
     right for risks/findings; an entity-type tag for everything else.
     ID in `code-sm` JetBrains, dim `ink-500`, left of title.
   - **Ask IRA** — always the last section. Single row: `Sparkles` icon,
     "Ask IRA: <query>" in `body-lg`, `brand-700`, right-pointing
     chevron. Hitting Enter while this row is highlighted routes to
     `/chat` with the query pre-filled.
3. **Footer** — 36px tall, `paper-50` bg, `body-sm` `ink-500`. Shortcut
   hints: `↵ to open`, `⌘↵ to open in new tab`, `esc to close`.

**Behavior**:

- Debounce 120ms. Zero query = recent searches (last 8) + pinned
  entities. Token-aware fuzzy match.
- Max 8 results per section; "Show all n" row at bottom of a section
  routes to the entity's list page with the query pre-applied.
- Natural-language queries (length >20 chars, ending in "?", or
  containing verbs like "show / find / summarize") auto-promote the
  "Ask IRA" row above "Entities."
- Keyboard only: arrow keys move selection, Enter opens, `⌘↵` opens in
  new tab, `⌘shift+K` scopes to Admin for superuser.
- Never closes on click-outside during an in-flight request (prevents
  accidental dismiss mid-stream).

**Rules**:

- **Never** add a second "search" input anywhere else. Page-level filters
  (§11.4) are not global search.
- **Never** show a loading spinner inside the palette — it implies
  remote latency. Inline a 2px `brand-600` top-edge bar that drifts
  right at 1.4s cycle during async work.

### 11.2 Workspace selector (multi-org)

Sits at the top of the sidebar as the first surface below the logo. Treats
multi-tenant switching as a quiet, infrequent action — not a splashy CTA.

```
container: 220×48, radius r-md (8), bg sidebar-surface, border none
padding: 0 12px, gap 8
content: 28×28 avatar (workspace mark, brand-900 bg + paper-0 monogram)
         + stacked label (workspace name 13/600 sidebar-accent,
         role 11/500 sidebar-text-dim)
         + ChevronsUpDown 14px sidebar-text-muted, right-aligned
```

On open, a popover (w-320, `paper-0` bg, `r-lg`, `shadow-md`) lists all
workspaces grouped by organization. Each row: 40px h, workspace avatar,
name `body`, role `body-sm` `ink-500` right-aligned, current one carries
a `CheckCircle2` icon in `brand-600`.

**Rules**:

- Switching a workspace is a hard route change — never optimistically
  swap data in-place. Show a 300ms `RouteTransition` overlay.
- Show a warning toast if the user is leaving unsaved form edits on the
  current workspace.
- Admin-only workspaces (e.g., tenant diagnostics) sit in a separate
  bottom group with a `ShieldAlert` glyph in `mitigated`.

### 11.3 Share dialog + permission model

Any entity — risk, control, engagement, session, dashboard, report,
workflow — is shareable via a shared `ShareDialog` (`md` modal, §10.12).

**Body** structure:

1. **Recipient input** — multi-token input; suggestions dropdown shows
   users/teams with avatar + role. Typing an email invites an external
   auditor (generates a time-boxed read-only link).
2. **Permission** — segmented tabs (§10.6 segmented): `View` · `Comment`
   · `Edit`. External invitees are locked to `View` unless admin.
3. **Expiry** — Select (§10.4) with presets `7 days`, `30 days`,
   `90 days`, `Never`. External default: 30 days.
4. **Message** (optional) — Textarea, 3 rows, 240-char max.
5. **Link row** — read-only `Input` with the share URL + `Copy` icon-button
   on the right. Copies to clipboard + toast "Link copied."
6. **Existing access** — list of current recipients with role pill and
   kebab (revoke / change permission).

**Footer**: `Cancel` (ghost) + `Send` (primary). Send triggers email
notification with a 128×72 preview image.

**Rules**:

- External auditors see a **read-only shell** — sidebar collapses to
  only the shared item's page, command palette is scoped to that item,
  no cross-entity navigation. Use the `SharedView.tsx`-style chrome:
  persistent `ReadOnlyBanner` at the top (`evidence-50` bg, `evidence`
  text, `Info` icon, no dismiss).
- Share on a **chat session** follows fork-on-interact: recipient views
  read-only; clicking `Continue` forks via `POST /sessions/{id}/fork`
  into their own workspace.
- Revoking access takes effect immediately; show a subtle "Access
  revoked" toast to the former recipient if they're live.

### 11.4 Filter bar (registries, tables, lists)

Every list/table page follows the **same filter contract**. Memorize once,
use everywhere — inconsistency here reads as product chaos.

**Horizontal layout** (left → right):

```
[ Search input (debounced 250ms) ]
[ Status chips — tabs, multi-select ]
[ Date range picker ]
[ Owner select ]
[ Severity / Priority select (where applicable) ]
[ Advanced filters button (opens slide-over) ]
--- spacer ---
[ View mode toggle ] [ Density toggle ] [ Column settings ]
```

- **Container**: `paper-0` bg, `1px paper-200` bottom border, 56px h,
  sticky top of the table viewport.
- **Search input**: `sm` size, `Search` icon left, placeholder matches
  the entity ("Search risks…", "Search controls…").
- **Status chips**: rendered as **segmented tabs** (§10.6) for 3–5
  options; rendered as **multi-select pills** for >5 options (pills
  follow §10.10 — no border, no icon; selected pill adds a 2px
  `brand-600/20` outer ring as the selection tell).
- **Advanced filters**: opens a right-aligned slide-over (420px) with all
  filterable dimensions grouped. Footer has `Reset` (ghost) + `Apply`
  (primary). A blue `evidence` dot on the button indicates active
  advanced filters.
- **Persistence**: filter state persists **per session** (URL query-string
  is canonical). Navigating away and back restores it. Explicit `Reset all`
  clears.

**Empty-state hint row** when filters return zero: a single `body-sm`
`ink-500` row — "No results match these filters. [Clear all]" — with
the clear action as an inline `link` variant button.

### 11.5 Notifications

Two parallel channels, never mixed:

1. **Toasts** (§10.9) — ephemeral system events: save/update/delete,
   workflow completion, share received live, network error. Never used
   for durable information.

2. **Notification inbox** — lives as a right-edge slide-over (420px)
   summoned from the sidebar `Bell` icon-button (top-row, near Search).
   Unread count renders as a `sidebar-accent` badge with `brand-600`
   text. Inbox content:

   - **Tabs** (§10.6 underline): `All` · `Assigned to me` · `Mentions` ·
     `Shared`.
   - **Row**: 72px tall, avatar + title (`body` weight 540) + meta
     (`body-sm` `ink-500`) + time-ago right-aligned. Unread rows carry
     a 2px `brand-600` left border; read rows have none.
   - **Bulk action bar** appears on scroll when any rows are selected
     via checkbox: `Mark read` · `Archive` · `Mute sender`.

3. **Email** — mirror of the inbox, configurable per-category in
   `/admin/settings`. Never used for non-user events (cron heartbeats,
   health).

**Rules**:

- **Never** stack more than one toast at a time in the visible region —
  newer toasts supersede older (sonner default). Error toasts are the
  exception: they persist until dismissed and can stack up to 3.
- **Never** use a toast for anything that will be needed more than once;
  if a user might want to read it again, route it through the inbox.

### 11.6 Comment threads

Every entity surface can receive comments via a shared `CommentsThread`
component. The thread lives in a right-hand drawer or an embedded panel.

**Composer**:

- Textarea (`md`), rich-text minimal: **bold**, _italic_, code, link,
  `@mention` (opens typeahead dropdown with user suggestions), `#`
  entity-link (opens palette-style picker).
- Right-aligned `Send` primary button; left-aligned `Resolve thread`
  ghost action when a thread is active.

**Comment row**:

```
layout: avatar (32) + content column + actions (visible on hover)
padding: 12px 16px
hover: paper-50 bg
author: body weight 540 ink-900
time: body-sm ink-500, tabular-nums
body: body ink-800, 16px gap above
reactions: inline flat pill row — "👍 3  ✅ 1" uses Lucide glyphs
           (ThumbsUp, CheckCircle2) as 14px `icon-sm` with tabular count
```

A **Resolved** thread dims to 60% opacity and gains a tiny `CheckCircle2`
`compliant` left-edge marker. The **Reopen** action is in the kebab.

**Rules**:

- **Never** render comments inline with primary data (e.g., inside a
  risk row). Always in a drawer or side-panel so the data reads cleanly.
- **Never** use avatar circles for the **AI** commenter — IRA's remarks
  appear as an indented `AIResponse` block (§4), never as a chat-style
  bubble. Author shows "IRA" in `brand-700` weight 600.

### 11.7 Audit trail drawer

Every detail page has an **Audit trail** tab or drawer. The trail is a
vertical timeline of CRUD actions, each as a compact row:

```
timestamp (tabular-nums, ink-500) · user avatar + name ·
action verb (created | updated | deleted | approved | rejected |
            assigned | shared | forked | exported | executed)
field diff (when `updated`): two-column before/after in code font,
            paper-50 bg, 1px paper-200 border, r-sm
```

- **Sticky filter row** at top: by actor, by action type, by date range.
- **Export** (`Download` icon) → `audit-trail-<entityId>-<date>.csv`.
- **Never** truncate diffs — an auditor needs the full value. Long
  strings wrap with a 2-line clamp and a `Show full` inline link-button.

### 11.8 Role-based UI (RBAC)

The platform serves seven personas (see §14) with distinct capability
sets. UI elements that the current user lacks permission for follow the
**hide-or-disable** rule:

| Condition                                         | Treatment                                                                 |
|---------------------------------------------------|---------------------------------------------------------------------------|
| Feature is invisible to this role                 | Hide entirely — no greyed-out affordances                                 |
| Feature visible but action is blocked             | Disabled state (§10.8) with tooltip: "Your role (<Role>) can't do this."  |
| Feature visible, action needs elevated permission | Enabled, but first click opens a small explainer popover with a request-access link |
| Read-only share recipient                         | Entire page enters `ReadOnlyBanner` mode (see §11.3)                      |

**Never** silently no-op a click on a disabled element. Always show a
tooltip or a popover explaining why.

---

## 12. AI surfaces — the IRA pattern

The platform's signature surface is its AI copilot (IRA — Intelligent
Risk Auditor). The AI interaction pattern is load-bearing for the entire
product, so it gets its own section.

### 12.1 Three-panel chat layout

`/chat` is **not** a single-column chat. It's a three-panel workspace:

```
┌────────────────┬────────────────────────────┬──────────────────┐
│  History       │       Conversation         │    Artifacts      │
│  (280px)       │       (flexible)           │   (420–520px)    │
│                │                            │                   │
│  [+ New Chat]  │  ┌──────────────────────┐  │  [Plan]          │
│                │  │  Messages thread     │  │  [Code]          │
│  Pinned  (3)   │  │                      │  │  [Sources]       │
│  ├ Q3 SOX…    │  │  User: ...           │  │  [Result]        │
│  └ Vendor…    │  │  IRA:  ...           │  │                   │
│                │  │  ...                 │  │  ────────────    │
│  Today         │  │                      │  │                   │
│  ├ Invoice…   │  │                      │  │  Artifact view    │
│  └ Controls…  │  └──────────────────────┘  │  (table / code /  │
│                │  ┌──────────────────────┐  │   chart / prose)  │
│  Yesterday     │  │  Input bar           │  │                   │
│  ├ ...        │  │  [📎] [Send ⌘↵]     │  │                   │
│                │  └──────────────────────┘  │  [Add to dash]    │
│  Earlier       │                            │  [Add to report]  │
└────────────────┴────────────────────────────┴──────────────────┘
```

**Rules**:

- History panel **does not replace** the app sidebar — it sits **inside**
  the chat page, to the right of the sidebar. The sidebar remains the
  app shell everywhere. History panel width: 280px; collapses to 48px
  icon-rail on `<xl`; hides on `<lg` (opened via a sheet from a
  `PanelLeft` icon-button in the conversation header).
- Conversation column is **never a chat bubble stream**. User messages
  get a single `ink-500` "You" label above body text — `body-lg`, no
  bubble. IRA messages follow §4 `AIResponse`.
- Artifact panel is collapsible (right edge grip). Default state: open
  when any message in the thread has an artifact; closed otherwise.

### 12.2 Artifact panel

Tabs (§10.6 underline) pin to the top of the right panel. Order is
fixed — it's the order of the pipeline:

| Tab       | Content                                                                                        |
|-----------|------------------------------------------------------------------------------------------------|
| `Plan`    | IRA's step-by-step analysis plan. Ordered list, each step is a card (§4 muted variant) with a status icon (`Circle` pending, `Loader2` running, `CheckCircle2` done, `AlertCircle` failed). |
| `Code`    | The generated SQL / Python. Code block with `shiki` syntax highlighting, `JetBrains Mono`, 13px. Header bar: language pill, copy button, "Re-run" ghost button. |
| `Sources` | Uploaded files + data source rows. Each row: file icon, name, size, row-count, status pill. Clicking expands to reveal schema (column name + inferred type in a 2-col grid). |
| `Result`  | The final answer: table, chart, metric, or prose narrative. Full-width, `paper-0` card. Table uses §4 DataGrid rules; charts use palette §2.   |

**Action row** at the bottom of the panel (sticky, `paper-0` bg, 1px
`paper-200` top border):

- `Add to dashboard` — opens a dashboard picker (§13.3) and drops the
  artifact as a widget.
- `Add to report` — opens a report picker, inserts as a section.
- `Save as workflow` — opens a naming modal, creates a workflow
  template from the generated code.
- `Download` — CSV (data) or PNG (chart) or PDF (prose).
- `Share` — opens §11.3 `ShareDialog`.

**Rules**:

- **Never** display the code tab empty with a "No code generated yet"
  placeholder — collapse it. Only show tabs that have content.
- **Never** auto-switch tabs mid-stream. The user picks where to look.
- **Never** re-run code without an explicit confirmation — analytics can
  be expensive.

### 12.3 Clarification chips (inline, not modals)

When IRA's input is ambiguous, it **does not open a modal**. Instead, the
assistant message renders an inline clarification block:

```
┌────────────────────────────────────────────────────────┐
│  I see two ways to interpret this — which one?         │
│                                                        │
│  ┌──────────────────┐  ┌──────────────────────────┐   │
│  │ Q1 2026 only     │  │ All time                 │   │
│  └──────────────────┘  └──────────────────────────┘   │
│  ┌──────────────────────────────────────────────┐     │
│  │ Just high-severity findings                  │     │
│  └──────────────────────────────────────────────┘     │
│                                                        │
│  … or type a reply in your own words.                 │
└────────────────────────────────────────────────────────┘
```

- **Chips** are `secondary` variant buttons at `sm` size, `r-full`
  radius, 1px `paper-200` border, `body-sm`. Hover: `brand-50` bg,
  `brand-700` text. Click auto-sends the chip's text as the next user
  message.
- **Block container**: 1px `paper-200` border (no fill), 16px pad,
  `r-lg`. Nested in the `AIResponse`.
- **Copy** is conversational and declarative. Never "Please choose one
  of the following options:". Prefer "I see two ways to interpret this
  — which one?"

### 12.4 Assumptions panel (editable AI inputs)

When a query auto-promotes to analysis without explicit clarification,
IRA surfaces the assumptions it made **in a collapsible panel above
the artifact tabs**:

```
┌──────────────────────────────────────────────────┐
│  Assumptions IRA made             [Edit ▾]       │
├──────────────────────────────────────────────────┤
│  • Time range: Q1 2026 (Jan 1 – Mar 31)         │
│  • Severity: High + Critical only               │
│  • Scope: All 14 business units                 │
└──────────────────────────────────────────────────┘
```

- Surface: `brand-50` bg, 1px `brand-200` border, `r-md`, 16px pad.
- Each assumption is a row: bullet + short label in `body-sm` `ink-800`.
- `Edit` opens an inline form (`sm` inputs, 12px gap) with an
  `Apply & re-run` primary button at the bottom.
- Collapsed state: single-line summary "3 assumptions applied" with a
  `ChevronDown`.

### 12.5 Progressive loader (multi-step AI)

While analysis runs, the conversation column shows a **single animated
row** directly below the user's message — not a blob of spinners:

```
●○○  Understanding query…
●●○  Planning analysis…
●●●  Writing code…
     Executing…
     Summarizing…
```

- Active step: `body` `ink-900` weight 540, 3 filled dots in `brand-600`.
- Completed steps: strikethrough in `ink-500`, with a `CheckCircle2`
  `compliant` 14px glyph replacing the dots.
- Pending steps: `body` `ink-400`, three `ink-300` dots.
- Stagger pulse: 400ms between dots, standard ease.
- When all steps complete, the row collapses into a single `body-sm`
  `ink-500` "Answered in 3.1s · 2 steps · 847 rows" meta line — which
  becomes the header of the final `AIResponse`.

**Rules**:

- **Never** show a generic "Thinking…" spinner. Every step must be
  named.
- **Never** hide the loader while the model is streaming partial output.
  The caret (§4 `AIResponse`) and the loader co-exist: loader shows the
  pipeline stage; caret shows the live token stream inside `Result`.

### 12.6 Workflow builder canvas (chat + preview)

A secondary mode of the chat page, routed via `/chat?mode=workflow`.
Same three-panel layout, but the right panel is **not** tabs — it's a
live preview of the workflow being described.

```
History │ Conversation │ Canvas (preview of workflow steps)
```

- **Canvas** renders each step as a `Card` (§4 outlined) with step
  number, title, short description, and a data-binding pill (source →
  ref). Steps are connected with a 2px `paper-300` connector line;
  hover on a step highlights its upstream/downstream connectors in
  `brand-400`.
- **Canvas is read-only**. The user's only way to edit is by typing a
  natural-language instruction ("Swap step 3's filter to exclude
  intercompany entries"). IRA updates the canvas in place.
- **Finalize** button sits sticky at the bottom of the canvas: opens
  a save-workflow modal (name, category, visibility).

### 12.7 Quick actions on empty chat

Before the user types, the conversation column shows a **single** hero
block — not a grid of promotional cards:

```
Serif display-lg: "What would you like to know?"
body-lg ink-500 (one line): "Upload data, pick a source, or ask IRA
                             anything about your audit."
60px gap
Row of 4 "quick actions" — secondary buttons with a left icon:
  • "Analyze a file" (Upload)
  • "Build a workflow" (GitBranch)
  • "Summarize last audit" (History)
  • "Find open risks" (Search)
32px gap
"Recent sessions" — horizontal scroll row of 4 Card (muted variant)
                    showing title, last-used time, preview.
```

**Rules**:

- **Never** generate AI-promotional copy ("I'm your AI copilot, ready to
  help!"). The tone is editorial — the user is the subject of the sentence.
- **Never** render empty quick-actions as a 2×2 grid of glowing gradient
  tiles. Flat, secondary-variant, one row.

---

## 13. Domain surfaces

These are the GRC surfaces the platform ships. Each gets a concrete
pattern so a new contributor can stand up a new surface without guessing.
The full IA lives in §13.0.

### 13.0 Information architecture

The sidebar groups surfaces into four bands. This order is canonical —
never re-shuffle without product-council approval.

```
IRAME.AI
[Workspace selector]              ← §11.2

⌘K  Ask IRA / Search              ← §11.1
Bell  Notifications               ← §11.5

HOME                              → /home                   §13.1
IRA AI                            → /chat                   §12

─── AUDIT LIFECYCLE ───

GOVERNANCE
  Business Processes              → /governance/processes   §13.2.1
  RACM                            → /governance/racm        §13.2.2
  Control Library                 → /governance/controls    §13.2.3
  Risk Register                   → /governance/risks       §13.2.4
  Audit Planning                  → /governance/planning    §13.2.5

EXECUTION
  Engagements                     → /execution/engagements  §13.3.1
  Control Testing                 → /execution/testing      §13.3.2
  Evidence & Workpapers           → /execution/evidence     §13.3.3
  Findings                        → /execution/findings     §13.3.4

WORKFLOWS                         → /workflows              §13.4

─── INTELLIGENCE ───

DASHBOARDS                        → /dashboards             §13.5.1
REPORTS                           → /reports                §13.5.2
AI CONCIERGE
  Document Forensics              → /ai-concierge/docs      §13.5.3
  Table Extractor                 → /ai-concierge/tables    §13.5.4

─── SYSTEM ───

CONFIGURATION                     → /configuration          §13.6.1
ADMIN
  Users & Teams                   → /admin/users            §13.6.2
  Roles & Permissions             → /admin/roles            §13.6.3
  System Settings                 → /admin/settings         §13.6.4
  Integrations                    → /admin/integrations     §13.6.5
  Audit Logs                      → /admin/logs             §13.6.6

─── RECENT SESSIONS ───  (scrollable, collapsible)

[User profile card]               ← §5 sidebar user card
```

### 13.1 Home

The home dashboard is **action-oriented**, not decorative. Lead Auditor,
Staff Auditor, Audit Manager, and CAE each see the same layout but with
role-weighted content.

**Layout** (single column, stacked):

1. **Page header** (§5) — `display-xl` serif: "Good morning, Priya."
   Subtitle `body-lg ink-600`: "You have **3 items** waiting on you and
   **2 engagements** on track this week." Numbers bold in `ink-900`.
2. **Action queue** — horizontal scroll row of `Card` (elevated
   variant), each 320×180, each representing a pending action:
   "Review Q1 SOX findings", "Approve vendor scope change", etc.
   Each card has a severity pill + CTA button. This is the single most
   important surface on the page.
3. **KPI band** — four `Card` (outlined), each 240×140:
   - `Open risks` with delta arrow + `evidence` pill trend.
   - `Control coverage` as % with a tiny 40px sparkline.
   - `Findings this quarter` with severity breakdown.
   - `Last audit` with relative time ("12 days ago") + link.
4. **Engagement timeline** — Gantt chart (§13.2.5), compact height,
   "This quarter" default range.
5. **Risk exposure heatmap** — 5×5 grid, see §13.2.4 risk heatmap.
   Read-only here; clicking a cell deep-links to the filtered Risk
   Register.

**Rules**:

- **Never** mock KPIs. If data is missing, show a 2-line empty state
  inline in the card: "No data yet. [Connect a source]" in `ink-500`.
- **Never** use gradient card backgrounds. KPI differentiation is via
  typography (number size) and severity pills, not color fills.
- **Never** put promotional content ("Try our new workflow!") on Home.
  Home is operational.

### 13.2 Governance

The governance cluster is where policy-of-record lives. All surfaces
here are **registries** — list + detail, with CRUD and versioning.

#### 13.2.1 Business Processes

The container for everything else. Each process owns an SOP, a RACM,
workflows, and risks.

**List page**: data table (§4), columns:
`Code` (mono, 13px) · `Name` (body) · `Owner` (avatar + name) ·
`Risks` (count pill) · `Controls` (count pill) · `Last reviewed`
(date). Row action: open detail.

**Detail page** opens at `/governance/processes/:id`:

- **Page header** with breadcrumb `Governance › Business Processes › <name>`.
- **Tab bar** (§10.6 underline) — `SOP` · `RACM` · `Workflows` · `Risks`.
  Exactly four tabs — no more.
- **SOP tab**: long-form editor. Uses the `Report reader` layout (§5)
  with editable sections. `@mentions` for controls and risks resolve to
  mini-tiles.
- **RACM tab**: embedded RACM grid (§13.2.2) scoped to this process.
- **Workflows tab**: list of workflows linked to this process + a
  `Run One-Click Audit` primary button (see §13.4.2).
- **Risks tab**: filtered Risk Register (§13.2.4) for this process.

#### 13.2.2 RACM (Risk-Control Matrix)

A specialized data grid, not a generic table. Rows = risks; columns =
controls; cells = mapping strength.

**Cell content**:
- Empty: hollow circle `ink-300`.
- Weak mapping: quarter-filled circle `mitigated`.
- Strong mapping: filled circle `compliant`.
- Under review: `AlertCircle` glyph, `high`.

**Hover** on a cell expands a popover (§10.3) with the mapping's
evidence count, last test date, and a link to open control-testing
scoped to this risk/control pair.

**Generator** lives at `/governance/racm/generate` as a full-page
wizard (4 steps: Upload SOP → Extract → Review → Commit). Step 4 is a
read-only preview that renders the extracted RACM before writing.

**Rules**:

- **Never** color a RACM cell with red/green alone — always carry the
  glyph (redundant encoding).
- **Never** allow editing in the matrix cell itself. Click to open a
  side drawer with the full mapping form.

#### 13.2.3 Control Library

Data table (§4). Columns:
`ID` (mono `CTL-0142`) · `Name` · `Framework` (pill — SOX, ISO, NIST,
custom) · `Type` (pill — Preventive, Detective, Corrective) ·
`Frequency` · `Owner` · `Status` (severity pill — Active, Draft,
Retired, Under review).

**Detail drawer** (`lg` modal) — tabs `Overview` · `Tests` · `Evidence`
· `RACM usage` · `Audit trail`.

**Bulk actions** when rows are selected: `Assign owner`, `Change
framework`, `Retire`, `Export`. Bar slides up from the bottom of the
viewport.

#### 13.2.4 Risk Register

Data table + a persistent `Risk heatmap` button in the filter bar that
opens a side-panel visualization.

**Columns**: `ID` (mono `R-0087`) · `Title` · `Process` · `Severity`
(pill — Critical / High / Medium / Low, spelled out) · `Likelihood` ·
`Impact` · `Score` (numeric, tabular) · `Owner` · `Status`.

**Risk heatmap** (5×5):
- X = Likelihood (1–5); Y = Impact (1–5).
- Cell color from diverging scale (§2): low-left → high-right.
- Cell content: count of risks, `numeric` 20px, centered.
- Click a cell filters the table to that bucket.
- **Always** label the cell with count text — never color-only.

**AI banner** (the only AI surface on governance pages) sits above the
filter bar: `brand-50` bg, 1px `brand-200` border, `Sparkles` icon,
body "IRA found 4 new risks since your last review." + `View`
secondary button. Dismisses per session; re-appears when data changes.

#### 13.2.5 Audit Planning

v1: **Timeline (Gantt) only.** Resources, risk matrix, and budget
views are v2.

**Gantt**:
- Rows = engagements; columns = weeks (default) / months (toggle).
- Bar: 24px tall, `r-sm`, fills from start → end date. Color by
  engagement status (`draft`, `evidence` active, `mitigated` at risk,
  `compliant` complete).
- Label on the bar: engagement name in `paper-0` (on dark bar) or
  `ink-900` (on light bar — auto-contrast), truncated with ellipsis.
- Dependency arrows between bars: 1.5px `ink-400` curved line with a
  small chevron head.
- Today marker: vertical 1px `brand-600` dashed line with "Today" label
  at the top.

**Rules**:

- **Never** use more than 5 color categories on the Gantt — use pill
  badges inside the bar for sub-classification.
- **Never** overlap bars without a visible offset — stack them on
  separate rows to keep legibility.

### 13.3 Execution

#### 13.3.1 Engagements

The unit of fieldwork. Data table with a `lifecycle` status chip:
`Planned` · `In fieldwork` · `In review` · `Reporting` · `Closed`.

**Detail page** layout:
- **Page header** with engagement code, name, status, `Export audit
  pack` primary action.
- **Phase tracker** — a horizontal stepper (§10.6 segmented look, but
  wider) showing the five phases with check/current/pending states.
- **Tabs**: `Overview` · `Controls` · `Evidence` · `Findings` ·
  `Team` · `Timeline` · `Audit trail`.
- **Overview** card bands show scope, RACM version used, lead auditor,
  budget vs actual, deadline.

#### 13.3.2 Control Testing

Matrix view: controls × test instances. Each cell shows test status
(Not started, In progress, Passed, Failed, Needs review).

**Inline test drawer** (right side) when a cell is clicked:
- Test objective (read-only).
- Evidence slot — drag-drop zone + list of linked evidence.
- Test procedure (rich-text).
- Conclusion (segmented: Pass / Fail / N/A).
- Notes.
- `Save draft` + `Submit for review` actions.

**AI assist** (opt-in): a `Draft test steps` ghost button inside the
drawer opens a small IRA panel that proposes procedure text. Accepts
on click; user edits freely.

#### 13.3.3 Evidence & Workpapers

A file explorer + a structured evidence ledger. Two views:

1. **Grid view**: 4-column grid of file cards — thumbnail (if image /
   PDF first page), filename, size, type pill, upload-time.
2. **Table view**: same data, as §4 DataGrid. Columns include `Linked
   controls` and `Linked tests` (both as clickable chips).

**Upload zone**: full-width drop target at the top of the page —
2px dashed `paper-300` border when idle, `brand-600` + `brand-50` tint
when hovering a drag. Accepts PDF, XLSX, CSV, DOCX, images.

**Chain of custody**: each evidence row has an expandable **trail**
strip showing `uploaded by → linked to test → approved by → exported`
as a mini timeline (same vocabulary as §11.7 audit trail).

#### 13.3.4 Findings

The findings tracker is **centralized across sources** (control tests,
AI runs, external audits). Data table with columns:
`ID` · `Title` · `Severity` (pill) · `Source` (pill — Test, AI,
Manual) · `Status` (Open, Remediation, Closed, Accepted risk) ·
`Owner` · `Due` · `Days open` (tabular).

**Detail drawer** includes:
- Narrative body (`AIResponse`-style if AI-authored).
- Evidence links.
- Remediation plan — an editable mini-kanban (Open → In progress →
  Verified → Closed) with due dates and assignees.
- Linked findings (duplicates, related) as pills.
- Cross-reference to engagement / control / risk / RACM row.

**Manual finding modal** (§10.12 `md`) has the composer form with
severity, title, narrative, evidence picker, linked entities.

### 13.4 Workflows

#### 13.4.1 Workflow library

A card grid of workflow templates (16 seed + user-created). Each card:

```
Card (outlined), 280×200, r-lg, no shadow default.
Icon (40px, r-md brand-50 tile, brand-600 stroke).
Title (heading-sm, 2-line clamp).
Description (body-sm, ink-600, 3-line clamp).
Meta row: category pill + "Used 143 times" in ink-500.
Hover: shadow-sm, border paper-300.
```

**Filter bar** (§11.4): search + category chips (`Financial`,
`Operational`, `IT`, `Compliance`, `Custom`) + advanced filters.

**Clicking a card** opens the workflow at `/workflows/:id` — detail
page with step visualization + `Run` primary button.

#### 13.4.2 One-Click Audit (OCA)

A specialized workflow that executes all workflows for a business
process in sequence. Routed from the process detail page.

**Wizard** (4 phases, each a full-screen step):

1. **Scope** — choose business process + which workflows to include
   (checkbox list).
2. **Data sources** — select files/data sources per workflow. AI
   auto-maps columns; manual tag where auto fails.
3. **Review** — summary of what will run, estimated duration.
4. **Execute** — progress view (see §13.4.3 Executor) with live
   findings feed.

**Output** is a consolidated cross-reference report. Find it at
`/reports/<oca-run-id>`.

#### 13.4.3 Workflow executor

Dedicated page `/workflows/:id/run`. Three-panel:

```
Input form   │   Progressive execution panel   │   Live findings feed
(left 320px) │   (center, flex)                │   (right 360px)
```

- **Input form**: required inputs, file uploads, optional params.
  `Run` primary button at bottom.
- **Progressive execution**: step-by-step list (§12.5 progressive
  loader). Each step expandable to show inputs/outputs.
- **Live findings feed**: findings appear as rows in real-time,
  newest on top, with a 200ms slide-in fade. Each row: severity pill +
  title + source. Click to open finding detail drawer (§13.3.4).

### 13.5 Intelligence

#### 13.5.1 Dashboards

Two variants, both first-class:

1. **Process dashboards** — auto-generated per business process. Layout
   is fixed: KPI band + risk breakdown + engagement status + control
   coverage. User can re-skin (hide tiles) but not fundamentally alter.
2. **Custom dashboards** — user-built via a drag-drop builder. 12-col
   grid; widget sizes from 3×2 (small KPI) to 12×6 (wide chart).

**Widget types** (catalog): KPI tile, number + sparkline, line chart,
bar chart, donut, risk heatmap, control coverage bar, findings feed,
table, AI artifact (from a saved chat response).

**Editing mode**: enters when the `Edit dashboard` primary button is
pressed. Grid becomes 4px `paper-200` dashed; widgets gain a drag
handle (top-left) and a delete × (top-right). Click `Done` to exit.

#### 13.5.2 Reports

Reports are **narrative surfaces** — this is the flagship paper
(§paper-50) canvas application. Three sources:

- **From chat** — save an IRA session or artifact as a report section.
- **From template** — pick a template (Audit Summary, Board Briefing,
  Controls Review, Findings Digest), configure via an AI wizard modal.
- **From builder** — a drag-drop section builder (v1 limited).

**Report reader layout** (§5 Report reader):
- Serif body toggle (reader preference, persisted).
- 66ch body cap.
- Drop cap on section 1 para 1.
- Inline citations as `code-sm` pills (brand-50 / brand-700).
- Section breaks: 1px `paper-200` rule, 48px top/bottom margin.

**Report actions** (top-right of header): `Export PDF` (primary,
triggers the Playwright PDF service), `Export Excel`, `Export DOCX`,
`Share`.

**Approval chain** (1–3 steps, configurable per report): reviewers
appear as avatars under the title with their status (pending / approved
/ rejected / not yet requested). Clicking a pending avatar opens the
approval modal for that reviewer.

**Rules**:

- **Never** use the cool app canvas (#FCFAFD) for a report surface —
  reports are always on paper-50. This is the one clearly-differentiated
  surface in the whole system.
- **Never** truncate citation links — full text in citation pills,
  tooltip for long URLs.

#### 13.5.3 AI Concierge — Document Forensics

A specialized upload-and-analyze surface for single documents (contracts,
invoices, board minutes). Layout: two-column.

Left — file upload zone + page preview (`react-pdf` viewer).
Right — analysis results tabs: `Summary` · `Entities` · `Risks` ·
`Key dates` · `Anomalies`. Each entity is a clickable pill that
highlights its position on the document preview.

#### 13.5.4 AI Concierge — Table Extractor

Takes a PDF or image, returns structured tables. Left: document preview
with detected table regions outlined in `brand-600 / 0.40`. Right: tab
strip of extracted tables; active tab shows the table as a §4 DataGrid
with row-headers preserved. Export to Excel/CSV.

### 13.6 System

#### 13.6.1 Configuration

Data-source management. List of configured sources: DB connections,
SFTP drops, cloud-storage buckets, file libraries. Each row carries a
`TestSparkLine` mini-chart of recent ingestion health + a `Test
connection` ghost action.

#### 13.6.2 Users & Teams

Standard CRUD. User row: avatar + name + email + role pills (multiple
ok) + team pills + last-active time + status pill (Active, Invited,
Deactivated).

#### 13.6.3 Roles & Permissions

A **matrix view** — rows are roles (6 built-in + custom), columns are
capability groups (Governance, Execution, Workflows, Intelligence,
Admin). Each cell is a multi-checkbox (Read / Write / Approve / Admin).

**Never** use nested accordions here — flat matrix with column filters
scales best for the seven-persona matrix.

#### 13.6.4 System Settings

One-column form page. Grouped sections: Branding, Data retention,
Notifications, Integrations defaults, Security. Each section is a
`Card` (outlined) with inline fields.

#### 13.6.5 Integrations

Cards grid of integrations (Google Workspace, M365, Slack, Teams,
ServiceNow, Jira). Each card: logo, name, status pill (Connected,
Disconnected, Error), `Configure` ghost button.

#### 13.6.6 Audit Logs

Read-only data table with filter bar (§11.4) and a fast-jump date
picker. Columns: `Timestamp` (tabular) · `Actor` · `Action` · `Entity`
· `IP` · `Result` (severity pill). Clicking a row opens the §11.7
audit-trail drawer with the full before/after diff.

---

## 14. Roles & personas

Seven personas, each with distinct capabilities. The design system
respects these capabilities through RBAC (§11.8) — **never** expose
capabilities a role lacks.

| Role                              | Primary pages                                     | Can                                     | Cannot                                    |
|-----------------------------------|---------------------------------------------------|-----------------------------------------|-------------------------------------------|
| **Lead Auditor**                  | Home, Governance, Execution, Reports              | Full CRUD on assigned engagements       | Modify tenant config, manage users        |
| **Staff Auditor**                 | Execution, Workflows, IRA AI                      | CRUD on assigned controls/tests         | Approve findings, close engagements       |
| **Audit Manager**                 | Home, Planning, Dashboards, Reports               | Full CRUD, approve/reject, allocate     | Change platform settings                  |
| **Chief Audit Executive (CAE)**   | Home (KPIs), Dashboards, Reports                  | Read-all, export, present               | Edit governance records                   |
| **Risk Officer**                  | Governance (Risk, RACM)                           | CRUD on risks/controls                  | Change engagement scope                   |
| **IT / Data Admin**               | Configuration, Admin                              | System settings, user management        | Approve findings                          |
| **External Auditor** (read-only)  | Execution (read), Reports (read)                  | View shared items, comment              | Any CRUD, download source data            |

**UI tailoring rules**:

- **Home page** picks a different action-queue composition per role.
  Lead Auditors see engagement actions first; Risk Officers see new
  risks; CAE sees board-prep items.
- **Command palette** (§11.1) scopes its `Pages` section to the role's
  accessible routes. It never surfaces routes the user can't enter.
- **External Auditor** chrome: the app sidebar collapses to a single
  `ReadOnlyBanner` with the shared-item link. No workspace selector.
  No bell inbox. No ⌘K.
- **CAE dashboards** get a subtle `paper-50` background (read as
  "executive reading surface") even though they're inside the app
  shell — this is the only place the report canvas leaks into the app
  shell.

---

## 15. Composition recipes — domain patterns

These are **composition recipes**, not new primitives. Each recipe is a
known-good combination of existing components for a repeat GRC need.

### 15.1 Severity pill + text

The canonical inline severity indicator. Pill (§10.10) + label — no
icon, no abbreviation.

```tsx
<Pill tone="error">Critical</Pill>   // risk
<Pill tone="warning">High</Pill>      // high
<Pill tone="warning">Medium</Pill>    // mitigated
<Pill tone="success">Low</Pill>       // compliant
<Pill tone="info">Info</Pill>         // evidence
```

### 15.2 Entity reference chip

When an entity (risk, control, finding) is referenced in prose, use:

```tsx
<EntityChip
  icon={<Shield size={14} />}
  id="R-0087"
  label="Privileged access review stale"
  href="/governance/risks/R-0087"
/>
```

Visual: 24px tall pill-ish (radius `r-sm`), `paper-50` bg, 1px
`paper-200` border, mono ID in `ink-500`, label in `ink-900 body-sm`,
icon `ink-500`. Hover: border `paper-300`, bg `paper-0`. This is the
**only pill** that breaks the no-border rule — because it's an entity
reference, not a category badge.

### 15.3 KPI tile

Standard card block used across Home and dashboards:

```
Card (outlined), 240×140, radius r-lg.
Header: label token uppercase in ink-500 — "OPEN RISKS"
Metric: display-md serif in ink-900 — "142"
Sub-metric: body-sm ink-500 with delta glyph — "↑ 12% vs Q4"
Optional: 40px sparkline, `brand-600` stroke, no fill.
```

### 15.4 Empty-state variants

Three flavors, picked by context:

- **First-use** — illustration (`paper-300` linework), heading serif
  ("No risks yet"), body ("Create your first risk or import from an
  existing RACM."), primary + ghost CTA row.
- **Filtered-out** — no illustration. Heading `ink-900` sans ("No
  results match these filters."), body in `ink-500` ("Try widening the
  date range or clearing the severity filter."), link-variant
  "Clear all filters" button.
- **Error** — `AlertCircle` `risk` 32px icon, heading sans ("Something
  went wrong loading this list."), body with the error code (`ink-500`,
  mono short hash), `Retry` secondary + `Report issue` ghost.

### 15.5 Confirmation destructive modal

Delete / retire / close actions:

```
Size: sm (400px), radius r-xl.
Header: display-sm serif "Delete this engagement?"
Body: body ink-700 — "You'll lose all linked tests, evidence, and
      workpapers. This cannot be undone."
Footer: [Cancel — ghost] [Delete engagement — destructive]
Extra: optional "Type DELETE to confirm" input for irreversible ops
       on top-level entities.
```

### 15.6 Quick-add inline form

Adding a risk / control / finding without leaving the list:

- Inline row appears as the **top row** of the table when `+ Add` is
  clicked.
- Row height matches data rows (44/32 by density).
- Inputs are borderless; on focus, a `brand-600` 2px bottom line
  appears (signal: "this is the input, not a cell").
- Save (`⌘↵`) commits and moves to the next row. Escape cancels.

### 15.7 Slide-over detail editor

Used for: control detail, risk detail, finding detail, user detail.

```
Position: right, full-height, 520px (md) or 720px (lg).
Radius: r-lg on the left edge only.
Shadow: shadow-xl.
Header: title heading-md + close × + breadcrumb above.
Body: scroll region with tabs (§10.6 underline).
Footer: sticky, paper-0, 1px paper-200 top. [Cancel] [Save changes].
```

### 15.8 Status banner

Page-level banners for maintenance, stale data, or consent prompts.

```
Position: sticky below page header.
Height: 56px.
Composition: tone icon (left, 20px) + body (body-sm) + action button
             (ghost, right-aligned) + close × (optional).
Tones: info (evidence), warning (mitigated), error (risk), announce
       (brand — brand-50 bg, brand-700 text, brand-200 border).
```

**Never** stack more than one banner. If multiple are active,
prioritize: error > warning > announce > info.

---

## 16. Content voice

The UI is the product's voice. These rules are load-bearing — break
them only if you can defend the break in a PR description.

### 16.1 Tense & person

- **Imperative for actions**: "Save assessment", "Export report" —
  not "Saving" or "Will save".
- **Past for confirmations**: "Saved." not "Save successful."
- **Present for state**: "3 risks open" — not "3 risks are currently open."
- **Second person for the user** when addressing: "You have 3 items"
  not "There are 3 items for the user."

### 16.2 Sentence case, always

- Buttons, menu items, table headers, page titles — sentence case.
- **Never** Title Case. **Never** ALL CAPS (except `label` token).
- Proper nouns keep their casing. "SOX", "IRA", "Q1 2026" stay as-is.

### 16.3 Numbers

- Spell out one through nine in body prose ("three risks"), use
  numerals for ≥10 ("12 findings").
- Exception: in data contexts (tables, KPIs, chart labels) always
  use numerals regardless of magnitude.
- Always use tabular nums (`numeric` token) for numbers in tables
  and KPIs.
- Percentages use `%` with no space ("12%" not "12 %"). Currency uses
  ISO codes for non-USD contexts ("EUR 1,200" not "€1,200" in
  enterprise views).

### 16.4 Dates

- Display dates as `Apr 28, 2026` by default.
- Display date-times as `Apr 28, 2026, 14:32 UTC` in audit contexts
  (never relative — auditors need precision).
- Use relative ("12 days ago") in ambient/social surfaces: Home,
  notifications, activity feeds. Pair with an absolute date in the
  `title=` / tooltip.

### 16.5 Severity language

- Spell severity out: `Critical`, `High`, `Medium`, `Low`, `Info`.
- When combined with counts: "3 critical findings" — lowercase
  severity inside a sentence; capitalized only when used as a pill label.
- Avoid: `Crit.`, `Hi`, `red-flag`, `blocker`, `P0`. The canon is the
  five words above.

### 16.6 AI voice

- IRA speaks in the **first person singular** when responding: "I
  found…", "I'll need to know…", "I can't answer that without more
  context."
- IRA **never apologizes in excess** — one "sorry" per turn, max, and
  only when the failure is IRA's (not the user's).
- IRA **never refers to itself as "AI" or "the assistant"**. Say "IRA"
  or "I".
- IRA **never hedges with "it seems" or "probably"** when the data is
  clear. Hedge only when the data is genuinely ambiguous.
- When IRA doesn't know, it says so in one sentence + the next best
  step: "I don't see an approved Q1 control set for this process. You
  can import one from the 2025 RACM, or I can draft a starter set from
  the SOP."

### 16.7 Error messages

- **Never** expose stack traces or internal IDs by default. Short code
  OK in small text.
- Structure: what happened (one sentence) + what to do (one sentence).
- "We couldn't load your findings. Retry, or reach out to your admin if
  this keeps happening." — not "Error: 500 Internal Server Error at
  /findings endpoint".

---

## 17. Accessibility, semantics, and performance

WCAG AA is a **contractual constraint** — GRC buyers carry accessibility
clauses in procurement. This section is the system-level contract that
every component in §§4, 10, 12, 13, 15 must satisfy. If a pattern in
those sections contradicts §17, §17 wins.

### 17.1 Semantic HTML first

Always reach for the native element before wrapping a `div`. Shadcn
components already do this — the rule is *don't un-do* it.

| Use                                     | Not                                                 |
|-----------------------------------------|-----------------------------------------------------|
| `<button>`                              | `<div role="button" onClick>`                       |
| `<a href>`                              | `<div onClick={navigate}>`                          |
| `<nav>`, `<main>`, `<aside>`, `<header>`, `<footer>` | `<div>` soup                                        |
| `<label for="…">` + `<input id="…">`     | Placeholder-only inputs                             |
| `<table>` + `<thead>`/`<tbody>`/`<th>`   | Divs with grid CSS (OK for TanStack Table but must carry `role="grid"` + `role="row"` + `aria-colindex`) |
| `<section aria-labelledby="…">`          | `<section>` with no label when it's a landmark      |

**Rules**:

- **Page-level landmarks**: every page has exactly one `<main>` (the
  content panel), one `<nav>` per nav region (sidebar, in-page tab bar),
  a footer only on reports. The app sidebar is a single `<nav aria-label="Primary">`.
- **Skip link** — the first focusable element on every page is a
  visually-hidden-until-focused `Skip to main content` link that jumps
  to `#main`. Required because the sidebar has many nav items.
- **Heading hierarchy**: one `<h1>` per page (the page-header title).
  Don't skip levels — going `<h1>` → `<h3>` breaks screen-reader TOC.

### 17.2 ARIA (only when semantics aren't enough)

| Situation                                                 | Pattern                                                                                     |
|-----------------------------------------------------------|---------------------------------------------------------------------------------------------|
| Icon-only button                                          | `aria-label="Close menu"` on the `<button>`; the Lucide icon gets `aria-hidden="true"`      |
| Decorative icon inside a labelled surface                  | `aria-hidden="true"` on the icon, label comes from the surrounding button/link text         |
| Async status (streaming AI, workflow run, upload progress) | Live region: `<div aria-live="polite" aria-atomic="true">` outside the DOM reflow path     |
| Form-level error summary                                  | `role="alert"` on the summary container; autofocus the first invalid field                  |
| Streaming AI caret                                         | Caret element `aria-hidden="true"` so the streaming text isn't polluted by "blinking cursor" announcement |
| Modal / dialog                                             | Radix `Dialog` handles it: `role="dialog"`, `aria-modal="true"`, focus trap, `Esc` to close, focus returns to trigger |
| Toast (non-interrupting)                                   | `aria-live="polite"` for info/success, `aria-live="assertive"` for error                    |
| Loading spinner                                           | Wrap in `<span role="status">` with a visually-hidden label — "Loading risks…"              |
| Table sort                                                | `aria-sort="ascending \| descending \| none"` on the active `<th>`                         |
| Expanded/collapsed row                                    | `aria-expanded` on the trigger; `aria-controls` pointing at the disclosed panel's id        |
| Selected multi-select pill                                | `aria-pressed="true"` on the toggle-chip button                                             |

**Rules**:

- **Never** put `aria-label` on something that already has a visible
  label — it silently **overrides** the visible text for screen readers.
- **Never** announce severity by color alone (§2 already rules this); a
  pill's label text is its ARIA name automatically.
- **Never** use `role="alert"` for non-urgent content — it interrupts
  the screen reader mid-sentence. Use `aria-live="polite"` for most
  things; reserve `assertive`/`alert` for blockers.

### 17.3 Keyboard navigation

Every interactive pattern must survive a no-mouse audit. Run the full
app with the pointer physically disconnected once per release.

**Global contract**:

- Tab order matches **visual** reading order — top→bottom, left→right
  (English / LTR). Don't use positive `tabindex` to shuffle; use DOM
  order.
- `Esc` closes any overlay (modal, popover, palette, drawer). The
  closing surface returns focus to the element that opened it.
- Focus ring is the `glow-brand` token (§6). **Never** `outline: none`
  without an equally-visible replacement.

**Per-pattern**:

| Pattern                   | Keys                                                                                    |
|---------------------------|-----------------------------------------------------------------------------------------|
| Command palette (§11.1)   | `⌘K` open · `↑/↓` move · `↵` open · `⌘↵` new tab · `Esc` close · `Tab` to footer hints |
| Data table (§4)           | `↑/↓` row · `←/→` column · `⌘↑/⌘↓` page jump · `Space` toggle select · `↵` open row    |
| Underline tabs (§10.6)    | `←/→` move selection · `Home/End` first/last · `↵` or auto-focus on selection           |
| Segmented tabs (§10.6)    | same as underline tabs                                                                  |
| Dropdown menu (§10.3)     | `↑/↓` move · `↵` select · `Esc` close · typeahead letters jump                          |
| Select (§10.4)            | `↑/↓` move · `↵` select · letters typeahead                                            |
| Date picker (§10.5)       | arrow keys day · `PgUp/PgDn` month · `Shift+PgUp/Dn` year · `Enter` select             |
| Dialog (§10.12)           | Radix-default focus trap · `Esc` close                                                  |
| Drawer / slide-over (§15.7) | `Esc` close · Tab cycles within drawer                                                  |
| Toast (§10.9)             | `F8` moves focus into notification region (OS hook); each toast tabbable                |
| Chart (§2 viz)            | Arrow keys move cursor between data points · `↵` opens detail · provides table fallback |

**Rules**:

- **Never** trap keyboard focus inside a non-modal surface. Only
  `Dialog`, `Sheet`, and `CommandPalette` trap; the rest let `Tab`
  escape.
- **Never** intercept `Tab` to perform app actions. `Tab` is sacred.

### 17.4 Forms

The shadcn Form + react-hook-form + Zod pattern is mandatory for any
form over three fields. It wins four things at once: type-safe values,
declarative validation, automatic accessible error association, and a
single place for server errors to land.

```tsx
const schema = z.object({
  riskId: z.string().min(1, "Required."),
  severity: z.enum(["critical", "high", "medium", "low"]),
});

const form = useForm<z.infer<typeof schema>>({
  resolver: zodResolver(schema),
});

<Form {...form}>
  <FormField
    control={form.control}
    name="riskId"
    render={({ field }) => (
      <FormItem>
        <FormLabel>Risk ID</FormLabel>
        <FormControl>
          <Input leftIcon={<Search size={16} />} {...field} />
        </FormControl>
        <FormDescription>Use the registry ID, not the display name.</FormDescription>
        <FormMessage />
      </FormItem>
    )}
  />
</Form>
```

**What this guarantees for accessibility**:

- `<FormLabel>` renders `<label htmlFor={id}>`; `<FormControl>`
  receives the same `id`. Screen readers associate them automatically.
- `<FormDescription>` is linked via `aria-describedby`.
- `<FormMessage>` renders with `role="alert"` when the field is
  invalid and is linked via `aria-errormessage`. **Never** render
  custom validation text outside `FormMessage` — it won't announce.

**Error placement**:

- Inline `FormMessage` directly below the field (default) — `body-sm`,
  `risk` color, `AlertCircle` 14px icon left-inline.
- Plus a **form-level summary** at the top of the form when the user
  submits and validation fails: `role="alert"`, `risk-50` bg,
  `AlertOctagon` icon, list of fields with anchor links that focus the
  offending input.

**Rules**:

- **Never** disable the submit button until the form is valid — it
  hides *why* the user can't submit. Let it be clickable; validation
  runs on submit, focus moves to the first invalid field.
- **Never** rely on browser-native tooltips for error text — they
  aren't announced and don't match the system's typography.
- **Never** clear a filled field after a server error. Preserve
  values; show the error; let the user edit.

### 17.5 Async content: skeletons, live regions, loading buttons

**Skeletons over spinners for anything larger than a button.** A
spinner tells the user "wait"; a skeleton tells them "this is what's
coming." GRC pages carry high information density — skeletons preserve
scroll position and page rhythm.

- Table: render header row + 8 placeholder rows with `Skeleton` cells
  (see §10.14).
- Card: render header + 2 text-line skeletons + sub-metric skeleton.
- Chart: render the axis + a muted area silhouette; animate the
  shimmer only if `prefers-reduced-motion: no-preference`.

**Loading buttons**: already defined in §10.1 — spinner in `paper-0`
color, **label stays visible** ("Saving…", not "…"), `pointer-events:
none`, `aria-busy="true"`. Never replace the label with an ellipsis.

**Aria-live wrapping**: the conversation column, the live findings
feed, and toast region each sit inside their own `aria-live="polite"
aria-atomic="false"` wrapper. The rest of the page is static to the
screen reader.

### 17.6 Performance contract

| Concern                      | Rule                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------|
| Font loading                 | `font-display: swap` on all three faces (Inter / Source Serif 4 / JetBrains Mono). Self-host + preload the two most-used weights (Inter 400, 600) |
| Image optimization           | Evidence thumbnails, avatars, report figures: WebP with AVIF fallback + `srcset` for 1×/2×. `loading="lazy"` below-the-fold |
| Virtualization threshold     | Any list >50 rows uses `@tanstack/react-virtual` or equivalent. Risk Register, Control Library, Findings, Audit Logs, chat message list all pre-meet this threshold |
| React Compiler               | Enabled project-wide (per `CLAUDE.md` §1.1). Don't add `memo`/`useMemo` manually unless profiling demands it |
| Bundle splitting             | Each route is a separate chunk (App Router default). Artifact panel, Report reader, AI Concierge tools are deferred — dynamic-import when the route opens |
| CLS (layout stability)       | Always reserve space for async content (skeleton dimensions must match real content height). AI streaming output grows from the bottom — reserve the `Result` container's min-height so the surrounding layout doesn't jump |
| Motion budget                | No continuous animation (no permanent pulses, marching ants, rotating gradients). State-transition only (§5 motion) |
| Streaming chart pause        | Any real-time chart has a visible **Pause stream** button — required for `prefers-reduced-motion` users and for cognitive-load accessibility |

### 17.7 Z-index scale

An explicit numeric scale prevents the `z-index: 9999` arms race. Only
these values are legal. Anything else is a bug.

| Token         | Value | Use                                                                 |
|---------------|-------|---------------------------------------------------------------------|
| `z-base`      | 0     | Default flow                                                         |
| `z-raised`    | 10    | Sticky page-header row, sticky table filter bar, sticky table header |
| `z-sticky`    | 20    | Sticky table column (first column pinned), sticky action bar         |
| `z-overlay`   | 30    | Popover, dropdown menu, select popover, tooltip                      |
| `z-modal`     | 50    | Dialog / drawer scrim + content                                      |
| `z-toast`     | 60    | Toast stack (sonner default)                                         |
| `z-palette`   | 70    | Command palette (above toasts; intentionally wins focus)              |
| `z-notification-toast` | 70 | Escalated from `z-toast` when an error toast must not be occluded |
| `z-devtools`  | 9999  | Only for dev/storybook overlays — **never** in production code       |

**Rule**: `z-index` must always reference a token from this table.
Raw numeric `z-index` on a component is a lint violation.

### 17.8 High-contrast / reduced-motion / forced-colors

The system already respects `prefers-reduced-motion` (§7). Complete
the triangle:

- **`prefers-contrast: more`** — bump all `ink-500` to `ink-700`,
  `paper-200` to `paper-300`, and every pill's text weight to 640.
  These swaps are deterministic — implement as a CSS media block.
- **`forced-colors: active`** (Windows High Contrast) — let the OS
  take over colors but keep layout intact. Don't use background images
  for meaningful UI (status icons must be real SVG, not `background:
  url(…)`).
- **Focus ring** — in `forced-colors`, the `glow-brand` ring collapses
  to `outline: 3px solid Highlight`. The purple disappears but the
  shape stays.

### 17.9 Internationalization readiness

Per CLAUDE.md: i18n-ready, RTL deferred to v2.

- All copy originates in a single strings module (`copy.ts` per
  feature). No inline strings in JSX beyond `label` and `aria-label`.
- All labels accept number and date formatter args — never concatenate
  ("3 findings" is `t("findings.count", { n: 3 })`, not `` `${n} findings` ``).
- CSS writes to **logical** properties where layout matters:
  `padding-inline-start` over `padding-left`, `margin-inline-end` over
  `margin-right`. This is the seam that makes the RTL flip painless in
  v2.

---

## 18. Data visualization accessibility

Charts are the hardest accessibility surface in a GRC product — they
carry the most information and the fewest affordances for assistive
tech. Every chart shipped by this system follows the four-channel
rule.

### 18.1 Four-channel rule

Encode data on **at least two** of these four channels. Color is
**never** the only channel.

| Channel   | Examples                                                    |
|-----------|-------------------------------------------------------------|
| Color     | Series color, severity hue, heat intensity                  |
| Position  | Bar length, scatter X/Y, line altitude                      |
| Shape / pattern | Series marker (circle / square / diamond / cross), stripe overlay on heatmap cells, dashed vs solid for forecast vs actual |
| Text      | Value label on bar, tooltip number, legend label             |

**Required combinations by chart type**:

| Chart              | Required channels                                                 |
|--------------------|-------------------------------------------------------------------|
| Bar / column        | Position + Text (value label either above or right-aligned)       |
| Line                | Position + Text (endpoint label) + Shape on markers when overlapping |
| Donut / pie         | Text (% label) + Legend with text; shapes not needed               |
| Risk heatmap (§13.2.4) | Color (diverging scale) + Text (count) + Pattern (optional stripe on Critical cells for `prefers-contrast: more`) |
| Forecast            | Solid line actual + Dashed line forecast + Shaded confidence band + Legend text |
| Real-time streaming | Color + Text (current value, fading trail) + Pause button          |

### 18.2 Screen-reader fallback

Every `<svg>` chart is accompanied by a **data table**, hidden by
default but reachable via a "View as table" link-variant button
immediately below the chart. The table is real `<table>` with `<th
scope="col">` headers and captions.

```tsx
<figure role="group" aria-labelledby="c1-title">
  <figcaption id="c1-title">Open findings by severity, Q1 2026</figcaption>
  <svg aria-describedby="c1-table" focusable="false">…</svg>
  <details>
    <summary>View as table</summary>
    <table id="c1-table">…</table>
  </details>
</figure>
```

### 18.3 Chart interaction keyboard contract

- Focus enters the chart via `Tab`; arrow keys traverse data points.
- `↵` opens the detail view for the focused point.
- `Esc` releases focus back to page flow.
- Focused data point carries a 2px `brand-600` ring and a tooltip
  that is also announced via `aria-live="polite"`.

### 18.4 Pattern overlay tokens (high-contrast mode)

When `prefers-contrast: more` is active, these SVG patterns layer over
the severity/risk colors for redundant encoding:

| Severity  | Pattern                                    |
|-----------|--------------------------------------------|
| Critical  | Diagonal stripes, 45°, 2px dark on tint    |
| High      | Cross-hatch, 4px, 1px dark on tint         |
| Medium    | Dotted, 2px, 3px spacing                   |
| Low       | Solid fill (no pattern — already low-contrast-safe) |
| Info      | Horizontal stripes, 3px, 4px spacing        |

Patterns live as `<pattern>` defs in a shared SVG sprite at
`/assets/patterns.svg` and are applied via `fill="url(#pattern-critical)"`.

---

## License & attribution

This `DESIGN.md` is the canonical specification for the design system.
Treat it as the source of truth. If UI and this document disagree, this
document wins until explicitly amended.

Format inspired by the `getdesign.md` 9-section convention. Tuned for
GRC SaaS; assumes React 19 + Tailwind v4 + shadcn/ui + Radix primitives.

_Last refined: 2026-04-23 — dark sidebar + cool canvas app shell; paper tokens re-roled for report surfaces._
_Expanded: 2026-04-23 — §§11–16 added: cross-cutting patterns, AI surfaces,
domain patterns, personas, composition recipes, content voice. Pulled
from the Auditify/IRA platform (github.com/tech-irame/auditify-revamp)
as the reference consumer._
_Reviewed: 2026-04-23 — §§17–18 added after ui-ux-pro-max audit: systematic
accessibility (ARIA / keyboard / forms / semantics), performance contract
(font-display / virtualization / z-index scale), and chart-accessibility
four-channel rule._
