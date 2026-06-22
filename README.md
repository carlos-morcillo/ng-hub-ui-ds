# ng-hub-ui-ds

[Español](./README.es.md) | **English**

The shared **design-token foundation** for the [ng-hub-ui](https://hubui.dev/)
family. It ships the canonical `--hub-ref-*` (primitive) and `--hub-sys-*`
(semantic) CSS custom properties — colour ramps, spacing, radii, typography,
surfaces, semantic colours, shadows, focus ring and more — with light/dark and
**8 built-in themes**.

Import it **once** and every ng-hub-ui library (panels, forms, calendar, …)
reads the same palette. Re-theme in one place and the whole family follows.

> Framework-agnostic — it is just CSS variables. There is no Angular or JS
> dependency; ship the compiled CSS or the SCSS source.

## Documentation and Live Examples

This package is part of [Hub UI](https://hubui.dev/), a collection of Angular
component libraries for standalone apps.

- Docs: https://hubui.dev/design-system/
- Hub UI: https://hubui.dev/

## 🧩 Library Family `ng-hub-ui`

This package is the design-token foundation the rest of the **ng-hub-ui**
ecosystem reads from:

- [**ng-hub-ui-accordion**](https://www.npmjs.com/package/ng-hub-ui-accordion) (deprecated — use ng-hub-ui-panels)
- [**ng-hub-ui-action-sheet**](https://www.npmjs.com/package/ng-hub-ui-action-sheet)
- [**ng-hub-ui-avatar**](https://www.npmjs.com/package/ng-hub-ui-avatar)
- [**ng-hub-ui-board**](https://www.npmjs.com/package/ng-hub-ui-board)
- [**ng-hub-ui-breadcrumbs**](https://www.npmjs.com/package/ng-hub-ui-breadcrumbs)
- [**ng-hub-ui-calendar**](https://www.npmjs.com/package/ng-hub-ui-calendar)
- [**ng-hub-ui-dropdown**](https://www.npmjs.com/package/ng-hub-ui-dropdown)
- [**ng-hub-ui-ds**](https://www.npmjs.com/package/ng-hub-ui-ds) ← You are here
- [**ng-hub-ui-forms**](https://www.npmjs.com/package/ng-hub-ui-forms)
- [**ng-hub-ui-history**](https://www.npmjs.com/package/ng-hub-ui-history)
- [**ng-hub-ui-milestones**](https://www.npmjs.com/package/ng-hub-ui-milestones)
- [**ng-hub-ui-modal**](https://www.npmjs.com/package/ng-hub-ui-modal)
- [**ng-hub-ui-nav**](https://www.npmjs.com/package/ng-hub-ui-nav)
- [**ng-hub-ui-paginable**](https://www.npmjs.com/package/ng-hub-ui-paginable)
- [**ng-hub-ui-panels**](https://www.npmjs.com/package/ng-hub-ui-panels)
- [**ng-hub-ui-portal**](https://www.npmjs.com/package/ng-hub-ui-portal)
- [**ng-hub-ui-skeleton**](https://www.npmjs.com/package/ng-hub-ui-skeleton)
- [**ng-hub-ui-sortable**](https://www.npmjs.com/package/ng-hub-ui-sortable)
- [**ng-hub-ui-stepper**](https://www.npmjs.com/package/ng-hub-ui-stepper)
- [**ng-hub-ui-utils**](https://www.npmjs.com/package/ng-hub-ui-utils)

---

## 📋 Table of Contents

1. [🧩 What is it and what is it for?](#-what-is-it-and-what-is-it-for)
2. [📦 Installation](#-installation)
3. [🚀 Import](#-import)
4. [🧱 Architecture: the two layers](#-architecture-the-two-layers)
5. [🎨 Semantic colours](#-semantic-colours)
6. [🌗 Themes](#-themes)
7. [🛠️ How to customise it](#️-how-to-customise-it)
8. [🧩 SCSS functions (how it is generated internally)](#-scss-functions-how-it-is-generated-internally)
9. [📋 Quick reference table](#-quick-reference-table)
10. [📊 Changelog](#-changelog)
11. [🤝 Contribution](#-contribution)
12. [☕ Support](#-support)
13. [📄 License](#-license)

---

## 🧩 What is it and what is it for?

Every ng-hub-ui library is themed with `--hub-*` CSS variables, but it does
**not define** the colours: it only **consumes** them (with sensible
fallbacks). This package is **the single source of truth** for those variables.

Without it, each library would use its fallback values in isolation. With it:

- **One single palette** feeds panels, forms, calendar, board… all at once.
- **Re-theme once** (a single token) and the change propagates across the whole
  family.
- **Dark mode and 8 themes** ready, switchable with one attribute.
- You can use it in **your own CSS** too (`var(--hub-sys-color-info-subtle)`),
  so your UI matches the components.

---

## 📦 Installation

```bash
npm install ng-hub-ui-ds
```

It has no dependencies. It is pure CSS/SCSS.

---

## 🚀 Import

Import it **once**, at the root of your application. Pick one path:

### Drop-in CSS (any app, no Sass required)

```css
@import 'ng-hub-ui-ds/styles/tokens/hub-tokens.css';
```

or in `angular.json`:

```json
"styles": [
  "node_modules/ng-hub-ui-ds/styles/tokens/hub-tokens.css",
  "src/styles.scss"
]
```

### SCSS source (if you use Sass)

It emits exactly the same `:root` rules, and lets you reference the source:

```scss
@use 'ng-hub-ui-ds/styles/tokens/hub-tokens';
```

Every ng-hub-ui component already reads these variables. Reference them in your
own styles too:

```css
.my-callout {
	background: var(--hub-sys-color-info-subtle);
	color: var(--hub-sys-color-info-emphasis);
	border: 1px solid var(--hub-sys-color-info-border-subtle);
}
```

---

## 🧱 Architecture: the two layers

The tokens follow a layered system:

| Layer          | Prefix              | What it is                                                    | Examples                                                                |
| -------------- | ------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Reference**  | `--hub-ref-*`       | Raw, context-free values                                      | `--hub-ref-color-blue-500`, `--hub-ref-space-3`, `--hub-ref-radius-md`  |
| **System**     | `--hub-sys-*`       | Meaningful assignments that components consume                | `--hub-sys-color-primary`, `--hub-sys-surface-page`, `--hub-sys-text-primary` |
| **Container**  | `--hub-container-*` | Inheritable bridge from `sys` to concrete containers/slots — a **re-base hook** | `--hub-container-bg`, `--hub-container-padding-x`, `--hub-container-gap` |

Golden rule: **components reference `sys` tokens only**. The `sys` tokens point
at the `ref` tokens. So changing a `sys` token re-themes; changing a `ref`
token adjusts the base palette.

```text
--hub-ref-color-blue-500  →  --hub-sys-color-primary  →  (consumed by components)
```

The optional `container` layer sits on top of `sys` as a **re-base hook**:
overriding one `--hub-container-*` token on a subtree re-bases every descendant
container that reads it (e.g. `ng-hub-ui-panels`), without touching `sys`. Paired
spacing uses the directional `-x` / `-y` form only (`--hub-container-padding-x/-y`,
`--hub-container-margin-x/-y`) — no shorthand.

---

## 🎨 Semantic colours

Each semantic colour (`primary` · `success` · `danger` · `warning` · `info`)
exposes a **uniform family** of five tokens:

| Token                               | Typical use                                    |
| ----------------------------------- | ---------------------------------------------- |
| `--hub-sys-color-<v>`               | Solid colour (accent, icon, strong border)     |
| `--hub-sys-color-<v>-subtle`        | Faint background (banners, alerts)             |
| `--hub-sys-color-<v>-border-subtle` | Faint border over the subtle background        |
| `--hub-sys-color-<v>-emphasis`      | Legible text over the subtle background        |
| `--hub-sys-color-<v>-dark`          | Dark variant of the colour                     |

Usage example (a callout that matches the rest of the family):

```css
.my-callout {
	background: var(--hub-sys-color-info-subtle);
	color: var(--hub-sys-color-info-emphasis);
	border: 1px solid var(--hub-sys-color-info-border-subtle);
}
```

---

## 🌗 Themes

Activate a theme with the `data-theme` attribute on `<html>` (or on any
container to theme a region):

```html
<html data-theme="dark">
  <!-- light (default) · base · bootstrap · dark · sunset · forest · mono · terminal -->
</html>
```

Because each theme **redefines the same tokens** with its own values,
everything that reads `--hub-sys-*` re-colours automatically, including your
own CSS.

---

## 🛠️ How to customise it

There are three mechanisms, from simplest to most advanced.

### 1. Override a token (CSS) — the main path

Because every value is a CSS custom property, re-theming is a one-liner — and
it **cascades to the whole family**:

```css
:root {
	--hub-sys-color-primary: #7c3aed;
	--hub-sys-color-primary-subtle: #ede9fe;
	--hub-sys-color-primary-emphasis: #5b21b6;
}
```

You can do it globally (`:root`), per theme (`[data-theme='dark']`) or per
region (`.my-section`).

### 2. Add your own accent

Define a `--hub-sys-color-<name>` family and components that accept a semantic
variant pick it up **without changes**. For example, the panels alert
(`<hub-panel appearance="alert" variant="brand">`):

```css
:root {
	--hub-sys-color-brand: #9333ea;
	--hub-sys-color-brand-subtle: #f3e8ff;
	--hub-sys-color-brand-border-subtle: #d8b4fe;
	--hub-sys-color-brand-emphasis: #6b21a8;
}
```

> With just `--hub-sys-color-brand` (the base accent) it already works:
> components derive the rest with `color-mix`. Define the full family when you
> want exact tints.

### 3. Create your own theme

Group your overrides under a theme attribute and activate it whenever you want:

```css
[data-theme='corporate'] {
	--hub-sys-color-primary: #0033a0;
	--hub-sys-surface-page: #fbfcff;
	--hub-sys-text-primary: #0a1f44;
	/* …the rest of the tokens that differ from the base theme */
}
```

---

## 🧩 SCSS functions (how it is generated internally)

The semantic colour families are **not written by hand**, and a theme only ever
sets the **accent** of each variant — `-subtle`, `-border-subtle` and `-emphasis`
are derived **once** in `:root` with `color-mix()` from the live accent, surface
and ink CSS variables. Adding a colour or a theme is uniform and boilerplate-free.

```scss
$hub-variants: primary, success, danger, warning, info;

// One accent per variant, per theme — just the base colour.
$hub-accents-light: (
	primary: var(--hub-ref-color-blue-500, #0d6efd),
	success: var(--hub-ref-color-green-500, #198754),
	danger:  var(--hub-ref-color-red-500, #dc3545),
	warning: var(--hub-ref-color-yellow-500, #ffc107),
	info:    var(--hub-ref-color-cyan-500, #0dcaf0)
);

// Sets ONLY --hub-sys-color-<variant> (the accent). Called in every theme block.
@mixin hub-color-accents($accents) {
	@each $name in $hub-variants {
		--hub-sys-color-#{$name}: #{map.get($accents, $name)};
	}
}

// Derives the role family from the live accent + surface + ink. Emitted ONCE in
// :root; themes only override the inputs, so the family recomputes contextually.
@mixin hub-color-derive() {
	@each $name in $hub-variants {
		--hub-sys-color-#{$name}-subtle:        color-mix(in srgb, var(--hub-sys-color-#{$name}) 12%, var(--hub-sys-surface-page, #fff));
		--hub-sys-color-#{$name}-border-subtle: color-mix(in srgb, var(--hub-sys-color-#{$name}) 35%, var(--hub-sys-surface-page, #fff));
		--hub-sys-color-#{$name}-emphasis:      color-mix(in srgb, var(--hub-sys-color-#{$name}) 80%, var(--hub-sys-color-ink, #212529));
		--hub-sys-color-#{$name}-dark:          var(--hub-sys-color-#{$name}-emphasis); // back-compat alias
	}
}

:root,
[data-theme='light'] {
	@include hub-color-accents($hub-accents-light);
	@include hub-color-derive();
}
```

> You almost never need to touch the SCSS: because the family is derived from the
> **single accent** at runtime, overriding `--hub-sys-color-<variant>` in plain CSS
> — even on a subtree — recomputes `-subtle` / `-border-subtle` / `-emphasis`
> automatically. The maps + mixins are just the internal mechanism, useful if you
> contribute to the package or compile your own palette variant.

---

## 📋 Quick reference table

| I want to…                 | How                                                          |
| -------------------------- | ----------------------------------------------------------- |
| Use the palette            | `@import '…/hub-tokens.css'` once                            |
| Change a global colour     | `:root { --hub-sys-color-primary: … }`                      |
| Change dark mode           | `[data-theme='dark'] { --hub-sys-… : … }`                   |
| Add your own accent        | define `--hub-sys-color-<x>` (+ optional family)            |
| Create a theme             | `[data-theme='<name>'] { … }` and activate it               |
| See all the tokens         | the tokens page at [hubui.dev](https://hubui.dev/design-system/) |

---

## 📊 Changelog

See [CHANGELOG.md](./CHANGELOG.md).

## 🤝 Contribution

Contributions are welcome.

1. **Fork** the repository.
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`.
3. **Commit** your changes: `git commit -m 'Add amazing feature'`.
4. **Push** to your branch: `git push origin feature/amazing-feature`.
5. **Submit** a pull request.

Repository: https://github.com/carlos-morcillo/ng-hub-ui-ds

## ☕ Support

Do you like this package? You can support the project by buying a coffee ☕:
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://buymeacoffee.com/carlosmorcillo)

## 📄 License

This project is licensed under the MIT License.

MIT © [Carlos Morcillo](https://www.carlosmorcillo.com)
</content>
</invoke>
