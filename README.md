# CSS Style guide

This is the style guide that I use to write CSS. It's inspired by other methodologies like BEM, SMACSS, OOCSS, etc but more simple. The aim of this guide is **write modular, scalable and maintainable CSS.**

## Modules

The css modules (a.k.a. components, objects, etc) are defined with classes. The name of the module **must be camelCase**. Example:

```css
/* One module */
.article {
    
}

/* Another module */
.imageCarrousel {

}
```

The module may have properties. The properties are joined to the module name with a `-` and **must be camelCase** too. Example:

```css
.article {
    /* main styles of the module */
}

.article-header {
    /* styles of the module property */
}
```

This allows to add sub-properties if it's needed:

```css
.article-header-title {
    
}
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

The use of camelCase notation allows to use a simple join character unlike BEM that needs two underscores (`.article__header__title`).

## Modifiers

A module or property may have modifiers. A modifier is used to change styles under some contexts or status. Unlike, for instance, BEM, the modifiers are other classes that you can combine with modules and properties. These classes may begin with `.is-*` and `.has-*`.

The `.is-*` modifier changes the element with a specific status. Some examples:

```css
.article.is-hidden {
    display: none;
}

.article-header.is-important {
    font-weight: bold
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

The `.has-*` modifier is used to change the element according to its content. Example:

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

The modifiers should be declared always combined with the modules/properties:

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

* Increments the priority of the selector.
* Allows to create different styles for the same modifier combined with different modules/properties.

There may be global modifiers if needed:

```css
/* This modifier is always the same */
.is-hidden {
    display: none;
}
```

## Layouts

For convention, the css styles used only for layout purposes must use the `.ly-*` namespace.
Example of the layout `.ly-simple` with two properties: `navigation` and `content`:

```css
.ly-simple {
    display: grid;
    grid-template-areas: 'navigation content';
    grid-template-columns: 400px 1fr;
}
.ly-simple-navigation {
    grid-area: navigation;
}
.ly-simple-content {
    grid-area: content;
}
```

```html
<div class="ly-simple">
    <nav class="ly-simple-navigation">...</nav>
    <main class="ly-simple-content">...</nav>
</div>
```

## CSS + JS

The css classes can be used by javascript to select elements. To prevent conflict between css and js, **the classes used by javascript should not be used by css, and viceversa**. Because that, there's the `.js-*` namespace:

```html
<article class="article js-popup">
    <h1>Hello world</h1>
</article>

<div class="js-popup">
    Other popup
</div>
```

```js
$('.js-popup').popup();
```

It's recomended to separate styling classes and functionality classes. This doesn't mean javascript can not use styling classes, but only for styling purposes:

```js
$('.article').addClass('is-hidden');
```

## Imports

In order to avoid problems with the selectors priority, the main css file should import the nested css files in the following order:

* global styles (reset, variables, normalize, etc)
* modules
* global modifiers
* hacks

Example:

```css
/* Global styles */
@import "normalize.css";
@import "reset.css";

/* Modules */
@import "modules/article.css";
@import "modules/comments.css";

/* Global modifiers and hacks */
@import "modifiers.css";
@import "ie.css";
```

# Cases

* [hacks](cases/hacks)
* [locks](cases/locks)
* [quantity](cases/quantity)
* [notch](cases/notch)
* [typography](cases/typography)
* [select (filamentgroup)](https://github.com/filamentgroup/select-css)
