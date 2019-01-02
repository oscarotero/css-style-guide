# Select

Crossbrowser css-only technique to style a selector.

Based in [Styling a Select Like It’s 2019](https://www.filamentgroup.com/lab/select-css.html)

```html
<select class="select-css">
    <option>This is a native select element</option>
    <option>Apples</option>
    <option>Bananas</option>
    <option>Grapes</option>
    <option>Oranges</option>
</select>
```

```css
.select-css {
    font-size: 100%;
    font-family: inherit;
    color: #444;
    line-height: 1.3;
    padding: .6em 2em .5em .8em;
    max-width: 100%; 
    box-sizing: border-box;
    margin: 0;
    border: 1px solid #aaa;
    box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
    border-radius: .5em;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    background-color: #fff;
    background-image: url('data:image/svg+xml;charset=UTF-8,<svg width="16px" height="16px" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg"><polygon fill="%23007CB2" points="0 3 0 4 7.5 13 8.5 13 16 4 16 3"></polygon></svg>'),
    linear-gradient(to bottom, #ffffff 0%,#efefef 100%);
    background-repeat: no-repeat, repeat;
    background-position: right .7em top 50%, 0 0;
    background-size: .65em auto, 100%;
}
.select-css::-ms-expand {
    display: none;
}
.select-css:hover {
    border-color: #888;
}
.select-css:focus {
    border-color: #aaa;
    box-shadow: 0 0 1px 3px rgba(59, 153, 252, .7);
    box-shadow: 0 0 0 3px -moz-mac-focusring;
    color: #222; 
    outline: none;
}
.select-css option {
    font-weight:normal;
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/select/)