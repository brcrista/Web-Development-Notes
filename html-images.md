# Images in HTML

* Always set the `width` and `height` attributes for the image.
  - This way, the browser will know how much space to reserve in the layout for the image before it loads.
  - Without this, users might see the page shift around when the image loads.
* Always scale the image to the size it will appear on the page.
  - This is from the *HTML & CSS* book. I'm guessing it's to avoid distorting the image or other visual artifacts from shrinking it.
  - That book is kind of old though -- 2011. It doesn't really treat targeting mobile devices at all.
* Counterintuitively to many people, images are `display: inline` by default. You may prefer to add this to your CSS reset file:

```css
img {
  display: block;
}
```
