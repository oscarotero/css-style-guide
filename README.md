# CSS Style guide

This is the style guide that I use to write CSS. It's inspired in other methodologies like BEM, SMACSS, OOCSS, etc but tries to be a bit more friendly and easy.

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

The module can have properties. The properties are joined to the module with a `-` and **must be camelCase** too. Example:

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

A module or property can have modifiers. A modifier serves to change styles under some circunstance or status. Unlike, for instance, BEM, the modifiers are other classes that you can combine with modules and properties. These classes may begin with `.is-*` and `.has-*`.

The `.is-*` modifier changes the element with a specific status. Some examples:

```css
.article.is-hidden {
    display: block;
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

The `.has-*` modifier serves to change the element according with its contain. Example:

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

Of course, there may be global modifiers if they are needed:

```css
/* This modifier is always the same */
.is-hidden {
    display: none;
}
```

## CSS + JS

The css classes can be used by javascript to select elements. To prevent conflict between css and js, **the classes used by javascript might not be used by css, and viceversa**. Because that, there's the `.js-*` namespace:

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

It's recomended to separate styling classes and functionality classes. This does not mean javascript cannot use styling classes, but only for styling purposes:

```js
$('.article').addClass('is-hidden');
```

## Import

In order to avoid problems with the selectors priority, the main css file should import the nested css files in the following order:

* global styles
* modules
* global modifiers

Example:

```css
/* Global styles */
@import "normalice.css";
@import "reset.css";

/* Modules */
@import "modules/article.css";
@import "modules/comments.css";

/* Global modifiers */
@import "modifiers.css";
```