# Tailwind Universal Design System

A brand-neutral, token-driven design system for building **e-commerce, travel & booking, SaaS, marketplace, corporate and admin-dashboard** interfaces on Tailwind CSS conventions. Every value is a CSS custom property that maps one-to-one onto a Tailwind theme extension, so the same components can carry a minimal corporate identity, a warm travel brand or a dense fintech console without being redesigned.

## Sources

**None were supplied.** No codebase, Figma file, brand guideline, logo or font binary was attached to this project — the brief was a written specification ("Company description: Tailwind"). Everything here is authored from scratch against Tailwind CSS's own conventions (4px spacing base, `sm/md/lg/xl/2xl` breakpoints, 50→950 colour ramps, semantic utility naming).

Consequences a reader should know about:

- **There is no logo.** Wherever a mark would go, the word mark is rendered in plain type (Inter 800, −0.04em). Nothing was drawn or reconstructed.
- **Fonts are substitutions.** No font files were provided; the system uses **Inter** (UI + display) and **JetBrains Mono** (code, IDs, tabular figures), loaded from Google Fonts. If you have real brand fonts, drop the binaries into `assets/fonts/` and replace the `@import` in `tokens/fonts.css` with `@font-face` rules — no other file needs to change.
- **Icons are Lucide 0.454** from jsDelivr, masked to `currentColor`. No proprietary icon set was available.
- **All imagery is placeholder.** Every image slot in the UI kits renders a neutral `.ph` block with a Lucide glyph.

---

## Index

| Path | What it is |
|---|---|
| `styles.css` | The single entry point consumers link. `@import` list only. |
| `tokens/` | `fonts · colors · typography · spacing · radius · shadows · layout · motion · base` |
| `components/` | 42 React primitives in five groups (`icon`, `forms`, `display`, `feedback`, `navigation`) + their CSS |
| `guidelines/` | 17 foundation specimen cards (colour, type, spacing, radius, elevation, grid, states, motion) |
| `ui_kits/commerce/` | "Aera" storefront: home, listing, product, cart drawer, checkout |
| `ui_kits/travel/` | "Wayfare" booking: results, tour detail, booking + confirmation |
| `ui_kits/dashboard/` | "Console" admin: overview, orders table + drawer, settings |
| `SKILL.md` | Agent-Skills wrapper so this folder works inside Claude Code |

**Hierarchy:** Foundation → Tokens → Components → Patterns (UI kits) → Pages.

---

## CONTENT FUNDAMENTALS

The default voice is **plain, second-person and unhurried**. It states what a thing does and what happens next; it does not sell inside the interface.

- **Person.** Address the user as *you*. The product refers to itself as *we* only in transactional confirmations ("We've emailed your itinerary"). Never *I*.
- **Casing.** Sentence case everywhere — buttons, headings, table headers, menu items, tabs. The only uppercase is the 11px overline/eyebrow label with `--tracking-wider`. No Title Case Buttons.
- **Verbs first on actions.** "Add to cart", "Fulfil order", "Save changes", "Clear filters" — never "Submit", "OK", or a bare noun.
- **Numbers are specific.** "312 pieces", "Showing 49–72 of 312", "vs last 30 days". A metric without a comparison baseline does not ship.
- **Errors say what to do.** "Enter a valid Eircode", not "Invalid input". "The issuing bank rejected the charge. Ask the customer for another card." Blame the system or state the fact; never the user.
- **Empty states name the cause and the exit.** "No results for 'merino' — try removing a filter" + a Clear filters button.
- **Length.** Buttons 1–3 words. Helper text one sentence. Card descriptions ≤ 2 lines. Marketing paragraphs ≤ 44ch wide.
- **Punctuation.** No exclamation marks. Ellipsis only in placeholders ("Search products"). Currency always with symbol and thousands separator: `$48,120`.
- **No emoji.** Not in UI copy, labels, badges, empty states or marketing. Status is carried by a Badge with a dot, never by a coloured square emoji.
- **Vibe:** *competent and quiet*. Compare — marketing: "Wardrobe staples, built to outlast the season." App: "Only 3 places left on this departure." Both are factual; neither uses hype adjectives.

---

## VISUAL FOUNDATIONS

**Colour.** Sky (`#0284c7` at 600) is the single action colour; slate is the neutral; teal is the secondary accent used sparingly for data and non-action emphasis. Semantic colours are emerald / amber / red / blue. Components never reference a ramp step directly — they reference a semantic alias (`--bg-primary`, `--text-secondary`, `--border-default`). That indirection is what makes rebranding a token edit. Light and dark themes are the same alias set redefined under `[data-theme="dark"]`; dark mode lifts the primary to the 500/400 steps so it stays legible on near-black.

**Type.** Inter throughout, JetBrains Mono for code, order IDs, prices in tables and any figure that must align. Display and heading sizes are fluid `clamp()` values so a page reflows between mobile and large desktop without breakpoint overrides; body sizes are fixed (18/16/14/13/12/11). Tracking tightens as size grows (−0.03em on display, 0 on body). Headings are 600–800 weight; body is 400; UI labels are 500. Line height 1.15 on headings, 1.5 on UI text, 1.65 on long-form prose. `text-wrap: balance` on headings, `pretty` on paragraphs.

**Spacing & layout.** 4px base, Tailwind steps. Cards pad 24, stacks gap 16, control clusters gap 8, sections use a fluid `clamp(3rem, …, 6rem)`. Containers cap at 1280 (2xl 1440) with 32px desktop gutters, 24 tablet, 16 mobile. 12-column grid, 24px gap. Dashboard shell: 264px sidebar (72px collapsed), 64px header, both sticky.

**Backgrounds.** Flat colour only: `--bg-page` (slate-50) behind, `--bg-surface` (white) for cards and bars. No gradient backgrounds, no textures, no patterns, no illustration washes. The *only* sanctioned gradients are (a) the bottom-up protection gradient on overlay image cards — `linear-gradient(180deg, transparent 35%, rgba(2,6,23,.78))` — so white text on photography always clears 4.5:1, and (b) the shimmer sweep inside skeletons.

**Cards.** 12px radius, 1px `--border-default`, white surface, `overflow: hidden`. Two elevations: **flat** (border only — the default inside dashboards) and **raised** (border + `--shadow-sm` — for marketing surfaces over the tinted page). Interactive cards lift 2px and go to `--shadow-lg` on hover, and their media zooms 4%.

**Shadows.** Cool slate-tinted, never black, never coloured. Five steps (xs→xl) used strictly by layer: xs on resting buttons, sm on raised cards, md on small popovers, lg on dropdowns/drawers/hovered cards, xl on modals. Dark theme swaps to deeper, more opaque black shadows since ambient contrast is lower.

**Borders & radii.** 1px borders at three strengths (subtle / default / strong) — dividers use subtle, containers default, form controls strong on hover. Radii: 4 small, **8 controls**, **12 cards**, 16 large surfaces and modals, 24 rare, full for pills, avatars and switch tracks.

**Animation.** Short and unshowy. 120ms for hover/focus colour changes, 180ms for menus, tooltips, accordions and modals, 280ms for drawers and progress fills. One curve does almost everything: `cubic-bezier(.2,0,0,1)`. A spring (`cubic-bezier(.34,1.3,.64,1)`) appears in exactly two places — the switch thumb and toast entry. Entrances fade + rise 4–12px. Nothing bounces, nothing rotates except spinners, nothing exceeds 420ms. All durations collapse to 0 under `prefers-reduced-motion`.

**Interaction states.** Consistent and mechanical: **hover** darkens the fill one ramp step (or fills with `--bg-hover` for ghost controls); **active** darkens two steps and nudges 0.5px down; **focus** is always a 2px `--border-focus` ring offset by a 2px surface-coloured gap (`--focus-ring`), identical on every control; **selected** uses `--bg-selected` with brand-coloured text; **disabled** drops to the neutral `--bg-disabled` surface with `--text-disabled` ink and no shadow — never a faded primary; **loading** keeps the control's exact size and swaps the label for a spinner; **error** and **success** re-colour the border and the ring, never the fill.

**Transparency & blur.** Used in two places only: the modal/drawer scrim (`rgba(15,23,42,.55)` + 8px backdrop blur) and the alpha-tinted semantic surfaces in dark mode. Text is never set in a translucent colour — full-opacity ink only, so contrast is predictable.

**Imagery.** Where real imagery exists it should be cool-toned and unfiltered, shot on neutral ground, no heavy grade and no grain. Product media is 4:3, travel media 3:2, hero media 4:3, avatars square-cropped to circles. Everything in this repo is a placeholder block.

**Fixed elements.** Marketing header is sticky with a 1px bottom border (no shadow until scrolled). Dashboard sidebar and header are both sticky. Booking/checkout summary cards stick at `top: 90px`. Toasts pin bottom-right, 24px from the edges.

---

## ICONOGRAPHY

**Lucide 0.454**, pulled from `cdn.jsdelivr.net/npm/lucide-static`. No icon set was provided with the brief, so this is a flagged substitution: Lucide's 2px round-cap outline style matches the system's density and weight, and is the closest CDN-available match to a neutral modern UI set.

- **Delivery.** The `Icon` component fetches the Lucide SVG once per name (cached) and inlines its markup, so the glyph strokes inherit `currentColor` and no SVG is ever hand-drawn. Names are Lucide kebab-case (`shopping-cart`, `chevron-down`, `triangle-alert`).
- **Sizes.** 16 in dense UI (buttons sm/md, table rows, inline labels), 20 default, 24 for touch targets and empty-state marks. Never scale a glyph past 28 — use an illustration slot instead.
- **Colour.** Icons take `--text-secondary` at rest and `--text-primary` on hover. Semantic icons take the matching `--text-success/-warning/-error/-info`. Stars in ratings are the one fixed exception: `--color-warning-500` filled, `--color-neutral-300` empty.
- **No emoji, ever**, and no Unicode pictographs as icons. The only non-Lucide glyphs in the system are the typographic `·` separator, `—` in ranges, `→` in inline links and `…` in truncation.
- **No icon font, no sprite sheet**, no `assets/icons/` directory — the CDN fetch is the whole mechanism, and it needs network access. To vendor icons for offline or production use, download the Lucide SVGs you use into `assets/icons/` and repoint `BASE` in `components/icon/Icon.jsx`.
- **Pairing rule.** Every icon-only control needs a `label` (it becomes both `aria-label` and the tooltip). Decorative icons inside labelled controls are `aria-hidden`.

---

## Components

42 exports, all reachable from the compiled bundle namespace.

**Icon** — `Icon`

**Forms** — `Button`, `IconButton`, `FormField`, `Input`, `Textarea`, `Select`, `SearchField`, `Checkbox`, `Radio`, `Switch`, `Slider`, `FileUpload`, `DatePicker`

**Display** — `Card`, `Badge`, `Tag`, `Avatar`, `AvatarGroup`, `StatCard`, `ProductCard`, `DestinationCard`, `PricingCard`, `Rating`, `Table`, `Skeleton`, `Progress`, `EmptyState`

**Feedback** — `Alert`, `Banner`, `Toast`, `ToastViewport`, `Modal`, `Drawer`, `Tooltip`, `Spinner`

**Navigation** — `Tabs`, `Breadcrumbs`, `Pagination`, `Accordion`, `Dropdown`, `SidebarNav`

Each directory holds `<Name>.jsx`, `<Name>.d.ts` (props contract, with usage notes per prop) and `<Name>.prompt.md` (what & when, a usage example, variants). Interaction styling lives in the group's CSS file so real `:hover`, `:focus-visible`, `:disabled` and `:checked` states exist rather than being simulated inline.

### Intentional additions

No source defined a component inventory, so the set is authored from the brief. Two notes on scope:

- **`Icon`** is a wrapper, not a UI component — it exists so no other component ever inlines an SVG.
- Requested items **not** built as separate primitives: *Combobox* (use `Select`; a typeahead needs product-specific data wiring), *TimePicker* (use `Select` with time options), *Popover* (the `.ds-popover` class is provided; `Dropdown` and `Tooltip` cover the real cases). Say the word and they become components.

---

## Responsive behaviour

Breakpoints are Tailwind's: sm 640, md 768, lg 1024, xl 1280, 2xl 1536 (also exposed as `--bp-*`). The rules components follow:

- **Adapt, don't shrink.** Grids in the UI kits are `repeat(auto-fit, minmax(…, 1fr))`, so KPI rows, product grids and two-column page layouts reflow to fewer columns and then stack, rather than compressing. Tables scroll horizontally inside `.ds-table-wrap` rather than squeezing columns. Two narrow-viewport behaviours are specified but **not yet implemented in the kits**: the dashboard sidebar collapsing into a left `Drawer`, and listing filters moving into a bottom `Drawer` behind a Filters button. Both use components that already exist — wire them up per product.
- **Touch.** Any control that is primary on mobile uses `size="lg"` (48px) and `block`. Minimum hit target is 44px; `IconButton lg` is 48.
- **Type** is fluid via `clamp()`, so headings need no per-breakpoint overrides.

## Accessibility

Contrast is checked against the semantic pairs, not the ramps: `--text-primary` on `--bg-surface` is ~16:1, `--text-secondary` ~7:1, `--text-muted` ~4.6:1 (body-size minimum), `--text-on-primary` on `--bg-primary` ~4.8:1. Focus is a visible 2px offset ring on every interactive element, identical everywhere. Form controls pair with `FormField` labels and `aria-invalid`; errors render with `role="alert"`. Tabs, menus, dialogs, progress bars, sort headers and pagination carry the matching ARIA roles and states. Modals close on Escape and scrim click. Status is never colour-only — badges pair a dot with a word, errors pair colour with an icon and text.

## Tailwind mapping

Token names are already Tailwind-shaped. A `theme.extend` that reads the custom properties gives you `bg-primary`, `bg-surface`, `text-secondary`, `text-muted`, `border-default`, `bg-success`, `rounded-card`, `shadow-md`, `gap-6` and so on:

```js
// tailwind.config.js
theme: { extend: {
  colors: {
    primary: 'var(--bg-primary)', surface: 'var(--bg-surface)', page: 'var(--bg-page)',
    success: 'var(--bg-success)', warning: 'var(--bg-warning)', error: 'var(--bg-error)', info: 'var(--bg-info)'
  },
  textColor: { primary: 'var(--text-primary)', secondary: 'var(--text-secondary)', muted: 'var(--text-muted)' },
  borderColor: { DEFAULT: 'var(--border-default)', subtle: 'var(--border-subtle)', strong: 'var(--border-strong)' },
  borderRadius: { control: 'var(--radius-control)', card: 'var(--radius-card)', surface: 'var(--radius-surface)' },
  boxShadow: { xs: 'var(--shadow-xs)', sm: 'var(--shadow-sm)', md: 'var(--shadow-md)', lg: 'var(--shadow-lg)', xl: 'var(--shadow-xl)' }
}}
```

Rule of thumb: **no one-off values**. If a design needs a spacing or colour that is not a token, add the token.

## Rebranding checklist

1. Replace the three ramps in `tokens/colors.css` (primary, accent, neutral) — semantic aliases follow automatically.
2. Swap the two families in `tokens/fonts.css`; adjust `--tracking-*` if the new face is wider or narrower.
3. Set the personality dials: `--radius-card` (0 = corporate/fintech, 12 = default, 16–24 = consumer), `--shadow-*` (flatten for enterprise), `--space-section`.
4. Leave component files alone. If you are editing a `.jsx` to rebrand, a token is missing.
