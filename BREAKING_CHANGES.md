# Breaking Changes - ng-hub-ui-ds

This document tracks all breaking changes in the `ng-hub-ui-ds` package.

## v22.9.0

### The Bootstrap bridge is gone: Bootstrap no longer drives the semantic tokens

- **Change**: a block of `--hub-sys-*` declarations resolved through Bootstrap's own variables
  (`--hub-sys-color-primary: var(--bs-primary, #0d6efd)`, and the same for `secondary`,
  `success`, `danger`, `warning`, `info`, `dark`, plus `--bs-body-bg`, `--bs-body-color`,
  `--bs-light` and `--bs-border-color`). It has been deleted. Every token now comes from this
  package's own ref layer.
- **Impact**: only an application that loads Bootstrap **and** relied on its palette to retint
  ng-hub-ui. If you set `--bs-primary` and expected `--hub-sys-color-primary` to follow, it no
  longer does. Nothing else changes: with Bootstrap absent, every one of those declarations
  already resolved to its fallback, so the rendered values are identical.
- **Migration**: set the hub token directly — `:root { --hub-sys-color-primary: #7c3aed; }` — which
  is what the token file's own header has always recommended. To keep a Bootstrap-driven theme,
  re-declare the bridge in your own stylesheet; it was ten lines.
- **Why**: the bridge made a published package's public API depend on whether an unrelated
  framework happened to be loaded, and its selector matched every theme, so a consumer could not
  opt out of it.

## v22.4.0

### `--hub-sys-color-{variant}-dark` is gone

- **Change**: every variant used to emit a `--hub-sys-color-{variant}-dark` token — a
  back-compat alias that resolved to `--hub-sys-color-{variant}-emphasis` and nothing else.
  The derivation mixin no longer writes it, so `var(--hub-sys-color-primary-dark)` (and the
  same for every other variant) now resolves to nothing.
- **Impact**: any stylesheet that reads the token. A CSS custom property that resolves to
  nothing fails silently — the declaration is dropped and the element falls back to its
  inherited or initial value — so this breaks quietly, at paint time, with no build error.
  Note the token that survives: `--hub-sys-color-dark` is the *`dark` variant's accent*, a
  different thing from the retired `-dark` **role** of each variant.
- **Migration**: `-emphasis` for the same colour the alias resolved to (legible text over the
  variant's `-subtle` background), or the `-on` token added in this same release for text and
  icons laid **on** the solid accent.
- **Why**: the alias enumerated the roles a second time while meaning nothing new, and 22.4.0
  opened the accent map so consumers can add their own variants — every extra role in the
  derivation loop is emitted once per variant, for every variant anyone ever adds.

> This entry was written after the fact. The removal shipped in 22.4.0 with a `### Removed`
> line in the changelog and no entry here; in this repository the major version tracks Angular
> and can never signal a break, which makes this file the only warning a consumer gets.
