
### Coordinate systems
Basically there are two coordinate systems: relative to `document` and relative to `window` (i.e. relative to the viewport).
They are the same before scrolling, as document coordinates are window coordinates plus scroll.

### Clumpsy way of determining position
There are properties telling us offset of the elements relative to `offsetParent` and thus requiring us to do recursive calculations to get element position.
Moreover these properties are somewhat inconsistent between browsers and there are some issues with margins/paddings/borders (?source?).
`element.offsetTop` and `element.offsetLeft` read-only properties return corresponding offset relative to `HTMLElement.offsetParent` padding box.

`HTMLElement.offsetWidth` and `HTMLElement.offsetHeight` read-only properties. Typically they include borders, padding and scrollbar (if present, if rendered).

### 'Like-a-Boss' way of getting position
`Element.getBoundingClientRect()` method returns the size of an element and its position **relative to the viewport**.
The returned value is a `DOMRect` object, 

    DOMRect = {
        left
        top
        right
        bottom
        [width]
        [height]
    }
 
which contains read-only properties describing the border-box in pixels. `width` and `height` are not standard (available in FF and Chrome???).

#### Scrolling
```js
var scrollLeft = (window.pageXOffset !== undefined) ?
    window.pageXOffset :
    (document.documentElement || document.body.parentNode || document.body).scrollLeft;
var scrollTop = (window.pageYOffset !== undefined) ?
    window.pageYOffset :
    (document.documentElement || document.body.parentNode || document.body).scrollTop;
```

or even 
```javascript
(((t = document.documentElement) || (t = document.body.parentNode)) && typeof t.ScrollLeft == 'number' ?
    t :
    document.body).ScrollLeft
```
in third part of ternary operator.
The `pageXOffset` property is an alias for the `scrollX` property.
All browsers except IE<9 support `pageXOffset/pageYOffset`, and in IE when DOCTYPE is set, the scroll can be taken from documentElement(<html>), otherwise from `body`.

### Another gotcha
The document (`html` or `body`) can be shifted from left-upper corner in IE:
```js
var topAdjunct = docElem.clientTop || body.clientTop || 0;
var leftAdjunct = docElem.clientLeft || body.clientLeft || 0;
```
