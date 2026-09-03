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
