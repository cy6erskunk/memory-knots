## Mouseover and mouseout

Problem: `mouseover` event is triggered when child elements are entered due to event bubbling.  

W3C added `relatedTarget` property
which contains the element the mouse came from in case of `mouseover`, or the element it goes to in case of `mouseout`.

Microsoft as usually created their own solution, `fromElement` to use with `mouseover` and `toElement` for `mouseout`.
Standard one is supported since IE9.

NB: jQuery normalizes this stuff to standard one (W3C), so normalized property is `relatedTarget` one.

## mouseenter and mouseleave

The same as `mouseover` and `mouseout`, but without bubbling to solve all that problems with extra triggers inside layer.  
Were invented by IE (present in 5.5), nowadays part of the 
[UI Events Spec](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-mouseenter).  
Implemented since Chrome 30 and FF 10.
