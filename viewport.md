### Try to get [visual viewport][5]
```js
var w = window.innerWidth || document.documentElement.clientWidth;
var h = window.innerHeight || document.documentElement.clientHeight;
```
### ...or whatever
```js
var w = Math.max(document.documentElement.clientWidth, window.innerWidth || 0)
var h = Math.max(document.documentElement.clientHeight, window.innerHeight || 0)
```
### TOC
- [Pixels](#pixels)
- [Screen size](#screen-size)
  - [window.innerWidth/Height](#windowinnerwidthheight)
  - [window.pageX/YOffset](#windowpagexyoffset)
- [Viewport](#viewport)
  - [document.documentElement.clientWidth/Height](#documentdocumentelementclientwidthheight)
  - [document.documentElement.offsetWidth/Height](#documentdocumentelementoffsetwidthheight)
- [Event coordinates](#event-coordinates)
- [Media queries](#media-queries)
- [Mobile browsers](#mobile-browsers)
  - [Measuring the layout viewport](#measuring-the-layout-viewport)(document.documentElement.clientWidth/Height)
  - [Measuring the visual viewport](#measuring-the-visual-viewport)(window.innerWidth/Height)
- [Resources](#resources)

## Here we go!
Mostly excerpts from [PPK][PPK viewports], with some additions

### Pixels
- CSS pixels
- device pixels

At zoom level 100% one CSS pixel is exactly equal to one device pixel.
CSS pixels increase in size when users zooms in, device pixels stay the same.

### Screen size
Screen size, i.e. screen.width and screen.height are measured in device pixels because they never change,
it is property of the screen (not IE8: it measures in CSS pixels).

#### window.innerWidth/Height
- Total size of the browser window, including scrollbars
- Measured in CSS pixels
- gets [CSS viewport][3] `@media (width)` and `@media (height)` which include scrollbars
- `initial-scale` and zoom [variations][4] may cause mobile values to <b>wrongly</b> scale down to what PPK calls the [visual viewport][5] and be smaller than the `@media` values
- zoom may cause values to be 1px off due to native rounding
- `undefined` in IE8-
- Opera measures it in device pixels.
- buggy Since Firefox 4 to Firefox 24, could give a wrong value before page load on certain circumstances

#### window.pageX/YOffset
- Scrolling offset of the page
- Measured in CSS pixels

### Viewport
The function of the viewport is to constrain the <html> element, which is the uppermost containing block of your site.
The viewport, in turn, is exactly equal to the browser window: it’s been defined as such.

#### document.documentElement.clientWidth/Height
- Viewport dimensions (regardless of the dimensions of the <html> element)
- Measured in CSS pixels
- equals CSS viewport width **minus** scrollbar width
- matches `@media (width)` and `@media (height)` when there is **no** scrollbar
- [same as][6] `jQuery(window).width()` which [jQuery][7] *calls* the <q>browser viewport</q>
- [available cross-browser][8]

If you know your DOM, you know that `document.documentElement` is in fact the <html> element: the root element of any HTML document.
However, the viewport is one level higher, so to speak; it’s the element that contains the <html> element.
That might matter if you give the <html> element a width (it is  not recommended, but still possible).

#### document.documentElement.offsetWidth/Height
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

### Mobile browsers
Two viewports: the visual viewport and the layout viewport.
Visual viewport is kinda window (aperture) moving on top of layout viewport.
The visual viewport is the part of the page that’s currently shown on-screen. The user may scroll to change the part of the page he sees, or zoom to change the size of the visual viewport.

However, the CSS layout, especially percentual widths, are calculated relative to the layout viewport, which is considerably wider than the visual viewport.

How wide is the layout viewport? That differs per browser. Safari iPhone uses 980px, Opera 850px, Android WebKit 800px, and IE 974px.

browsers have chosen their dimensions of the layout viewport such that it completely covers the screen in fully zoomed-out mode (and is thus equal to the visual viewport).

The layout viewport width is always the same. If you rotate your phone, the visual viewport changes, but the browser adapts to this new orientation by zooming in slightly so that the layout viewport is again as wide as the visual viewport.

This has consequences for the layout viewport’s height, which is now substantially less than in portrait mode. But web developers don’t care about the height, only about the width.

### Measuring the layout viewport
#### document.documentElement.clientWidth/Height
- Layout viewport dimensions
- Measured inCSS pixels
- Full support: Opera, iPhone, Android, Symbian, Bolt, MicroB, Skyfire, Obigo
- Problems
  - Visual viewport dimensions in Iris
  - Samsung WebKit reports the correct values when a <meta viewport> tag is applied to the page; the dimensions of the <html> element otherwise.
  - Screen dimensions in device pixels in Firefox
  - IE returns 1024x768. However, it stores the information in document.body.clientWidth/Height. This is consistent with IE6 desktop.

### Measuring the visual viewport
#### window.innerWidth/Height
- Visual viewport dimensions
- Measured in CSS pixels
- Full support: iPhone, Symbian, BlackBerry
- Problems
  - Opera and Firefox return the screen width in device pixels.
  - Android, Bolt, MicroB, and NetFront return the layout viewport dimensions in CSS pixels.
- Not supported
  - IE, but it gives the visual viewport dimension in document.documentElement.offsetWidth/Height.
  - Samsung WebKit reports either the dimensions of the layout viewport or of the <html>, depending on whether a <meta viewport> tag has been applied to the page or not.

---
## Resources

- [Live outputs for various dimensions][9] 
- [<b>verge</b>][10] uses cross-browser viewport techniques 
- [<b>actual</b>][11] uses `matchMedia` to obtain precise dimensions in any unit
- [stackoverflow answer][stackoverflow answer]
- [PPK viewports][PPK viewports]
- [PPK viewports2][PPK viewports2]

  [PPK viewports]: http://www.quirksmode.org/mobile/viewports.html
  [PPK viewports2]: http://www.quirksmode.org/mobile/viewports2.html
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
