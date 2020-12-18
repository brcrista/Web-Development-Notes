# Front end frameworks

## CSS resets

1. https://www.webfx.com/blog/web-design/the-history-of-css-resets/
1. https://www.webfx.com/blog/web-design/a-comprehensive-guide-to-css-resets/
1. https://www.webfx.com/blog/web-design/should-you-reset-your-css/

A few popular options:

* [Eric Meyer's reset stylesheet](https://meyerweb.com/eric/tools/css/reset/)
    - Erases all default styles
    - This one is very popular, though Eric Meyer himself has recommended that people should adapt it to their own uses rather than just copy-pasting it blindly.
* [Normalize.css](https://necolas.github.io/normalize.css)
    - Adds a set of default styles to override individual browsers' defaults
* Bootstrap contains its own reset file based on Normalize.css: [_reboot.scss](https://github.com/twbs/bootstrap/blob/9f9e4d04a127b3505f01bb6c341d3d40430f39ff/scss/_reboot.scss).

## Frameworks

* [Bootstrap](https://getbootstrap.com)
* [HTML5 Boilerplate](https://html5boilerplate.com)
    - This is [intended for static sites](https://github.com/h5bp/html5-boilerplate/blob/v8.0.0/dist/doc/usage.md).
      As you can see from the source code, it would take some work to chop up and put into Razor views.
