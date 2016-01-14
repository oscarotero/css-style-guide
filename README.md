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

This allows to add more properties if it's needed:

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

The use of camelCase notation allows to use a simple join character unlike BEM that needs two underscores and hiphens (for example: `.article__header__title`).

## Modifiers

A module or property can have modifiers. A modifier serves to change styles under some circunstance. Unlike, for instance, BEM, the modifiers are other classes that you can combine with modules and properties. These classes must begin with `.is-*` and `.has-*`.

The `.is-*` modifier tell a specific aspect of the element. Some examples:

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

The `.has-*` modifier serves to change the element if it has a specific content. Example:

```css
.article {
    width: 500px;
}

.article.has-image {
    width: 700px;
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

## CSS + JS

The css classes can be used by javascript to select elements. To prevent conflict between css and js, **the classes used by javascript may not be used by css, and viceversa**. Because that, there's the `.js-*` namespace:

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

This allows to separate the classes for styling and the classes for funcionality. Of course, javascript can use the rest of the classes but only for styling purposes:

```js
$('.article').addClass('is-hidden');
```
