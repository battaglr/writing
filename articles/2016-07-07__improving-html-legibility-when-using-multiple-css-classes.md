# Improving HTML legibility when using multiple CSS classes

Lately one of my primary concerns is writing code that can be understood
quickly, and using multiple CSS classes on an HTML element can —*in some
cases*— compromise that.

That’s why I like separating different *kind* of classes with a slash.

```html
<div class="Card">
  <span class="Card-icon / Icon Icon--close"></span>
  ...
</div>
```

By doing this we can easily improve the legibility and make our code look neat
at the same time.

*This is certainly not a new or original idea, but just wanted to share the
thought.*
