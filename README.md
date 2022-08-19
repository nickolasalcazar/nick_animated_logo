# Animated SVG Logo
An animated logo of my name made with an SVG and CSS.

Inspired a [guide](https://www.cassie.codes/posts/creating-my-logo-animation/) by Cassie Codes.

#How I gave the logo a handwriting animation

To make the logo look like it is being handwritten, we make use of the `<clipPath>` HTML element.

According to [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/clipPath), `<clipPath>` "restricts the region to which paint can be applied. Conceptually, parts of the drawing that lie outside of the region bounded by the clipping path are not drawn."

In this example, `<clipPath>` is used to define a region (the enclosed region within the SVG path of letter 'N') where any paint outside of the region will be ignored. An animation is used to 'draw' within this region by interacting with a properties of an SVG path that contained with the same region. The article [How SVG Line Animation Works](https://css-tricks.com/svg-line-animation-works/) by Chris Coyier explains this concept.

To make the handwriting animation for the letter 'N', wrap the 'N' path in a `<clipPath>` element and give the `<clipPath>` element an ID like `id="letter-n"`.
```
<svg id="logo-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
  <clipPath id="letter-n>
    <path d="...">
  </clipPath>
</svg>
```
Then add the path that will be displayed 'within' the letter 'N' - she `stroke` of this path will draw the letter.
```
<svg id="logo-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
  <clipPath id="letter-n>
    <path d="...">
  </clipPath>
  <path clip-path="url(#letter-n)" id="letter-n-path" d="..."/>
</svg>
```
Then add the following CSS:
```
#letter-n-path {
  stroke-width: 27.4px;       /* Thickness of the line that draws 'N'  */
  stroke-dasharray: 1200;     /* How many pieces the letter of made of */
  animation: draw-letter-n 2s forwards reverse;
}

@keyframes draw-letter-n {
  to {
    stroke-dashoffset: 1200;
  }
}
```