# The `border` confusion

From time to time I see how the confusion or discussion around `border: 0` or
`border: none` arises in a code review or a casual talk.

Let’s try to clarify this a bit.

The `border` property is a [shorthand](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)
property, and as such it allows us to set values of other properties
simultaneously. The following declarations are equivalent:

```
border: 1px solid #000;
```

```
border-width: 1px;
border-style: solid;
border-color: #000;
```

Therefore when we use `border: 0` is the same as using `border-width: 0`,
and when we use `border: none` is the same as using `border-style: none`.
Since a border without width or style can not be rendered, both values are
equivalent in this context.

If our intention is to remove a border, probably the most explicit way to
express it is by defining a width of zero, that’s why I prefer to
use `border: 0`.

Finally, and to be honest, we shouldn’t *care* much about this. We have a
problem to solve —to remove some border— it doesn’t matter how we do it.
The smart —*lazy*— thing to do is to let our tools do this work for us
—*and I’m not suggesting that you add a rule in your linter for this*.
If some value saves a few more bits than other, great, let’s choose a
minifier that can optimize that and use it.
