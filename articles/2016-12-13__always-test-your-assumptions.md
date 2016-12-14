# Always test your assumptions

Not every field allows the opportunity to usually perform quick and easy tests
for our assumptions. Sometimes we let ourselves take a decision based on
previous thoughts —or even by someone else’s thoughts— without even doing a
quick check.

I would like to have drop-jawing examples, but I don’t, so I’ll tell you how
I ended-up saving a few bytes in two occasions by simply doing really
quick tests.

> *I will be using real code examples from the
[cells order](https://github.com/battaglr/griss-cells-order/) module for
[Griss](https://github.com/battaglr/griss/), so you can reproduce these tests
if you want.*

> *Also to facilitate readability the CSS escape character is not included, and
some fractions of the code have been simplified.*

## Assumption #1

I had a CSS property —`position: relative`— that had to be repeated for the
126 classes my module had —most of the times automatically by using Sass.

I had two options:

1. Repeat `position: relative` 126 times —probably not the brightest idea.
2. Create an abstraction, and only write it once.

Of course, I choose the second option and wrote:

```scss
[class*="gs-Grid-cell--push"],
[class*="gs-Grid-cell--pull"] {
  position: relative;
}
```

But then I thought, *what would happen once the file has being minified and
gzipped?* Well, apparently increase its size by 11 bytes compared with the
version that had `position: relative` repeated 126 times.

So, I had an unnecessary abstraction that increased my file size by 11 bytes,
and surely will end-up cluttering the dev tools panels. Of course, 11 bytes
aren’t much, and if I thought that they will increase the code readability
I would have probably paid the price; but in this case it wasn’t worth it, and
decided to repeat a declaration 126 times.

Good choice or bad choice? I think it was a good choice, of course. But it was
a choice that I could only make after testing my assumption, otherwise I
wouldn’t have the opportunity to make it.

## Assumption #2

After that, I had this code that would compile to 6 different rules:

```scss
.gs-Grid-cell--push(n)@#{$breakpoint} {
  position: relative;
  left: auto;
}

.gs-Grid-cell--pull(n)@#{$breakpoint} {
  position: relative;
  right: auto;
}
```

Since with these rules I’m overriding another rule that must already have
`position: relative`, I can remove that declaration and save a few more bytes.
But since I was already in this *testing spree*, I thought, *why not?*.
Turns out that by removing that declaration the weight of the file after
being minified and gzipped increased by 3 bytes, proving me wrong yet
another time —and making me realize that I need to understand gzip better.

*Yes*, I know 3 bytes are almost nothing, but *hey!*, I saved 3 bytes by just
testing another simple assumption. And of course you can’t test every single
thought you have each day; but you can test quite a bit of them, and that will
certainly make a difference.
