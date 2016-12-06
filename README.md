# Mercury

Mercury is a set of assorted Sass mixins used in Hashrocket projects.

## Responsive Mixins

Mercury's responsive mixins use up to 5 viewport breakpoints:

- `$site-width-max: 1400px`
- `$site-width-mid: 800px;`
- `$site-width-narrow: 480px;`

They're `!default`, so you can override them from outside the file at will.

### `tablet`, `mobile` and `max`

Save typing time & readability by using `tablet` and `mobile` mixins, which rely on the above breakpoint presets. `tablet` and `mobile` are shorthand for `max-width($site-width-mid)` and `max-width($site-width-narrow)`, respectively.

`max` is shorthand for `min-width($site-width-max)`, so you can set maximum values on elements that might otherwise rely on `vw` units. For example:

```scss
.foo {
  // default to 80% of viewport ...
  width: 80vw;

  // for tablets and smaller, 90% of viewport ...
  @include tablet {
    width: 90vw;
  }

  // and if the viewport is larger than $site-width-max, fix the width at 1000px.
  @include max {
    width: 1400px;
  }
}

```

### `responsive`

Inject a bunch of responsive styles in one line of code by using the `responsive` mixin, which is detailed [in this post over at the Hashrocket blog](http://hashrocket.com/blog/posts/drop-in-responsive-styles-with-sass).

```scss
// font size will be 20px default, 14px for narrower than `$site-width-mid`,
// and 10px for narrower than `$site-width-narrow`

.foo {
  @include responsive(font-size, 20px, 14px, 10px);
}
```

### `max-width` and `min-width`

If you need to specify an arbitrary breakpoint, just use `max-width` or `min-width`.

```scss
@include max-width(550px) {
  // only show for viewports <= 550px
}
```

### `max-vw`

A big downside to using `vw` units is that they scale to the viewport no matter what – and for very wide viewport sizes (fullscreened on an external monitor, for example) this can start to look absurd.

The `max-vw` mixin does a bit of quick math for you: using the `max` mixin (detailed above), it overrides your `vw` value with a fixed pixel equivalent to what the `vw` value would be at `$site-width-max`. An example will help:

```scss
.foo {
  // assign margins of 10vw, 5vw and 2vw for default, tablet and mobile widths, respectively.

  @include responsive(margin, 10vw, 5vw, 2vw);

  // BUT, for viewport sizes larger than $site-width-max,
  // keep the margin at the equivalent of 10% of $site-width-max.

  @include max-vw(margin, 10);

  // So now, even when the window gets extremely wide,
  // the margin value will cap out at 10% of $site-width-max (140px).
}
```

## Including Viewport Height

If you set `$scaleToViewportHeight` to `true`, Mercury's responsive mixins will also take viewport height into consideration. These values, by default, are:

- `$site-height-mid: 800px`
- `$site-height-short: 480px;`

For example, `@include tablet` will trigger at a viewport width less than `$site-width-mid` OR a viewport height less than `$site-width-height`.

## Print Mixins

Hiding/showing elements for printing comes up fairly often; use `+print` and `+hide-print` to get the job done in one easy line.

```scss
.foo {
  @include print {
    // these attributes will only affect the print styles
  }
  @include hide-print {
    // these attributes won't affect the print styles
  }
}
```

## SVG Background Support

Use Mercury to easily include SVG paths as background images. Here's a simple example using a 20x20 circle. Just register your SVG path with a name, viewBox width, viewBox height, and path data (this saves the SVG to a Sass map where it can be accessed via `svg-url`):

```scss
@include register-svg(my_circle, 20, 20, "<circle cx='10' cy='10' r='10' />");
```

... and now it's available as a background image, using `svg-url`:

```scss
.foo {
  background: svg-url(my_circle) center no-repeat;
}
```

`svg-url` takes two optional arguments: `$fill` and `$rendering`. They can either be named, or passed in that order.

`$fill` wraps your path in a `<g>` with a `fill` color:

```scss
.foo {
  background: svg-url(my_circle, #ff0000) center no-repeat;
}
```

`$rendering` lets you override the default rendering, which is `geometricPrecision`.

You can then resize the background using `background-size` and otherwise treat it just like a normal background image.

## Other Utilities

Mercury also includes a couple of common, self-explanatory utility mixins:

```
@include clearfix;
@include hide-text;
```
