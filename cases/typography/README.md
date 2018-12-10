# Typography

Guide of advanced css features for typography.

## Caps

More info: [Font Variant Caps](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-caps)

To use real small caps:

```css
.small-caps {
  font-variant-caps: small-caps;
}
```

## Numbers

More info: [Font Variant Numeric](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric)

### Lining / old style

Lining figures are uppercase numbers. Old style figures are numbers to use inside a body text.

```css
.lining {
  font-variant-numeric: lining-nums;
}

.old-style {
  font-variant-numeric: oldstyle-nums;
}
```

### Proportional / tabular

Proportional means numbers with different widths. Tabular numbers align horizontally no matter the number.

```css
.proportional {
  font-variant-numeric: proportional-nums;
}

.tabular {
  font-variant-numeric: tabular-nums;
}
```

## Ligatures

More info: [Font Variant Ligatures](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-ligatures)

The common ligatures are enabled by default in most browsers. You can enable also other different ligatures:

### Discretional / contextual

Discretional ligatures are more ornamental. Contextual are more common in script typefaces, and are used to make the text look "natural"

```css
.discretional {
  font-variant-ligatures: discretionary-ligatures;
}

.contextual {
  font-variant-ligatures: contextual;
}
```

## Other features

System fonts

```css
.system {
  font-family: -apple-system, system-ui, sans-serif;
}
```

Text decoration skip

```css
.skip {
  text-decoration-skip-ink: auto;
  -webkit-text-decoration-skip: ink; /* Safari */
}
```

[Online demo](https://oscarotero.github.io/css-style-guide/cases/typography/)