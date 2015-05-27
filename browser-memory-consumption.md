## Browsers Memory Consumption

The table below displays memory consumption by different browsers when opening static HTML pages of different size.
All pages are constructed using numerous `<span>` elements with the 
```
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Magnam debitis, dolor atque voluptatum numquam consequuntur exercitationem quisquam eaque tempora quis soluta fuga ad beatae illum dicta magni eos! Doloremque, tenetur.
```
text content.

|   | 20Mb page | 40Mb page | 100Mb page | 200Mb page |
| --- | --------- | --------- | ---------- | ---------- |
|Google Chrome<br/>43.0.2350.0 canary (64-bit) — OSX | 180 - ... Mb  |300 - ... Mb | 680 - ... Mb | 1.3 - ... Gb|
Google Chrome<br/>41.0.2272.104 (64-bit) — OSX|180 - ... Mb | 300 - ... Mb | 650 - ... Mb | 1.2 - ... Gb
Google Chrome<br/>41.0.2272.101 m — Win 7|130 - ... Mb|180 - … Mb|420 - … Mb|??? (800 Mb)
Mozilla Firefox<br/>36.0.4 — OSX|180 (120) Mb|370 (230) Mb|730 (530) Mb|1.3 (1.1) Gb
Mozilla Firefox<br/>36.0.4 — OSX<br/>before minimisation |260 (120) Mb|550 (380) Mb||
Safari<br/>8.0.4 — OSX|180 Mb|???|???|???
MS IE 11 — Win 7|230 Mb|470 Mb|1.0 Gb|??? (1.7 — 2.0 Gb)
MS IE 10 — Win 7|180 Mb|340 Mb|1.0 Gb|1.5 Gb

All values are roughly rounded average values of at least 3 measurements. The accuracy is ~10%.

### Data Sources
- Google Chrome: Values from Chrome Task Manager were used (they seem to be almost the same as Private Working Set
in Windows Task Manager or Memory value in OS X Activity Monitor)
- Firefox: data from “about:memory” page were used, measurements were made after doing “GC”, “CC"
and "Minimize memory usage”. The  overall “Explicit allocations” value and “top” for the 
corresponding page is listed. For 20 and 40 Mb pages, values obtained before memory minimisation are also listed.
- Safari: Value from Activity Monitor is used
- IE:  Task Manager — Private Working Set values

### Notes
Notation "XXX — …" for Chrome browser it means that initially it consumes XXX of memory,
but this number increases when the user interacts with page (e.g. scrolls it).
After a while the memory usage might decrease but to values which are generally higher than the original value (XXX).

It took Safari about 3 minutes to load a 20Mb page; bigger size pages could not be loaded (browser was still
working after tens of minutes; however, it did not hang down, the tab could be easily closed).

Google Chrome for Windows could not load a 200Mb page: the browser seemed to finish downloading
the page in 8 minutes (as there was no network activity and CPU load) but it  failed to render
and display the very end of the page (the last 5%).

IE11 could not load a 200Mb page at all: the page hangs in the browser;
it is reloaded or the CPU load is stable at ~50% usage rate and nothing happens.

