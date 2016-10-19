#WAT?
```  
  <link rel="shortcut icon" href="whatever.ico" type="image/x-icon">
```
Favicon was initially introduced in IE5 in March 1999 — `/favicon.ico` was used to get an icon when saving page to the Bookmarks.

## Some facts
- IE 5-10 support `.ico` only
- IE 5-8  support `rel="shortcut icon"` only
- IE 9+ supports `rel="icon"`, but requires `type` to be declared (`type="image/vnd.microsoft.icon"` or `type="image/x-icon"`)
- IE 11 supports `rel="icon"` and various image formats (GIF, PNG)

## Painful fact 
- IE10 does not support conditional comments and it does not support PNG favicons as well — it makes impossible
to leave serarate declaration with ICO file wrapped in conditional comments for IE only

## Corner cases
> If links for both image (PNG) and ICO favicons are present:

### `Firefox` and `Safari`
-  use the favicon that comes __last__ (any size)

### `Chrome`
- for Mac
  - is any ICO formatted? use last
  - otherwise last @32 favicon
  - otherwise last @16
  - otherwise whatever
- for Windows
  - last @16 favicon
  - last ICO
  - @32 favicon
  - whatever

### Opera
will choose completely at random.

### Internet Explorer 8 on WindowsXP
(max possible version of IE on XP)
- single link@rel='shortcut icon'@href='favicon.ico' with icon built from PNGs is displayed correct (even w/o @type)
- tries to get `/favicon.ico` in absence of link@rel='shortcut icon'
- ignores all but __first__ link
- displays @16 version in favorites bar, @32 on desktop and in Start menu

### IE9, IE10 on Win7
- `rel="icon"` requires `type="icon/x-icon"` or `type="image/vnd.microsoft.icon"` to work
  - when both present, `rel="icon"` overrides `rel="shortcut icon"`

### Edge, IE 11 on Win 10
- displays the very __first__ one with `@rel="icon"`
  - otherwise first `@rel="shortcut icon"`

### Mac
- iOS Safari does not support transparency in `apple-touch-icon` and replaces alpha-channel with opaque black
  - w/o `apple-touch-icon` it shows square screenshot of the page in the icon
- OSX Safari uses `apple-touch-icon` to display icon in favorites page and supports transparency
- Safari on iOS 7 doesn’t add effects to icons, older versions  won't add effects for files named with `-precomposed.png` suffix
- [Icon and Image Sizes](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)
- Safari 9 uses special [`mask-icon`](https://developer.apple.com/library/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9.html#//apple_ref/doc/uid/TP40014305-CH9-SW20) to display in pinned tab (`rm -fr ~/Library/Safari/Template\ Icons/` and restart Safari to clear pinned tabs icon cache)
