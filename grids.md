# The best way to create css grids in modern browsers

## The compatible version

This style guide relies on [flexbox](http://caniuse.com/#feat=flexbox) and [calc](http://caniuse.com/#search=calc) to build a responsive grid system, so it requires IE>=10.

```css
ul.grid {
    list-style: none;
    margin: 0;
    padding: 0;
}
ul.grid > li {
    margin-bottom: 20px;
}

/* Start columns */
@media (min-width: 401px) {
    ul.grid {
        display: flex;
        flex-wrap: wrap;
    }
    ul.grid > li {
        margin-right: 20px;
    }
    ul.grid > li:last-child {
        margin-right: 0;
    }
}

/* 2 columns grid */
@media (min-width: 401px) AND (max-width: 600px) {
    ul.grid > li {
        width: calc((100% / 2) - (20px / 2));
    }
    ul.grid > li:nth-child(2n) {
        margin-right: 0;
    }
}

/* 3 columns grid */
@media (min-width: 601px) AND (max-width: 800px) {
    ul.grid > li {
        width: calc((100% / 3) - ((20px * 2) / 3));
    }
    ul.grid > li:nth-child(3n) {
        margin-right: 0;
    }
}

/* 4 columns grid */
@media (min-width: 801px) AND (max-width: 1000px) {
    ul.grid > li {
        width: calc((100% / 4) - ((20px * 3) / 4));
    }
    ul.grid > li:nth-child(4n) {
        margin-right: 0;
    }
}

/* 5 columns grid */
@media (min-width: 1001px) AND (max-width: 1200px) {
    ul.grid > li {
        width: calc((100% / 5) - ((20px * 4) / 5));
    }
    ul.grid > li:nth-child(5n) {
        margin-right: 0;
    }
}

/* 6 columns grid */
@media (min-width: 1201px) {
    ul.grid > li {
        width: calc((100% / 6) - ((20px * 5) / 6));
    }
    ul.grid > li:nth-child(6n) {
        margin-right: 0;
    }
}
```

## The future version

This version uses also [css variables](http://caniuse.com/#feat=css-variables), so it's not supported by IE and Edge:

```css
ul.grid {
    --cols: 2; /* Number of columns */
    --gap: 20px; /* Distance of separation between columns */
    list-style: none;
    margin: 0;
    padding: 0;
}
ul.grid > li {
    margin-bottom: var(--gap);
}

/* Start columns */
@media (min-width: 401px) {
    ul.grid {
        display: flex;
        flex-wrap: wrap;
    }
    ul.grid > li {
        margin-right: var(--gap);
        width: calc((100% / var(--cols)) - ((var(--gap) * (var(--cols) - 1)) / var(--cols)));
    }
    ul.grid > li:last-child {
        margin-right: 0;
    }
}

/* 2 columns grid */
@media (min-width: 401px) AND (max-width: 600px) {
    ul.grid {
        --cols: 2;
    }
    ul.grid > li:nth-child(2n) {
        margin-right: 0;
    }
}

/* 3 columns grid */
@media (min-width: 601px) AND (max-width: 800px) {
    ul.grid {
        --cols: 3;
    }
    ul.grid > li:nth-child(3n) {
        margin-right: 0;
    }
}

/* 4 columns grid */
@media (min-width: 801px) AND (max-width: 1000px) {
    ul.grid {
        --cols: 4;
    }
    ul.grid > li:nth-child(4n) {
        margin-right: 0;
    }
}

/* 5 columns grid */
@media (min-width: 1001px) AND (max-width: 1200px) {
    ul.grid {
        --cols: 5;
    }
    ul.grid > li:nth-child(5n) {
        margin-right: 0;
    }
}

/* 6 columns grid */
@media (min-width: 1201px) {
    ul.grid {
        --cols: 6;
    }
    ul.grid > li:nth-child(6n) {
        margin-right: 0;
    }
}
```