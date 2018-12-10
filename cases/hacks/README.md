# Hacks

Sometimes you need to create hacks for specific browsers (well, mainly for _internet explorer_). These hacks **must be in a different file** to not interfere in the main css of the page. This allows to remove the hacks in a future without edit the other css or html code.

```html
<link rel="stylesheet" href="all-browsers.css">
<link rel="stylesheet" href="ie-10-11.css" media="(-ms-high-contrast: none), (-ms-high-contrast: active)">
<!--[if IE]>
<link rel="stylesheet" type="text/css" href="ie-9-and-older.css" />
<![endif]-->
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/hacks/)