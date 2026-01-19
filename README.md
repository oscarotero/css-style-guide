# CSS Style guide

This is the style guide that I use to write CSS. It's inspired by other
methodologies like BEM, SMACSS, OOCSS, etc but more simple. The aim of this
guide is **write modular, scalable and maintainable CSS.**

## Components

CSS components (a.k.a. modules) are defined with classes.

```css
/* The 'article' component */
.article {}
```

Don't use `-` character for component names. If you want to differentiate words,
use _camelCase_ or underscores:

```css
/* The 'image carousel' component */
.imageCarousel {}

/* Alternative naming if you don't like camelCase */
.image_carousel {}
```

Components may have properties. The properties are joined to the component name
with a `-`. Example:

```css
.article {
  /* styles of the component */
}

.article-header {
  /* styles of the component's property */
}
```

Like component names, properties shouldn't have `-` characters:

```css
.article-mainImage {
  /* styles of the mainImage property of article component */
}
```

This allows to add sub-properties if it's needed:

```css
.article-header-title {}
```

```html
<article class="article">
  <header class="article-header">
    <h1 class="article-header-title">
      The title
    </h1>
  </header>
</article>
```

But don't use use sub-properties if you really don't need to. The previous
example is clearer as following:

```html
<article class="article">
  <header class="article-header">
    <h1 class="article-title">
      The title
    </h1>
  </header>
</article>
```

> [!note]
>
> The `.article-header-title` example only makes sense if the component has
> different titles in different positions. For example `.article-section-title`
> or `.article-footer.title`. But if it has only one title, just use
> `.article-title`.

## Modifiers

Components and properties may have modifiers. Modifiers are used to change
styles under some contexts or status. Unlike, for instance, BEM, modifiers are
independent classes that you can combine with components and properties. These
classes must start with `.is-*`.

The `.is-*` modifier changes the element with a specific status. Some examples:

```css
.article.is-hidden {
  display: none;
}

.article.is-important {
  background: yellow;
}
```

```html
<article class="article is-important">
  ...
</article>
```

The modifiers must be declared always combined with the components/properties:

```css
/* wrong */
.is-important {
  background: yellow;
}

/* right */
.article.is-important {
  background: yellow;
}
```

This has two advantages:

- Increments the priority of the selector.
- Allows to create different styles for the same modifier combined with
  different components/properties.

There may be global modifiers if needed:

```css
/* This is a global modifier, it can be combined with any component */
.is-hidden {
  display: none;
}
```

Don't create a modifier if you can use
[`:has()`](https://developer.mozilla.org/en-US/docs/Web/CSS/:has) or a similar
CSS selector:

```css
.article {
  width: 500px;
}

/* not cool */
.article.is-video {
  width: 900px;
}

/* much better! */
.article:has(.article-video) {
  width: 900px;
}
```

```html
<article class="article">
  <video class="article-video" src="video.ogv"></video>
</article>
```

## Settings

Components have two parts: settings and implementation. The settings is a list
of CSS variables at the top:

```css
.button {
  /* Settings */
  --size: 1rem;
  --color: white;
  --color-hover: var(--color);
  --color-focus: var(--color-hover);
  --background: blue;
  --background-hover: darkblue;
  --background-focus: black;

  /* Implementation */
  font-size: var(--size);
  color: var(--color);
  background-color: var(--background);

  &:hover {
    color: var(--color-hover);
    background-color: var(--background-hover);
  }

  &:focus {
    color: var(--color-focus);
    background-color: var(--background-focus);
  }
}
```

This allows to create new variations of the same component easily using
modifiers:

```css
.button.is-secondary {
  --color: blue;
  --color-hover: var(--color);
  --color-focus: var(--color-hover);
  --background: white;
  --background-hover: #ccc;
  --background-focus: #999;
}

.button.is-big {
  --size: 2rem;
}
```

Use variables for all values that you want to customize. And place all possible
states in the same place:

```css
/* Not cool. It makes difficult to modify or create variations */
.details {
  --color: gray;

  &:open {
    --color: black;
  }

  color: var(--color);
}

/* Much better! */
.details {
  --color: gray;
  --color-open: black;

  color: var(--color);
  &:open {
    color: var(--color-open);
  }
}
```

## Layouts

By convention, CSS styles used only for layout purposes must use the `.ly-*`
namespace. Example of the `2columns` layout with two properties: `navigation`
and `content`:

```css
.ly-2columns {
  display: grid;
  grid-template-areas: "navigation content";
  grid-template-columns: 400px 1fr;
}
.ly-2columns-navigation {
  grid-area: navigation;
}
.ly-2columns-content {
  grid-area: content;
}
```

```html
<div class="ly-2columns">
  <nav class="ly-2columns-navigation">...</nav>
  <main class="ly-2columns-content">...</main>
</div>
```

Like components, layouts can be customizable:

```css
.ly-2columns {
  --navigation-width: 400px;

  display: grid;
  grid-template-areas: "navigation content";
  grid-template-columns: var(--navigation-width) 1fr;
}
```

## !important

The `!important` flag **is not recommended,** but may be needed in few edge
cases. Every time it's used, include a comment explaining the reason, so it can
be removed in the future.

```css
.popup-title {
  font-weight: bold
    !important; /* This overrides the inline style applied by JavaScript */
}
```

## Imports

In order to avoid problems with the selectors priority, the main CSS file should
import the nested CSS files in the following order:

- global styles (reset, variables, normalize, etc)
- components
- global modifiers/utils

You can use `@layer` for better organization:

Example:

```css
/* Global styles */
@import "normalize.css" layer(base);
@import "reset.css" layer(base);

/* Components */
@import "components/article.css" layer(components);
@import "components/comments.css" layer(components);

/* Global modifiers */
@import "modifiers.css" layer(utils);
```

---

Other notes:

- [100vh](cases/100vh)
- [quantity](cases/quantity)
- [typography](cases/typography)
- [select (filamentgroup)](https://github.com/filamentgroup/select-css)
