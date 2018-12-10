# Flexible typography with CSS locks

This style guide relies on [media queries](http://caniuse.com/#feat=css-mediaqueries) and [calc](http://caniuse.com/#search=calc) to build a responsive grid system, so it requires IE>=10.

Based in [Flexible typography with CSS locks](http://blog.typekit.com/2016/08/17/flexible-typography-with-css-locks/) article.

```css
/*
 * minValue: 1.3em
 * maxValue: 3.5em
 * minWidth: 21em
 * maxWidth: 40em
 */
h1.title {
    /* calc({minValue}em + ({maxValue} - {minValue}) * ((100vw - {minWidth}em) / ({maxWidth} - {minWidth}))) */
    font-size: calc(1.3em + (3.5 - 1.3) * ((100vw - 21em) / (40 - 21)));
}

@media (max-width: 21em) {
    h1 {
        font-size: 1.3em;
    }
}

@media (min-width: 40em) {
    h1 {
        font-size: 3.5;
    }
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/locks/)