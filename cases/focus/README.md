# Focus

How to handle focus styles using `:focus` and `:focus-visible`.

Based in [The :focus-visible Trick](https://css-tricks.com/the-focus-visible-trick/) article.

```css
/* Focusing the button with a keyboard */
button:focus-visible {
  outline: 4px dashed black;
}
/* Firefox supports :-moz-focusring */
button:-moz-focusring {
  outline: 4px dashed black;
}

/* Focusing the button with a mouse/touch */
button:focus:not(:focus-visible) {
  outline: none;
  box-shadow: 1px 1px 5px rgba(1, 1, 0, .7);
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/cuantity/)