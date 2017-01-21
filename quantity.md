# Quantity queries

This guide allows to create quantity queries using only css.

Based in [Use Quantity Queries to Make Your CSS Quantity-Aware](http://www.hongkiat.com/blog/quantity-queries-css-quantity-aware/) article.

```css
/* At least 5 */
ul li:nth-last-child(n+5),
ul li:nth-last-child(n+5) ~ li {
    border: 2px dashed;
}

/* At most 5 */
ul li:nth-last-child(-n+5):first-child,
ul li:nth-last-child(-n+5):first-child ~ li {
    background-color: yellow;
}

/* Between 5 and 8 */
ul li:nth-last-child(n+5):nth-last-child(-n+8):first-child,
ul li:nth-last-child(n+5):nth-last-child(-n+8):first-child ~ li {
    font-weight: bold;
}

/* Exactly 5 */
ul li:nth-last-child(5):first-child,
ul li:nth-last-child(5):first-child ~ li {
    text-decoration: underline;
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/tests/css-selectors.html)