    var w = Math.max(document.documentElement.clientWidth, window.innerWidth || 0)
    var h = Math.max(document.documentElement.clientHeight, window.innerHeight || 0)

## Excerpt from [PPK][PPK viewports]
### Pixels
- CSS pixels
- device pixels

At zoom level 100% one CSS pixel is exactly equal to one device pixel.
CSS pixels increase in size when users zooms in, device pixels stay the same.

### Screen size
Screen size, i.e. screen.width and screen.height are measured in device pixels because they never change,
it is property of the screen (not IE8: it measures in CSS pixels).

### window.innerWidth/Height
- Total size of the browser window, including scrollbars
- Measured in CSS pixels
- gets [CSS viewport][3] `@media (width)` and `@media (height)` which include scrollbars
- `initial-scale` and zoom [variations][4] may cause mobile values to <b>wrongly</b> scale down to what PPK calls the [visual viewport][5] and be smaller than the `@media` values
- zoom may cause values to be 1px off due to native rounding
- `undefined` in IE8-
- Opera measures it in device pixels.
- buggy Since Firefox 4 to Firefox 24, could give a wrong value before page load on certain circumstances

### window.pageX/YOffset
- Scrolling offset of the page
- Measured in CSS pixels

### Viewport
The function of the viewport is to constrain the <html> element, which is the uppermost containing block of your site.
The viewport, in turn, is exactly equal to the browser window: it’s been defined as such.

### document.documentElement.clientWidth/Height
- Viewport dimensions (regardless of the dimensions of the <html> element)
- Measured in CSS pixels
- equals CSS viewport width **minus** scrollbar width
- matches `@media (width)` and `@media (height)` when there is **no** scrollbar
- [same as][6] `jQuery(window).width()` which [jQuery][7] *calls* the <q>browser viewport</q>
- [available cross-browser][8]

If you know your DOM, you know that document.documentElement is in fact the <html> element: the root element of any HTML document.
However, the viewport is one level higher, so to speak; it’s the element that contains the <html> element.
That might matter if you give the <html> element a width (it is  not recommended, but still possible).

### document.documentElement.offsetWidth/Height
- Dimensions of the <html> element (and thus of the page)
- Measured in CSS pixels
- IE measures the viewport, and not the <html> element

### Event coordinates
pageX/Y gives the coordinates relative to the <html> element in CSS pixels.
clientX/Y gives the coordinates relative to the viewport in CSS pixels.
screenX/Y gives the coordinates relative to the screen in device pixels.
- IE doesn’t support pageX/Y
- IE and Opera calculate screenX/Y in CSS pixels

### Media queries
width/height uses the same values as documentElement .clientWidth/Height (the viewport, in other words). It works with CSS pixels.
device-width/device-height uses the same values as screen.width/height (the screen, in other words). It works with device pixels.

---
## Resources

- [Live outputs for various dimensions][9] 
- [<b>verge</b>][10] uses cross-browser viewport techniques 
- [<b>actual</b>][11] uses `matchMedia` to obtain precise dimensions in any unit
- [stackoverflow answer][stackoverflow answer]
- [PPK viewports][PPK viewports]

  [PPK viewports]: http://www.quirksmode.org/mobile/viewports.html
  [1]: http://dev.w3.org/csswg/mediaqueries/#width
  [2]: http://dev.w3.org/csswg/mediaqueries/#height
  [3]: http://www.w3.org/TR/CSS2/visuren.html#viewport
  [4]: https://github.com/ryanve/verge/issues/13
  [5]: http://www.quirksmode.org/mobile/viewports2.html
  [6]: https://github.com/jquery/jquery/blob/1.9.1/src/dimensions.js#L12-L17
  [7]: https://api.jquery.com/width/
  [8]: http://www.quirksmode.org/mobile/tableViewport.html
  [9]: http://ryanve.com/lab/dimensions/
  [10]: http://github.com/ryanve/verge
  [11]: http://github.com/ryanve/actual
  [stackoverflow answer]: http://stackoverflow.com/questions/1248081/get-the-browser-viewport-dimensions-with-javascript
