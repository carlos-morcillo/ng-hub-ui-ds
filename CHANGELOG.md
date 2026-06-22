# Changelog

All notable changes to `ng-hub-ui-ds` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [22.1.0] - 2026-06-22

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
