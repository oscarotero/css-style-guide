# 100vh in iOS

Based in
[CSS fix for 100vh in mobile WebKit](https://allthingssmitty.com/2020/05/11/css-fix-for-100vh-in-mobile-webkit/)
and the [PostCSS plugin](https://github.com/postcss/postcss-100vh-fix)

```css
body {
  height: 100vh;
}

/* Apply the hack only in Safari */
@supports (-webkit-touch-callout: none) {
  body {
    height: -webkit-fill-available;
  }
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/100vh/)
