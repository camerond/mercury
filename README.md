# Mercury

Mercury is a set of assorted Sass mixins used in Hashrocket projects.

## Responsive Mixins

Mercury's responsive mixins use 3 viewport breakpoints, set by the variables `$site-width-max`, `-mid` and `-narrow`. They're `!default`, so you can override them from outside the file at will. They default to 1400, 800 and 480px, respectively.

Save typing time & readability by using `+tablet` and `+mobile` mixins, which rely on the above breakpoint presets, 

### `+tablet`, `+mobile` and `+max`

`+tablet` and `+mobile` are shorthand for `max-width($site-width-mid)` and `max-width($site-width-narrow)`, respectively.

`+max` is shorthand for `+min-width($site-width-max)`, so you can set maximum values on elements that might otherwise rely on `vw` units (for example).

### `+responsive`

Inject a bunch of responsive styles in one line of code by using the `+responsive` mixin, ` which is detailed [in this post over at the Hashrocket blog](http://hashrocket.com/blog/posts/drop-in-responsive-styles-with-sass).

### `+max-width` and `+min-width`

If you need to specify an arbitrary breakpoint, just use `+max-width` or `+min-width`.

## Print Mixins

Hiding/showing elements for printing comes up fairly often; use `+print` and `+hide-print` to get the job done in one easy line.

## SVG Background Support

Use Mercury to easily include SVG paths as background images. Here's a simple example using a 20x20 circle. Just register your SVG path:

```
+register-svg(my_circle, 20, 20, "<circle cx='10' cy='10' r='10' />")
```

... and now it's available as a background image, using `svg-url`:

```
.foo
  background: svg-url(my_circle) center no-repeat
```

You can then resize the background using `background-size` and otherwise treat it just like a normal background image.

## Clearfix

There's a clearfix.
