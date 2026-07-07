# Changelog

All notable changes to `ng-hub-ui-ds` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [22.5.2] - 2026-07-07

### Changed

- **docs (token catalogue)** — documented the new `<hub-table>` scroll/selected-row tokens shipped in `ng-hub-ui-paginable` 22.6.0: `--hub-table-container-overflow`, `--hub-table-selected-bar-width`, `--hub-table-selected-bar-color` (public), plus the internal `--hub-table-cell-bar-*` relays. Documentation-only — no token or compiled-CSS changes.

## [22.5.1] - 2026-07-07

### Changed

- **docs (token catalogue)** — documented the new `<hub-table>` header chrome tokens in `docs/variables-css-library.en.md`: `--hub-table-head-font-size`, `--hub-table-head-font-weight`, `--hub-table-head-padding-x`, `--hub-table-head-padding-y` and `--hub-table-head-position` (shipped in `ng-hub-ui-paginable` 22.5.0). Documentation-only — no token or compiled-CSS changes.

## [22.5.0] - 2026-07-04

### Added

- **One-call partial theming — `theme()` mixin** (`styles/mixins/_theme.scss`, forwarded by the root Sass entry): pass only the overrides as partial maps (`$accents`, `$space`, `$gap`, `$radius`, `$shadow`, `$font-family/-size/-weight`, `$line-height`, plus a raw `$tokens` escape hatch) and it emits the matching custom properties with the canonical names — everything derived (sys aliases, role families, utilities, components) re-derives at runtime through the var() chain. Scopeable to `:root`, a `[data-theme]` block or any subtree.
- **Radius tokens `xl` / `xxl`** (`--hub-ref-radius-xl: 1rem`, `--hub-ref-radius-xxl: 2rem` and their `--hub-sys-radius-*` aliases), completing Bootstrap's radius scale — `.rounded-4` / `.rounded-5` are now emitted by the surfaces sheet.
- **Breakpoints** (`styles/mixins/_breakpoints.scss`, forwarded by the root Sass entry): the Bootstrap-compatible `$hub-breakpoints` map (sm 576 · md 768 · lg 992 · xl 1200 · xxl 1400, retunable via `with (…)`) plus `media-breakpoint-up($name)` / `media-breakpoint-down($name)` mixins.
- **Responsive utility variants** (mobile-first, Bootstrap-exact names) generated for the highest-traffic groups: display (`.d-{bp}-*`), 12-column spans (`.col-{bp}-1…12`), spacing (`.p/.px/.py/.pt/.pb/.ps/.pe-{bp}-*`, `.m…-{bp}-*`, auto margins) and gap. Other groups get their responsive variant in consumer code with `media-breakpoint-up()`.
- **Focus ring**: `focus-ring()` helper mixin over the (previously unconsumed) `--hub-sys-focus-ring-width/color` tokens, plus the `.focus-ring` utility.
- **Background / text opacity hooks**: `bg()`, `text-bg()` and `text-color()` now emit their colour through the local custom properties `--hub-bg-opacity` / `--hub-text-opacity` (default 1, via `color-mix`), and the sheets add Bootstrap's `.bg-opacity-10/25/50/75/100` and `.text-opacity-25/50/75/100`.
- **Link utilities & mixin**: `link-color($variant)` (accent link with `-emphasis` hover) and the `.link-{variant}`, `.link-underline(-{variant})`, `.link-underline-opacity-0…100` (via `--hub-link-underline-opacity`), `.link-offset-1…3` and `.icon-link` classes.
- **`.bg-gradient`** and **print display utilities** (`.d-print-none/inline/inline-block/block/grid/table(-row/-cell)/flex/inline-flex`).
- **Surface mixins** (`styles/mixins/_surfaces.scss`, forwarded by the root Sass entry): `bg($variant, $subtle)` over the open accent map plus `body` / `transparent`, `text-bg($variant)` (accent background + guaranteed-contrast `-on` text), `border($width, $color)`, `border-color($variant)`, `radius($size)` (none | sm | md | lg | pill | circle) and `shadow($size)` (none | sm | md | lg | inset).
- **Helper mixins** (`styles/mixins/_helpers.scss`, forwarded by the root Sass entry): `visually-hidden()`, `stretched-link()`, `ratio($x, $y)` (native `aspect-ratio`) and `clearfix()`.
- **Surface utility sheet** (`styles/utilities/surfaces.scss` / `.css`, exported as `./styles/utilities/surfaces`): Bootstrap-exact helpers built on the surface mixins — backgrounds (`.bg-primary` … `.bg-dark`, `.bg-*-subtle`, `.bg-body`, `.bg-transparent`, `.bg-white/black`), `.text-bg-*`, borders (`.border`, per-side add/remove, `.border-{variant}` colours, `.border-1…5` widths), radii (`.rounded`, `.rounded-0…3`, `.rounded-circle`, `.rounded-pill`, per-side variants), shadows (`.shadow-sm/.shadow/.shadow-lg/.shadow-none`) and `.opacity-0/25/50/75/100`. `.rounded-4` / `.rounded-5` are not emitted — the ds radius scale has no xl/xxl tokens yet.
- **Layout sheet expansion** (`styles/utilities/layout.scss`), all Bootstrap-exact: per-side spacing (`.pt/.pb/.ps/.pe-*`, `.mt/.mb/.ms/.me-*` on the 0–5 scale, logical properties), auto margins (`.m-auto`, `.mx-auto`, `.ms-auto` …), `.row-gap-*` / `.column-gap-*`, table display helpers (`.d-table(-row/-cell)`), position (`.position-*`, `.top/bottom/start/end-0/50/100`, `.translate-middle(-x/-y)`, `.fixed-top/bottom`, `.sticky-top/bottom`), overflow (`.overflow-*` plus `-x`/`-y` axes), `.order-first/0…5/last`, `.align-content-*`, float (`.float-start/end/none`, `.clearfix`), `.visible`/`.invisible`, `.z-n1/0…3`, `.object-fit-*`, vertical alignment (`.align-baseline/top/middle/bottom/text-top/text-bottom`), interactions (`.user-select-*`, `.pe-none/.pe-auto`) and the behaviour helpers (`.visually-hidden`, `.visually-hidden-focusable`, `.stretched-link`, `.ratio` + `.ratio-1x1/4x3/16x9/21x9`).
- **Typography mixins** (`styles/mixins/_typography.scss`, forwarded by the root Sass entry): `text-truncate()`, `text-break()`, `font-family($family)`, `font-size($size)` — Bootstrap's heading scale 1–6 derived from the base token, or the xs/sm/base/lg steps —, `font-weight($weight)`, `line-height($height)` and `text-color($variant)` over the open accent map plus the `body` / `muted` document roles.
- **Text utility sheet** (`styles/utilities/text.scss` / `.css`, exported as `./styles/utilities/text`): Bootstrap-exact helpers built on the typography mixins — alignment (`.text-start/center/end`), wrapping (`.text-wrap/nowrap`, `.text-break`, `.text-truncate`), transform (`.text-lowercase/uppercase/capitalize`), decoration (`.text-decoration-none/underline/line-through`), weight & style (`.fw-lighter/light/normal/medium/semibold/bold/bolder`, `.fst-italic/normal`), size (`.fs-1…6`), line-height (`.lh-1/sm/base/lg`), `.font-monospace`, and semantic text colours (`.text-primary` … `.text-dark`, `.text-body`, `.text-muted`, `.text-white`, `.text-black`, `.text-reset`).
- **Native-element reset** (`styles/base/reset.scss` / `.css`, exported as `./styles/base/reset`): an opt-in, token-driven reboot of the browser defaults — `box-sizing: border-box`, body typography/surface from `--hub-ref-*` / `--hub-sys-*`, heading/paragraph/list margins on the spacing scale, link colors from `--hub-sys-link-*`, monospace for `code`/`pre`, form controls inheriting the document font, and sensible `hr`/`table`/`fieldset` normalization. Load it only when the host app does not already ship a reset (e.g. Bootstrap's Reboot).

### Removed

- **BREAKING**: the `hub-`-prefixed utility sheet (`styles/utilities/layout.hub.scss` / `.css`) and its `./styles/utilities/layout.hub` package exports. The ds now ships a single, unprefixed utility sheet: `styles/utilities/layout`, whose helper names mirror Bootstrap's exactly. Migration: update imports from `ng-hub-ui-ds/styles/utilities/layout.hub` to `ng-hub-ui-ds/styles/utilities/layout` and rename classes — `.hub-stack` → `.stack`, `.hub-d-flex` → `.d-flex`, `.hub-gap-3` → `.gap-3`, `.hub-row`/`.hub-col-6` → `.row`/`.col-6`, `.hub-w-50` → `.w-50`, `.hub-justify-*` → `.justify-content-*`, `.hub-items-*` → `.align-items-*`, `.hub-self-*` → `.align-self-*`, and `.hub-grid` → `.grid-auto`. Do not load the sheet AND Bootstrap globally in the same document (the names now overlap by design; the spacing scale already matched Bootstrap's).
- **BREAKING**: the Tailwind-style flex aliases `.flex-1`, `.flex-auto`, `.flex-initial` and `.flex-none` — helper classes mirror Bootstrap exactly, which has no such utilities. Use `.flex-fill` / `.flex-grow-*` / `.flex-shrink-*` instead.

### Changed

- **Size scales are now generated from public Sass maps** — `$hub-space-scale`, `$hub-radius-scale` and `$hub-gap-steps` (`!default`, retunable via `with (…)`) are the single source for the `--hub-ref-space-*` / `--hub-ref-radius-*` blocks and their `sys` aliases, mirroring the `$hub-accents` pattern. Emitted CSS is unchanged except `--hub-sys-radius-pill`'s dead-code fallback, normalized from `9999px` to the ref value `50rem`.
- The layout primitives of the utility sheet (`.stack`, `.cluster`, `.grid-auto`, `.row`, `.col-*`, `.center`) are now emitted from the canonical layout mixins instead of duplicating their CSS — no behaviour change; the mixins remain the single source of truth.
- **BREAKING**: the flexbox alignment utilities of the unprefixed sheet now use Bootstrap's exact names — `.justify-start|end|center|between|around|evenly` → `.justify-content-*`, `.items-start|end|center|baseline|stretch` → `.align-items-*`, `.self-auto|start|end|center|baseline|stretch` → `.align-self-*`.

## [22.4.5] - 2026-07-02

### Added

- Token-spec MD: new `INTERNAL` status in the Components legend for variables the component writes at runtime (from inputs/config/state) — inventoried so every variable in code has a row, but explicitly not themable hooks.
- Token-spec MD: documented 35 previously missing component variables — the `--hub-dropdown-header-*` / `--hub-dropdown-divider-color` hooks (buttons), the `--hub-nav-mobile-*` drawer hooks, the `--hub-milestone-pulse-*` / `--hub-milestone-reveal-*` animation hooks, `--hub-stepper-nav-title-max-width`, and the `INTERNAL` runtime variables of badges (`--hub-badge-group-*`), nav (`--hub-nav-sticky-top`), skeleton (`--hub-skeleton-node-*`), milestones (`--hub-milestone-index`), panels (`--hub-panels-multiple-vertical-panel-min-width`) and forms slider (`--hub-slider-from/-to/-percent`).

### Changed

- Token-spec MD: the formal component-token regex required three name segments (`{2,}`), invalidating the dominant `--hub-{component}-{property}` pattern (89 legitimate tokens like `--hub-badge-bg`); relaxed to `{1,}`.
- Token-spec MD: the "Tokenization coverage" appendix was a stale snapshot (e.g. `paginable` listed at 22.4% — it is now 84.8%); regenerated with current per-library numbers, dated methodology notes and updated priorities (`buttons` is now the lowest at 70.6%).
- Token-spec MD: the "Standalone neutral colors" table wrongly claimed `secondary` / `light` / `dark` derive no role family — they are `$hub-accents` variants and derive the full family like every other variant. Split into "Neutral variant accents" (with `neutral` added) and "Standalone brand aliases" (`--hub-sys-color-brand-default` / `-on-default`, the only true base-only tokens).
- Token-spec MD: the "Directional spacing rule" now records the grandfathered logical-suffix exceptions (modal margin cascade, `--hub-nav-mobile-*-padding-inline`, `--hub-table-batch-actions-margin-inline-end`) and clarifies that single-value spacing tokens may keep the bare `-padding` suffix.
- Token-spec MD: 213 "Initial value" cells re-synchronized from the actual code declarations (new value-parity guard below) — including the canonical accent-slot derivations (oklch, 12% subtle / 80% emphasis) that panels, toast and nav now share, and the new `--hub-speed-dial-label-bg` / `--hub-speed-dial-label-color` tokens from buttons 22.7.0.
- `tokens-parity.mjs` guard extended: library scan now covers `.ts` / `.html` (inline component styles count as public API), consumed-only hooks (`var(--hub-x, fallback)` without a declaration) must now have an MD row, and `INTERNAL` rows are checked for existence in code like `IN_USE` ones. A new **value-parity check (D)** compares every component row's "Initial value" cell against the token's declaration in the file named by its Source column (tolerant normalization; `url(data:)` icons and Sass-interpolated values exempt), and `--write` rewrites drifted cells from code.

- Token-spec MD: `--hub-table-filter-count-bg` / `--hub-table-filter-count-color` were still marked `PENDING` but have shipped in paginable — promoted to `IN_USE` (a new parity sub-check now flags any PENDING/PROPOSAL row whose token is declared in code).

- Token-spec MD: adversarial re-audit fixes — 27 `Source` cells pointed at ghost files (24 legacy `accordion/*` rows → retargeted to the panels bridge `panels.variables.scss`; 3 `form/*` → the real forms fieldset component) and 60% of `Source` line numbers had drifted (675 cells renumbered); `url(data:)` icon values are no longer exempt from value parity (3 had drifted — `--hub-check-input-checked-icon` documented a different glyph entirely) and the descriptive icon placeholders were replaced by the real data URIs; the Figma-mapping sections now use real tokens as examples; `--hub-avatar-size` reclassified `IN_USE` → `INTERNAL` (written from the `size` input; a CSS override is overruled by the inline host style); the three `--hub-form-fieldset-border-*` values re-synced to the fallbacks the fieldset actually consumes.
- `tokens-parity.mjs`: two more guards — **check E** validates every `Source` cell (file exists, contains the token, right line; `--write` retargets/renumbers) and **check F** keeps each library's `docs/css-variables-reference.md` "Default" cells in sync with the code declarations (254 cells resynchronized on first run).

### Removed

- Token-spec MD: the superseded `tabs` proposal section (23 `--hub-tabs-tab-*` PENDING rows) — the tabs UI shipped in `ng-hub-ui-panels` as `--hub-panels-tab-*`; a tombstone note now points there.
- Token-spec MD: 49 superseded PENDING rows in the `select` section — the `--hub-select-btn-*` block shipped as the `--hub-select-button-*` tokens, and the `--hub-select-checkbox-input-*` / `--hub-select-radio-input-*` proposals were dropped in favour of the `check` component tokens the implemented select actually uses.

## [22.4.4] - 2026-07-01

### Changed

- Token-spec MD: documented the `<hub-input>` affix and clear-button tokens added in `ng-hub-ui-forms` 22.3.0 — `--hub-input-icon-color` / `--hub-input-icon-size`, `--hub-input-affix-inset` / `--hub-input-affix-gap`, and `--hub-input-clear-icon` / `--hub-input-clear-size` / `--hub-input-clear-color` / `--hub-input-clear-hover-color`. Docs only — no change to the emitted tokens.

## [22.4.3] - 2026-07-01

### Changed

- Token-spec MD: documented the six `--hub-icon-*` component tokens (`size`, `color` and the variable-font axes `fill` / `weight` / `grade` / `optical-size`), added by the new `ng-hub-ui-icons` 22.0.0 library. Docs only — no change to the emitted tokens.

## [22.4.2] - 2026-06-29

### Changed

- Token-spec MD: documented the `--hub-breadcrumb-max-item-width` component token (added in `ng-hub-ui-breadcrumbs` 22.3.0 for opt-in item truncation). Docs only — no change to the emitted tokens.

## [22.4.1] - 2026-06-29

### Changed

- Token-spec MD: documented the `--hub-badge-max-width` component token (added in `ng-hub-ui-badges` 22.4.0 for content truncation). Docs only — no change to the emitted tokens.

## [22.4.0] - 2026-06-26

### Added

- **Open, user-extensible semantic accent map.** The set of variant names is no longer hard-coded: it is driven by a configurable `$hub-accents` Sass map (`!default`). Consumers can redefine the defaults or **add any number of custom variants** (e.g. `brand`, `accent`, `tertiary`) — each one automatically gets its full derived role family (`-subtle`, `-border-subtle`, `-emphasis`, `-on`). Two entry points, no per-library recompile:
    - `@use 'ng-hub-ui-ds/styles/tokens/hub-tokens' with ($hub-accents-extra: (brand: #ff6b00))` — additive: keeps the defaults and merges your variants (recommended).
    - `with ($hub-accents: (...))` or defining `$hub-accents` before importing — full replacement.
- **Neutral variants in the default set.** `secondary`, `neutral`, `light` and `dark` are now first-class accents that derive the same role family as the chromatic ones (9 default variants total).
- **`--hub-sys-color-{variant}-on` contrast pair** for every variant. A grayscale on-color derived from the accent's own lightness via relative-color syntax (`oklch(from … )`), so dark accents resolve to white text and light accents to near-black — recomputed live with the accent, no second token to maintain.
- **Canonical structural layer.** New tokens: `--hub-ref-space-6/7`, sizing (`--hub-sys-size-full/-auto/-min/-max/-fit` and fractions `-1-2/-1-3/-2-3/-1-4/-3-4`), responsive container widths (`--hub-sys-container-max-width-sm…xxl`), grid (`--hub-sys-grid-columns/-gutter-x/-gutter-y`) and a semantic gap scale (`--hub-sys-gap-0…5`).
- **Layout mixins** (`@use 'ng-hub-ui-ds' as hub`): `hub.stack`, `hub.cluster`, `hub.grid`, `hub.grid-fixed`, `hub.row` + `hub.col($span)` (12-column grid) and `hub.center`.
- **Opt-in utility sheets** in two flavours sharing one naming rule — canonical `hub-` prefixed (`styles/utilities/layout.hub`) and unprefixed (`styles/utilities/layout`): a 12-column grid (`row` + `col-1…12`), display/flex helpers, directional padding/margin (`p/px/py`, `m/mx/my` 0–5), gap, and width/height sizing (`w-auto`, `w-25/50/75/100`, `vw-100`, `vh-100`, `min-vh-100`, …).
- **External-system bridge mixins** (opt-in): `hub.bridge-bootstrap`, `hub.bridge-tailwind`, `hub.bridge-material`, `hub.bridge-open-props`, each with `$mode: adopt | project | both` (hub adopts the host's tokens, or projects its theme onto the host).
- The canonical token spec (`docs/variables-css-library.en.md`) now ships **inside this package** as the single source of truth.

### Changed

- Semantic role derivation (`-subtle` / `-border-subtle` / `-emphasis`) now mixes `in oklch` instead of `in srgb` for perceptually smoother tints.
- `package.json` exposes new `exports` (`.`/`styles`, `styles/mixins/*`, `styles/utilities/*`) and a `build:styles` script that compiles tokens **and** the utility sheets.

### Removed

- **`--hub-sys-color-{variant}-dark`** (legacy back-compat alias of `-emphasis`). Consume `-emphasis` (or the new `-on` for contrast text).

## [22.3.1] - 2026-06-25

### Fixed

- The default / `light` theme accents are no longer silently overridden by the Bootstrap bridge: `:root` and `[data-theme='light']` now re-assert the ref-based accents (and surfaces/text/border) after the bridge block, instead of resolving through `--bs-*` when Bootstrap is present.
- Removed the stray `--hub-sys-color-primary-dark` Bootstrap override so all five variants derive `-dark` from the canonical `-emphasis` alias.

## [22.3.0] - 2026-06-24

### Added

- `--hub-sys-color-brand-default` and `--hub-sys-color-brand-on-default` semantic tokens. `brand` is the default accent consumed by component theme mixins (e.g. `ng-hub-ui-buttons` / `ng-hub-ui-badges`); it aliases the active theme's `primary`, so it re-colours automatically per theme.

## [22.2.0] - 2026-06-24

### Added

- **`body` / `main` base (shell) layer**: new inheritable tokens that standardise the application-shell layout so a vertical or horizontal aside reads one consistent token set.
    - **`--hub-body-*`** — the outer app/page wrapper. Twelve tokens (`width`, `margin-x/-y`, `padding-x/-y`, `row-gap`, `column-gap`, `bg`, `border-color`, `border-style`, `border-width`, `border-radius`) that **inherit from the matching `--hub-container-*` tokens** (with `sys`/`ref` fallbacks), so the container spacing system drives the whole page.
    - **`--hub-main-*`** — the content region: `bg`, `border-radius`, `padding-x`, `padding-y`.
    - **`--hub-main-wrapper-*`** — the centered wrapper around the content region: `bg`, `border-radius`, `gap`, `padding-x`, `padding-y` and `max-width` (default `1200px`).
- All tokens are live, re-basable CSS custom properties; paired spacing uses the canonical directional `-x` / `-y` form only (no `padding`/`margin` shorthand).

### Added

- **`container` base layer**: 22 inheritable `--hub-container-*` tokens (typography, visual and layout) bridging `sys` tokens to concrete containers/slots. Acts as a **re-base hook layer** with real spacing defaults (`padding: space-3`, gaps `space-2`): overriding one container token on a subtree re-bases every descendant container that reads it (e.g. `panels`). Paired spacing uses the canonical directional `-x`/`-y` form only — `--hub-container-padding-x/-y` and `--hub-container-margin-x/-y`, with no `padding`/`margin` shorthand.
- **Primitive tokens**: `--hub-ref-font-size-xs` and `--hub-ref-font-weight-semibold`, completing the canonical font scales.
- **`--hub-sys-color-ink`**: per-theme contrast target that flips `-emphasis` toward white on dark/terminal surfaces.
- **`build:tokens` script** (+ `prepublishOnly`) so `hub-tokens.css` is always recompiled from `hub-tokens.scss`, never hand-edited or stale.

### Changed

- **Semantic colour families are now CSS-variable-first.** A theme sets only the accent (`--hub-sys-color-{variant}`); `-subtle`, `-border-subtle` and `-emphasis` are derived once in `:root` with `color-mix()` against the contextual `--hub-sys-surface-page` / `--hub-sys-color-ink`. Overriding a single accent — even on a subtree — recomputes the whole family at runtime, with no per-theme boilerplate. Replaces the per-theme ramp maps + `hub-semantic-colors` mixin (now `hub-color-accents` + `hub-color-derive`).
- Regenerated `hub-tokens.css` from source (was stale: missing the `sys` radius/shadow-md/surface aliases already present in the SCSS).

### Notes

- `--hub-sys-color-{variant}-dark` is kept as a back-compat alias of `-emphasis`.


## [22.0.0] - 2026-06-17

### Changed

- Aligned with Angular 22.
- README documentation standardized.


## [1.0.0] - 2026-06-16

Initial release. The shared design-token foundation for the ng-hub-ui family,
extracted from the documentation app so every library reads one source of truth.

### Added

- **Primitive (`ref`) tokens**: full colour ramps (`--hub-ref-color-*`), spacing, radii, border widths, typography and icon sizing.
- **Semantic (`sys`) tokens**: surfaces, text, borders, shadows, focus ring, z-index, opacity, state overlays, transitions, and the semantic colour families.
- **Semantic colour families** generated from a per-theme SCSS map by the `hub-semantic-colors` mixin — each of `primary` / `success` / `danger` / `warning` / `info` exposes a uniform set: base, `-subtle`, `-dark`, `-border-subtle`, `-emphasis`.
- **8 built-in themes**: `light` / `base`, `bootstrap` (+ Bootstrap bridge), `dark`, `sunset`, `forest`, `mono`, `terminal` — switched with `[data-theme='…']`.
- **Two consumption paths**: the compiled `hub-tokens.css` (drop-in for any app) and the `hub-tokens.scss` source (override tokens via standard CSS custom properties).
