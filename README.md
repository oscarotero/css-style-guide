# CSS Style guide

This is the style guide that I use to write CSS. It's inspired by other
methodologies like BEM, SMACSS, OOCSS, etc but more simple. The aim of this
guide is **write modular, scalable and maintainable CSS.**

## Components

CSS components (a.k.a. modules, objects, etc) are defined with classes.

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

> [!note]
>
> The use of camelCase notation allows to use a simple join character unlike BEM
> that needs two underscores (`.article__header__title`).

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

Don't use use sub-properties if you really don't need to. The previous example
is clearer as following:

```html
<article class="article">
  <header class="article-header">
    <h1 class="article-title">
      The title
    </h1>
  </header>
</article>
```

## Modifiers

Components and properties may have modifiers. Modifiers are used to change
styles under some contexts or status. Unlike, for instance, BEM, modifiers are
independent classes that you can combine with components and properties. These
classes should start with `.is-*` and `.has-*`.

The `.is-*` modifier changes the element with a specific status. Some examples:

```css
.article.is-hidden {
  display: none;
}

.article-header.is-important {
  font-weight: bold;
}

.article p.is-highlighted {
  background: yellow;
}
```

```html
<article class="article is-hidden">
  invisible content
</article>
```

The `.has-*` modifier is used to change the element according to its content.
Example:

```css
.article {
  width: 500px;
}

.article.has-video {
  width: 900px;
}
```

```html
<article class="article has-video">
  <video class="article-video" src="video.ogv"></video>
</article>
```

The modifiers must be declared always combined with the components/properties:

```css
/* wrong */
.has-video {
  width: 900px;
}

/* right */
.article.has-video {
  width: 900px;
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

Some `has-` modifiers can be replaced with the
[`:has()` selector](https://developer.mozilla.org/en-US/docs/Web/CSS/:has)
supported by all modern browsers:

```css
/* Old way */
.article.has-video {
  width: 900px;
}

/* Modern way */
.article:has(.article-video) {
  width: 900px;
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

## CSS + JS

The CSS classes can be used by JavaScript to select elements. To prevent
conflict between CSS and JS, **the classes used by JavaScript should not be used
by CSS, and viceversa**. Because that, there's the `.js-*` namespace:

```html
<article class="article js-popup">
  <h1>Hello world</h1>
</article>

<div class="js-popup">
  Other popup
</div>
```

```js
document.querySelector(".js-popup")?.style.display = "block";
```

It's recomended to separate styling classes and functionality classes. This
doesn't mean JavaScript can not use styling classes, but only for styling
purposes:

```js
document.querySelector(".article")?.classList.add("is-hidden");
```

## !important

The `!important` flag **is not recommended,** but may be needed in few edge
cases. Every time we use it, we should include a comment explaining the reason,
so it can be removed in the future.

```css
.popup-title {
  font-weight: bold
    !important; /* This overrides the inline style applied by the plugin popup */
}
```

## Imports

In order to avoid problems with the selectors priority, the main CSS file should
import the nested CSS files in the following order:

- global styles (reset, variables, normalize, etc)
- components
- global modifiers
- hacks

Example:

```css
/* Global styles */
@import "normalize.css";
@import "reset.css";

/* Components */
@import "components/article.css";
@import "components/comments.css";

/* Global modifiers and hacks */
@import "modifiers.css";
@import "ie.css";
```

## Layers

Additionally, we can use CSS layers for better organization and priority:

```css
@layer global {
  /* Normalize, reset */
}

@layer components {
  /* Components */
}

@layer utils {
  /* Utils, global modifiers, hacks, etc */
}
```

---

Other notes:

- [100vh](cases/100vh)
- [quantity](cases/quantity)
- [typography](cases/typography)
- [select (filamentgroup)](https://github.com/filamentgroup/select-css)
