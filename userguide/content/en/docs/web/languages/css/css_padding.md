---
title: CSS Padding
---

The CSS `padding` properties are used to generate space around an element's content, inside of any defined borders.

With CSS, you have full control over the padding. There are properties for setting the padding for each side of an element (top, right, bottom, and left).

## Padding - Individual Sides

CSS has properties for specifying the padding for each side of an element:
*	`padding-top`
*	`padding-right`
*	`padding-bottom`
*	`padding-left`

All the padding properties can have the following values:
*	length - specifies a padding in px, pt, cm, etc.
*	% - specifies a padding in % of the width of the containing element
*	inherit - specifies that the padding should be inherited from the parent element
Note: Negative values are not allowed.

### Example
Set different padding for all four sides of a `<div>` element:
```css
div {
  padding-top: 50px;
  padding-right: 30px;
  padding-bottom: 50px;
  padding-left: 80px;
}
```


## Padding - Shorthand Property
To shorten the code, it is possible to specify all the padding properties in one property.

The `padding` property is a shorthand property for the following individual padding properties:
*	`padding-top`
*	`padding-right`
*	`padding-bottom`
*	`padding-left`
So, here is how it works:

If the `padding` property has four values:
*	**padding: 25px 50px 75px 100px;**
	*	top padding is 25px
	*	right padding is 50px
	*	bottom padding is 75px
	*	left padding is 100px
### Example
Use the padding shorthand property with four values:
```css
div {
  padding: 25px 50px 75px 100px;
}
```
If the padding property has three values:
*	**padding: 25px 50px 75px;**
	*	top padding is 25px
	*	right and left paddings are 50px
	*	bottom padding is 75px
### Example
Use the padding shorthand property with three values:
```css
div {
  padding: 25px 50px 75px;
}
```