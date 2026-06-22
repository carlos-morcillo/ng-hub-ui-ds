# ng-hub-ui-ds

**Español** | [English](./README.md)

La **base de design tokens** compartida de la familia
[ng-hub-ui](https://hubui.dev/). Publica las variables CSS canónicas
`--hub-ref-*` (primitivas) y `--hub-sys-*` (semánticas) — rampas de color,
espaciado, radios, tipografía, superficies, colores semánticos, sombras, focus
ring y más — con claro/oscuro y **8 temas integrados**.

Impórtala **una vez** y cada librería de ng-hub-ui (panels, forms, calendar…)
lee la misma paleta. Re-tematizas en un sitio y toda la familia sigue.

> Agnóstica de framework — son solo variables CSS. Sin dependencia de Angular ni
> de JS; envía el CSS compilado o el código SCSS.

## Documentación y ejemplos en vivo

Este paquete forma parte de [Hub UI](https://hubui.dev/), una colección de
librerías de componentes Angular para aplicaciones standalone.

- Documentación: https://hubui.dev/design-system/
- Hub UI: https://hubui.dev/

## 🧩 Familia de librerías `ng-hub-ui`

Este paquete es la base de design tokens de la que lee el resto del ecosistema
**ng-hub-ui**:

- [**ng-hub-ui-accordion**](https://www.npmjs.com/package/ng-hub-ui-accordion) (obsoleta — usa ng-hub-ui-panels)
- [**ng-hub-ui-action-sheet**](https://www.npmjs.com/package/ng-hub-ui-action-sheet)
- [**ng-hub-ui-avatar**](https://www.npmjs.com/package/ng-hub-ui-avatar)
- [**ng-hub-ui-board**](https://www.npmjs.com/package/ng-hub-ui-board)
- [**ng-hub-ui-breadcrumbs**](https://www.npmjs.com/package/ng-hub-ui-breadcrumbs)
- [**ng-hub-ui-calendar**](https://www.npmjs.com/package/ng-hub-ui-calendar)
- [**ng-hub-ui-dropdown**](https://www.npmjs.com/package/ng-hub-ui-dropdown)
- [**ng-hub-ui-ds**](https://www.npmjs.com/package/ng-hub-ui-ds) ← Estás aquí
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

## 📋 Índice

1. [🧩 ¿Qué es y para qué sirve?](#-qué-es-y-para-qué-sirve)
2. [📦 Instalación](#-instalación)
3. [🚀 Importación](#-importación)
4. [🧱 Arquitectura: las dos capas](#-arquitectura-las-dos-capas)
5. [🎨 Los colores semánticos](#-los-colores-semánticos)
6. [🌗 Temas](#-temas)
7. [🛠️ Cómo modificarlo](#️-cómo-modificarlo)
8. [🧩 Funciones SCSS (cómo se genera por dentro)](#-funciones-scss-cómo-se-genera-por-dentro)
9. [📋 Tabla de referencia rápida](#-tabla-de-referencia-rápida)
10. [📊 Changelog](#-changelog)
11. [🤝 Contribución](#-contribución)
12. [☕ Apoyo](#-apoyo)
13. [📄 Licencia](#-licencia)

---

## 🧩 ¿Qué es y para qué sirve?

Cada librería de ng-hub-ui se tematiza con variables CSS `--hub-*`, pero **no
define** los colores: solo los **consume** (con _fallbacks_ sensatos). Este
paquete es **la fuente de verdad única** de esas variables.

Sin él, cada librería usaría sus valores de respaldo de forma aislada. Con él:

- **Una sola paleta** alimenta panels, forms, calendar, board… a la vez.
- **Re-tematizas una vez** (un token) y el cambio se propaga a toda la familia.
- **Modo oscuro y 8 temas** listos, conmutables con un atributo.
- Lo usas también en **tu propio CSS** (`var(--hub-sys-color-info-subtle)`), así
  tu UI casa con los componentes.

---

## 📦 Instalación

```bash
npm install ng-hub-ui-ds
```

No tiene dependencias. Es CSS/SCSS puro.

---

## 🚀 Importación

Impórtalo **una sola vez**, en la raíz de tu aplicación. Elige una vía:

### CSS drop-in (cualquier app, sin Sass)

```css
@import 'ng-hub-ui-ds/styles/tokens/hub-tokens.css';
```

o en `angular.json`:

```json
"styles": [
  "node_modules/ng-hub-ui-ds/styles/tokens/hub-tokens.css",
  "src/styles.scss"
]
```

### Código SCSS (si usas Sass)

Emite exactamente las mismas reglas `:root`, y te deja referenciar la fuente:

```scss
@use 'ng-hub-ui-ds/styles/tokens/hub-tokens';
```

Cada componente de ng-hub-ui ya lee estas variables. Refiérelas también en tus
propios estilos:

```css
.mi-aviso {
	background: var(--hub-sys-color-info-subtle);
	color: var(--hub-sys-color-info-emphasis);
	border: 1px solid var(--hub-sys-color-info-border-subtle);
}
```

---

## 🧱 Arquitectura: las dos capas

Los tokens siguen un sistema por capas:

| Capa            | Prefijo             | Qué es                                                       | Ejemplos                                                                |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **Referencia**  | `--hub-ref-*`       | Valores crudos, sin contexto                                 | `--hub-ref-color-blue-500`, `--hub-ref-space-3`, `--hub-ref-radius-md`  |
| **Sistema**     | `--hub-sys-*`       | Asignaciones con significado que consumen los componentes    | `--hub-sys-color-primary`, `--hub-sys-surface-page`, `--hub-sys-text-primary` |
| **Container**   | `--hub-container-*` | Puente heredable de `sys` a contenedores/slots concretos — un **re-base hook** | `--hub-container-bg`, `--hub-container-padding-x`, `--hub-container-gap` |

Regla de oro: **los componentes referencian solo tokens `sys`**. Los `sys`
apuntan a los `ref`. Así, cambiar un `sys` re-tematiza; cambiar un `ref` ajusta
la paleta base.

```text
--hub-ref-color-blue-500  →  --hub-sys-color-primary  →  (lo usan los componentes)
```

La capa opcional `container` se apoya sobre `sys` como **re-base hook**:
sobrescribir un token `--hub-container-*` en un subárbol re-basa cada contenedor
descendiente que lo lee (p. ej. `ng-hub-ui-panels`), sin tocar `sys`. El espaciado
emparejado usa solo la forma direccional `-x` / `-y` (`--hub-container-padding-x/-y`,
`--hub-container-margin-x/-y`) — sin atajo.

---

## 🎨 Los colores semánticos

Cada color semántico (`primary` · `success` · `danger` · `warning` · `info`)
expone una **familia uniforme** de cinco tokens:

| Token                               | Uso típico                                     |
| ----------------------------------- | ---------------------------------------------- |
| `--hub-sys-color-<v>`               | Color sólido (acento, icono, borde fuerte)     |
| `--hub-sys-color-<v>-subtle`        | Fondo tenue (banners, alertas)                 |
| `--hub-sys-color-<v>-border-subtle` | Borde tenue sobre el fondo subtle              |
| `--hub-sys-color-<v>-emphasis`      | Texto legible sobre el fondo subtle            |
| `--hub-sys-color-<v>-dark`          | Variante oscura del color                      |

Ejemplo de uso (un aviso a juego con el resto de la familia):

```css
.mi-aviso {
	background: var(--hub-sys-color-info-subtle);
	color: var(--hub-sys-color-info-emphasis);
	border: 1px solid var(--hub-sys-color-info-border-subtle);
}
```

---

## 🌗 Temas

Activa un tema con el atributo `data-theme` en `<html>` (o en cualquier
contenedor para tematizar una zona):

```html
<html data-theme="dark">
  <!-- light (por defecto) · base · bootstrap · dark · sunset · forest · mono · terminal -->
</html>
```

Como cada tema **redefine los mismos tokens** con sus valores, todo lo que lee
`--hub-sys-*` se re-colorea automáticamente, incluido tu propio CSS.

---

## 🛠️ Cómo modificarlo

Hay tres mecanismos, de más simple a más avanzado.

### 1. Sobrescribir un token (CSS) — el camino principal

Como cada valor es una variable CSS, re-tematizar es una línea, y **cascada a
toda la familia**:

```css
:root {
	--hub-sys-color-primary: #7c3aed;
	--hub-sys-color-primary-subtle: #ede9fe;
	--hub-sys-color-primary-emphasis: #5b21b6;
}
```

Puedes hacerlo global (`:root`), por tema (`[data-theme='dark']`) o por zona
(`.mi-seccion`).

### 2. Añadir tu propio acento

Define una familia `--hub-sys-color-<nombre>` y los componentes que aceptan una
variante semántica la recogen **sin cambios**. Por ejemplo, el alert de panels
(`<hub-panel appearance="alert" variant="brand">`):

```css
:root {
	--hub-sys-color-brand: #9333ea;
	--hub-sys-color-brand-subtle: #f3e8ff;
	--hub-sys-color-brand-border-subtle: #d8b4fe;
	--hub-sys-color-brand-emphasis: #6b21a8;
}
```

> Con solo `--hub-sys-color-brand` (el acento base) ya funciona: los componentes
> derivan el resto con `color-mix`. Define la familia completa cuando quieras
> tintes exactos.

### 3. Crear un tema propio

Reúne tus overrides bajo un atributo de tema y actívalo cuando quieras:

```css
[data-theme='corporate'] {
	--hub-sys-color-primary: #0033a0;
	--hub-sys-surface-page: #fbfcff;
	--hub-sys-text-primary: #0a1f44;
	/* …el resto de tokens que difieran del tema base */
}
```

---

## 🧩 Funciones SCSS (cómo se genera por dentro)

Las familias de color semántico **no se escriben a mano**, y un tema solo fija el
**acento** de cada variante — `-subtle`, `-border-subtle` y `-emphasis` se derivan
**una sola vez** en `:root` con `color-mix()` a partir del acento, la superficie y
el _ink_ vivos. Así, añadir un color o un tema es uniforme y sin _boilerplate_.

```scss
$hub-variants: primary, success, danger, warning, info;

// Un acento por variante, por tema — solo el color base.
$hub-accents-light: (
	primary: var(--hub-ref-color-blue-500, #0d6efd),
	success: var(--hub-ref-color-green-500, #198754),
	danger:  var(--hub-ref-color-red-500, #dc3545),
	warning: var(--hub-ref-color-yellow-500, #ffc107),
	info:    var(--hub-ref-color-cyan-500, #0dcaf0)
);

// Fija SOLO --hub-sys-color-<variante> (el acento). Se llama en cada tema.
@mixin hub-color-accents($accents) {
	@each $name in $hub-variants {
		--hub-sys-color-#{$name}: #{map.get($accents, $name)};
	}
}

// Deriva la familia de roles del acento + superficie + ink vivos. Se emite UNA
// vez en :root; los temas solo cambian las entradas y la familia se recalcula.
@mixin hub-color-derive() {
	@each $name in $hub-variants {
		--hub-sys-color-#{$name}-subtle:        color-mix(in srgb, var(--hub-sys-color-#{$name}) 12%, var(--hub-sys-surface-page, #fff));
		--hub-sys-color-#{$name}-border-subtle: color-mix(in srgb, var(--hub-sys-color-#{$name}) 35%, var(--hub-sys-surface-page, #fff));
		--hub-sys-color-#{$name}-emphasis:      color-mix(in srgb, var(--hub-sys-color-#{$name}) 80%, var(--hub-sys-color-ink, #212529));
		--hub-sys-color-#{$name}-dark:          var(--hub-sys-color-#{$name}-emphasis); // alias retrocompatible
	}
}

:root,
[data-theme='light'] {
	@include hub-color-accents($hub-accents-light);
	@include hub-color-derive();
}
```

> Casi nunca necesitas tocar el SCSS: como la familia se deriva del **acento
> único** en tiempo de ejecución, sobrescribir `--hub-sys-color-<variante>` en CSS
> plano — incluso en un subárbol — recalcula `-subtle` / `-border-subtle` /
> `-emphasis` automáticamente. Los mapas + mixins son solo la mecánica interna,
> útil si contribuyes al paquete o compilas tu propia variante de la paleta.

---

## 📋 Tabla de referencia rápida

| Quiero…                    | Cómo                                                        |
| -------------------------- | ----------------------------------------------------------- |
| Usar la paleta             | `@import '…/hub-tokens.css'` una vez                        |
| Cambiar un color global    | `:root { --hub-sys-color-primary: … }`                      |
| Cambiar el modo oscuro     | `[data-theme='dark'] { --hub-sys-… : … }`                   |
| Añadir un acento propio    | define `--hub-sys-color-<x>` (+ familia opcional)           |
| Crear un tema              | `[data-theme='<nombre>'] { … }` y actívalo                  |
| Ver todos los tokens       | la página de tokens en [hubui.dev](https://hubui.dev/design-system/) |

---

## 📊 Changelog

Consulta [CHANGELOG.md](./CHANGELOG.md).

## 🤝 Contribución

Las contribuciones son bienvenidas.

1. **Haz un fork** del repositorio.
2. **Crea** una rama de característica: `git checkout -b feature/amazing-feature`.
3. **Haz commit** de tus cambios: `git commit -m 'Add amazing feature'`.
4. **Haz push** a tu rama: `git push origin feature/amazing-feature`.
5. **Abre** un pull request.

Repositorio: https://github.com/carlos-morcillo/ng-hub-ui-ds

## ☕ Apoyo

¿Te gusta este paquete? Puedes apoyar el proyecto invitándome a un café ☕:
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://buymeacoffee.com/carlosmorcillo)

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT.

MIT © [Carlos Morcillo](https://www.carlosmorcillo.com)
</content>
