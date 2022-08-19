# Animated SVG Logo
An animated logo of my name made using an SVG HTML element and CSS.

[See the animation here.](https://nickolasalcazar.github.io/nick_animated_logo/)

Inspired by a [guide](https://www.cassie.codes/posts/creating-my-logo-animation/) by Cassie Codes.

## Animating handwriting

To animate the logo to look like it is being handwritten, use of the `<clipPath>` element.

According to [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/clipPath), `<clipPath>` "restricts the region to which paint can be applied. Conceptually, parts of the drawing that lie outside of the region bounded by the clipping path are not drawn."

In this example, a `<clipPath>` element is used to define a **stensil** that will be painted within. The shape of that stensil is an SVG path in the shape of the letter 'N'.

Then, an animation is used to paint within this `<clipPath>` (AKA 'stensil') by interacting with a properties of a separate SVG path that is contained with the `<clipPath>`. The article [How SVG Line Animation Works](https://css-tricks.com/svg-line-animation-works/) by Chris Coyier demonstrates how to make an SVG path 'draw' itself by using the path's `stroke` properties.

Essentially, we define a `<clipPath>` that is the shape of a letter, which acts like a stensil. Within this stensil, we draw the path of the letter that we want to animate as handwriting.

### Define the clipPath
First define the 'stensil' using a `<clipPath>`.

The path of the letter 'N' is defined in the `<path>` tag below. We wrap the `<path>` tag in a `<clipPath>` element and give the `<clipPath>` element an ID, `letter-n`. This creates a stensil in the shape of the `<path>` element.
```
<svg id="logo-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
  <clipPath id="letter-n">
    <path d="..." />
  </clipPath>
</svg>
```
We have now created our stensil in the shape of the letter 'N', as defined by the `<path>` element. Now we need to draw in it.

### Draw within the clipPath
Add the path that will be drawn within the letter 'N'. To draw within the `<clipPath id="letter-n">`, assign the `<path>` element the attribute `clip-path="url(#letter-n)"`. Also assign it the ID `letter-n-path` to select the element in CSS.
```
<svg id="logo-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
  <clipPath id="letter-n">
    <path d="...">
  </clipPath>
  <!-- The path that will be drawn within id="letter-n" -->
  <path clip-path="url(#letter-n)" id="letter-n-path" d="..."/>
</svg>
```
Then add the following CSS to animate the path:
```
#letter-n-path {
  stroke-width: 27.4px;       /* Thickness of the line that draws 'N'  */
  stroke-dasharray: 1200;     /* How many pieces the letter is made of */
  animation: draw-letter-n 2s forwards reverse;
}

@keyframes draw-letter-n {
  to {
    stroke-dashoffset: 1200;
  }
}
```
This should draw a path within the stensil defined by the `<clipPath>` element, and appear as though the element is being handwritten.