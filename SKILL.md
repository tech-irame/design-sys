---
name: editorial-grc
description: Editorial GRC design system — the official, opinionated design language for the governance/risk/compliance SaaS platform. Activate whenever building UI, components, pages, or any React/Tailwind/shadcn interface that should match the Editorial GRC aesthetic. Triggers on explicit design requests ("build a button", "design a dashboard card", "make a risk register row", "render an AI response"), on any work mentioning GRC / governance / risk / compliance / audit / controls / evidence / findings, and on any file path under `app/`, `components/`, `ui/`, or similar frontend surfaces in a GRC product. The skill supplies the full DESIGN.md spec (tokens, typography, components, state matrices, refusal list) and ready-to-use patterns so generated UI lands on-brand on the first try.
---

# Editorial GRC — Design System Skill

You are building UI in the **Editorial GRC** design system. The canonical
spec lives in `./DESIGN.md` inside this skill folder. **Read it before you
start generating UI.** The quick-reference below is a cheat sheet — treat
DESIGN.md as the source of truth when they conflict.

---

## North-star check

> Would Anthropic ship this? If the surface reads calm, deliberate, and
> trustworthy — yes. If it reads busy, shouty, or corporate — redesign.

---

## Quick-reference tokens

### Colors (copy-paste ready)

```css
/* Brand (anchor = 600, dark anchor = 900) */
--brand-50:  #F7F0FF;
--brand-100: #EDDEFE;
--brand-200: #DCBBFD;
--brand-300: #C393FA;
--brand-400: #A366F0;
--brand-500: #8838DE;
--brand-600: #6A12CD;  /* anchor: buttons, links, primary */
--brand-700: #550FA5;  /* on-surface body text (AA) */
--brand-800: #3B0B72;
--brand-900: #26064A;  /* anchor: display, dark canvas */
--brand-950: #170330;

/* App canvas (chrome surfaces — dashboards, data, workflows) */
--canvas:          #FCFAFD;  /* app body bg — brand-600 at ~2% on white */
--canvas-elevated: #FFFFFF;  /* cards / modals on canvas */
--canvas-border:   #F0EAF6;  /* subtle card border on canvas */

/* Sidebar (dark shell — anchored to brand-900 every theme) */
--sidebar-bg:             #26064A;                    /* brand-900 */
--sidebar-border:         rgba(255 255 255 / 0.08);
--sidebar-text:           rgba(255 255 255 / 0.85);
--sidebar-text-dim:       rgba(255 255 255 / 0.55);
--sidebar-text-muted:     rgba(255 255 255 / 0.45);
--sidebar-surface:        rgba(255 255 255 / 0.06);
--sidebar-surface-hover:  rgba(255 255 255 / 0.08);
--sidebar-surface-active: rgba(255 255 255 / 0.12);   /* distinct from hover */
--sidebar-accent:         #FFFFFF;

/* Warm paper + ink (report surfaces only — reader, PDF, narrative) */
--paper-0:   #FFFFFF;
--paper-50:  #FAF7F2;  /* REPORT CANVAS — reader mode only */
--paper-100: #F3EEE5;
--paper-200: #E8E1D2;
--paper-300: #D6CCB7;
--ink-300:   #C2B9CB;
--ink-400:   #9A8FAE;
--ink-500:   #6B5D82;
--ink-600:   #4A3D62;
--ink-700:   #332848;
--ink-800:   #1F1433;  /* default body text */
--ink-900:   #0F0720;  /* display, max contrast */

/* GRC semantic (no pure red/amber/green) */
--risk:      #B42318;  /* Critical / Error / destructive */
--high:      #C2410C;  /* High severity */
--mitigated: #B45309;  /* Medium / mitigated / Warning */
--compliant: #15803D;  /* Low / Compliant / Success */
--evidence:  #0369A1;  /* Sources / Info-blue / Evidence */
--info:      #6A12CD;  /* Info (brand-tied) */
--draft:     #6B5D82;  /* Draft / Muted / Default */

/* Dark mode: canvas + report unify to #12081E, ink #F1EDE3. Sidebar
   stays brand-900 (#26064A) — it's always dark, every theme. */
```

### Typography

- **Display** (narrative hero only): `Source Serif 4`, weight 320–520,
  letter-spacing negative.
- **UI** (default everywhere): `Inter`, weight 400 / 520 (numeric) / 600
  (heading) / 560 (label uppercase 12px).
- **Mono** (AI responses, evidence IDs, code, receipts): `JetBrains Mono`.

Root = 16px. Use `rem`. Tabular numerics on every number.

### Spacing / radius

- 8pt grid: 2, 4, 6, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128.
- Radius: xs 4 · sm 6 · **md 8** (default) · lg 12 · xl 16 · 2xl 20 · full.

### Elevation

Borders first, shadows sparingly, tint never. Focus ring =
`0 0 0 4px rgba(106,18,205,0.24)`.

### Motion

- Durations: 75 / 150 / **200** / 300 / 500ms.
- Eases: `standard (0.2,0,0,1)`, `emphasized (0.3,0,0,1)`, `spring (0.34,1.56,0.64,1)`.
- State transitions only — never decoration. Always respect
  `prefers-reduced-motion`.

---

## App shell at a glance

- **Dark sidebar** (256px, `brand-900`) anchors every screen. White-opacity text scale, 3px white left bar on active items, weight-600 label. Every sidebar value comes from a `sidebar-*` token — never raw `rgba(255,255,255,x)`.
- **No topbar.** Global chrome lives in the sidebar. Page chrome is the first content row: **breadcrumb → title → context chips → actions**. Serif title for narrative pages, sans for registry/task pages.
- **Canvas by role** — app canvas `#FCFAFD` for dashboards/data/workflows; report canvas `#FAF7F2` (paper-50) for reader mode and PDFs only.
- **32px page padding.** Never 28.

## Always

- **Use serif for narrative hero** (reports, dashboard headline, AI response context). Everything else = Inter.
- **Tabular numerics on every number** — KPIs, table cells, risk scores, currencies.
- **Spell out severity**: `Critical` / `High` / `Medium` / `Low` — never abbreviate.
- **Snap to the 8pt grid.** If something wants 14px, use 12 or 16.
- **Reserve `brand-600` for signal.** Primary buttons, selected state, focus ring, links. Don't paint containers with it.
- **Write UI copy in full sentences** with a period.
- **Prefer borders to shadows** for card elevation.
- **Ship both densities** — every table must work at 32px row height.
- **Show AI thinking honestly** — pulse dots during generation, caret while streaming, timestamp when done.
- **Pills are flat**: tinted bg + label text. **No border. No icon.**

## Never

- **Never use** pure `#FF0000`, `#FFA500`, `#00FF00` — use the GRC semantic scale.
- **Never put** `brand-600` on small body text over `canvas` or `paper-50` (~4.0:1). Use `brand-700` for text.
- **Never write** raw `rgba(255,255,255, …)` in sidebar code — compose from `--sidebar-*` tokens.
- **Never break the 8pt grid** on page padding — use 24 or 32, never 28 or 20.
- **Never use** drop-shadows decoratively on cards, buttons, or sidebars.
- **Never animate** for decoration. No hover-bounce. No scroll-reveals.
- **Never center** body paragraphs outside of hero moments.
- **Never emoji** in UI copy — use Lucide icons.
- **Never** return a chat-bubble AI response with avatar circle. AI responses are considered prose, not chat bubbles.
- **Never** put a border or icon on a pill. (Toasts are the one exception — they keep a category icon.)
- **Never** abbreviate severity labels (`C`, `H`, `M`, `L`).
- **Never** use `text-transform: uppercase` on anything other than the `label` token.
- **Never** `fill=` on a Lucide icon — they're stroke-based. Use `color` + `currentColor`.

---

## Stack assumptions

- React 19 + Next.js 15 (App Router) + TypeScript (`strict`).
- Tailwind v4 with `@theme` block for tokens.
- shadcn/ui components over Radix primitives.
- Lucide icons (`lucide-react`).
- TanStack Table v8 for data grids; `@tanstack/react-virtual` for virtualization.
- Recharts for common charts; visx for custom GRC viz.
- RHF + Zod 4 for forms.
- Vercel AI SDK v6 + AI Elements for AI surfaces.
- Motion (`motion` package) for transitions — sparingly.

---

## Component cheat sheet

### Button

```tsx
// Sizes: sm (h-8), md (h-10), lg (h-12). Radius 8. Font weight 600.
// Variants: primary | secondary | ghost | destructive | link
// Icon: left | right | only (square) | none. Gap 8px.

<Button variant="primary" size="md" leftIcon={<Plus size={16} />}>
  Save assessment
</Button>
```

- **primary**: bg `brand-600`, text white. Hover `brand-500`, active `brand-800`.
- **secondary**: bg `paper-0`, border `paper-200`, text `ink-800`.
- **ghost**: transparent; hover `brand-50` bg + `brand-700` text.
- **destructive**: bg `risk` #B42318, text white.
- **link**: text `brand-700`, underline on hover only.
- Disabled = 50% alpha, no pointer events.
- Focus = `glow-brand` ring.

### Input

```tsx
// Sizes: sm (h-8), md (h-10), lg (h-12). Radius 8.
// States: default | focus | filled | error | success | disabled | read-only
// Compose: label · helper · error text · icon-left · icon-right · placeholder

<Input
  label="Risk ID"
  leftIcon={<Search size={16} />}
  placeholder="R-142"
  helperText="Use the registry ID, not the display name."
/>
```

- **default**: border `paper-200`, bg `paper-0`, text `ink-900`.
- **focus**: border `brand-600`, ring `brand-600/20` 3px.
- **error**: border `risk`, bg `risk/10` (~`risk-50`), focus ring `risk/20`.
- **success**: border `compliant`, bg `compliant-50`.
- **disabled**: bg `paper-100`, text `ink-400`.
- **read-only**: bg `paper-50`, text `ink-800`, no caret.

### Pill (flat — no border, no icon)

```tsx
// Sizes: sm (h-5), md (h-6 default), lg (h-7). Radius 999px.
// Variants (status): default | success | error | warning | info | disabled
// Variants (GRC severity): Critical | High | Medium | Low | Info — same visual treatment, different text.

<Pill tone="error">Critical</Pill>
<Pill tone="warning">High</Pill>
<Pill tone="success">Low</Pill>
```

- bg: `[semantic]-50`, text: `[semantic]-700` (light) / `[semantic]` (dark).
- Border: **none**. Icon: **none**. Label: always spelled out.

### Card

```tsx
// Radius 12. Default = outlined (1px paper-200 border, no shadow).
// Variants: outlined | elevated (shadow-md) | muted (paper-100 bg) | feature (brand-50 bg)

<Card variant="outlined">{…}</Card>
```

### AI Response (signature pattern — NOT a chat bubble)

```tsx
<AIResponse
  meta="Answered in 1.2s · 4 sources · model: risk-analyst-4"
  citations={[{id: "IT-GEN-04", href: "/evidence/it-gen-04"}]}
  streaming
>
  Three SOX IT General Controls failed in Q1 2026: <Citation id="IT-GEN-04" />
  (privileged access review — evidence stale by 47 days)…
</AIResponse>
```

- Container: rounded-xl, 1px gradient border (violet → magenta at 24% alpha).
- Bg: paper-0 + rgba(106,18,205,0.03) tint.
- Body: `body-lg` 17px, 66ch max.
- Citations: inline pill-shaped badge, JetBrains Mono `code-sm`, `brand-50` bg, `brand-700` text.
- Streaming cursor: 2px `brand-600` caret, 1.2s blink.
- Thinking dots: three `brand-400` dots, spring-easing pulse, 900ms stagger.

### Data table

```tsx
// TanStack Table v8. 44px rows comfortable / 32px compact.
// Selected row: brand-50 bg + 2px brand-600 left border. No heavy swap.
// Numeric columns: text-align right + tabular-nums.
```

### Toast (the one place an icon is kept)

```tsx
<Toast tone="success" icon={<CheckCircle />}>Saved.</Toast>
```

Tones: default · success · error · warning · info. Width 380px. Auto-dismiss:
info/success 5s, warning 8s, error = persistent until dismissed.

### Modal

Sizes: sm 400 / md 560 / lg 720 / xl 960 / fullscreen / auto. Radius 16,
shadow `shadow-xl`. Overlay `ink-900/40` + 4px backdrop-blur.

---

## GRC domain patterns (cheat sheet — full spec in DESIGN.md §§11–16)

### App-shell contract

- **⌘K is the only global search.** Two sections: pages + entities,
  always with "Ask IRA" as the last row. No second search input anywhere.
- **Workspace selector** sits at the top of the sidebar. Switching is a
  hard route change — never swap data in place.
- **Filter bar contract** — every list page has: search + status chips +
  date range + owner + severity + advanced-slide-over + view/density
  toggles. State persists to URL query-string.
- **Notifications** — toasts for ephemeral, inbox for durable.
  Never mix.
- **RBAC** — hide features a role can't see; disable with a tooltip
  when visible-but-not-allowed. External auditors get the read-only
  shell.
- **Audit trail drawer** on every detail page. Vertical timeline with
  before/after diffs; CSV export.

### AI / IRA signature patterns

- **Three-panel chat** (`/chat`): History 280 | Conversation flex |
  Artifacts 420–520. History is **inside** the page, never replaces
  the app sidebar.
- **Artifacts** has fixed tabs in pipeline order: `Plan` · `Code` ·
  `Sources` · `Result`. Only show tabs that have content.
- **Clarification** is inline chips — never a modal. Chips are
  secondary-variant `sm` buttons, `r-full`, click auto-sends.
- **Assumptions** surface above artifact tabs in a `brand-50` editable
  panel when IRA made inferences without asking.
- **Progressive loader**: one named row per pipeline step, dots →
  checkmarks → collapsed meta line.
- **Workflow builder canvas**: same 3-panel layout, but right panel is
  a read-only preview. User edits only via natural language in chat.

### Domain surfaces (IA)

```
HOME · IRA AI ·
GOVERNANCE (Processes · RACM · Controls · Risks · Planning) ·
EXECUTION (Engagements · Testing · Evidence · Findings) ·
WORKFLOWS ·
INTELLIGENCE (Dashboards · Reports · AI Concierge) ·
SYSTEM (Configuration · Admin)
```

Pattern notes:
- **Home** is action-oriented. Lead with an action queue row; KPI band;
  engagement Gantt; risk heatmap. No promotional content.
- **Governance** surfaces are registries (list + detail with tabs).
  Business Processes own 4 tabs exactly: SOP · RACM · Workflows · Risks.
- **RACM** is a specialized matrix, not a table. Redundant encoding
  (color + glyph). Never edit in-cell.
- **Risk heatmap** — 5×5 diverging scale, always carries count text.
- **Audit Planning v1** = Gantt only. Resources/budget deferred.
- **Engagements** run through 5 phases: Planned · In fieldwork · In
  review · Reporting · Closed. Stepper above detail tabs.
- **Findings** are cross-source (test / AI / manual). Mini-kanban for
  remediation. `AIResponse`-styled body when AI-authored.
- **Workflow library** — card grid. Detail → `/workflows/:id`. Run →
  `/workflows/:id/run` (executor) with live findings feed.
- **One-Click Audit** is a 4-step wizard routed from a process page;
  output is a consolidated cross-reference report.
- **Reports** are the only surface on **warm paper** canvas (`paper-50`
  / `#FAF7F2`). Serif body toggle, 66ch, drop-cap para 1. App surfaces
  stay on cool canvas (`#FCFAFD`).
- **AI Concierge** has two tools: Document Forensics + Table Extractor.
- **Roles** = 6 built-in + custom. Admin `Roles & Permissions` is a
  flat matrix, never nested accordions.

### Composition recipes (compose, don't invent)

- `EntityChip` — the one pill that carries a border (entity ref, not a
  category badge).
- `SeverityPill` — `<Pill tone=...>Critical|High|Medium|Low|Info</Pill>`.
  Always spelled out.
- `KPITile` — 240×140 outlined Card with label + `display-md` serif
  number + delta sub-metric.
- `EmptyState` — three flavors: first-use (illustration), filtered-out
  (no illustration), error (AlertCircle `risk`).
- `ConfirmDestructiveModal` — `sm`, serif title, destructive button,
  "Type DELETE" for top-level entities.
- `SlideOverEditor` — 520/720px right panel with tabs + sticky footer.
- `StatusBanner` — sticky below page header, single instance only.

### Content voice

- **Sentence case always**, except the `label` token.
- **Spell out severity** (`Critical`, `High`, `Medium`, `Low`, `Info`).
  Never `C/H/M/L` or `P0`.
- **IRA speaks first person**: "I found…", "I can't answer that without
  more context." Never "The AI thinks…".
- **Errors** structure: what happened (one sentence) + what to do (one
  sentence). Never raw 500s.
- **Dates** are `Apr 28, 2026` by default; absolute + UTC in audit
  contexts; relative only in ambient surfaces (with absolute in title).

---

## Workflow

1. **Read DESIGN.md** (in this folder) for any spec you don't have
   memorized. It's the source of truth.
2. **Compose, don't invent.** A "RiskPill" is a `Pill` with `tone="error"`
   and `"Critical"` label. A "KPI tile" is a `Card` with specific
   content structure. Don't create new primitives when composition works.
3. **Verify against the refusal list** in DESIGN.md §9 before finalizing —
   if any item applies, redo.
4. **Reference the preview files** at `./preview.html` and
   `./preview-dark.html` (if present) for visual confirmation of how
   tokens render in context.
5. **Deviate only with justification.** If you need to break a rule,
   leave a JSDoc explaining why.

---

## When in doubt

- Ask: is this data-dense or narrative? → sans for dense, serif for narrative.
- Ask: is this ephemeral or permanent? → toast for ephemeral, inline for permanent.
- Ask: is color doing work? → add a redundant text/position signal.
- Ask: does the user need this pixel-pushing? → probably not; default to the token.

The spec is opinionated, not dogmatic. When a real user need beats a
stylistic rule, the user need wins — but document it.
