# Notch

The "notch" is the shape that Apple added to the iPhoneX creating a white bar on de edges. This guide allows to remove that effect and extend the webpage to the entire screen:

Based in [Removing the White Bars in Safari on iPhone X](http://stephenradford.me/removing-the-white-bars-in-safari-on-iphone-x/)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover"> 
```

```css
body {
    padding: env(safe-area-inset-top)
             env(safe-area-inset-right) 
             env(safe-area-inset-bottom) 
             env(safe-area-inset-left);
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/notch/)