# Flexible typography with CSS locks

This style guide relies on [media queries](http://caniuse.com/#feat=css-mediaqueries) and [calc](http://caniuse.com/#search=calc) to build a responsive grid system, so it requires IE>=10.

Based in [Flexible typography with CSS locks](http://blog.typekit.com/2016/08/17/flexible-typography-with-css-locks/) article.

```css
/*
 * min-value: 1.3em
 * max-value: 3.5em
 * min-width: 21em
 * max-width: 40em
 */
h1.title {
    /* calc({min-value}em + ({max-value} - {min-value}) * ((100vw - {min-width}em)/({max-width} - {min-width}))) */
    font-size: calc(1.3em + (3.5 - 1.3) * ((100vw - 21em)/(40 - 21)));
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