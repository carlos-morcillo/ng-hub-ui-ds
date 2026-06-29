# Changelog

All notable changes to `ng-hub-ui-ds` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
