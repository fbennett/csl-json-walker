# csl-json-walker

This is supporting code for the
[citeproc-js](https://bitbucket.org/fbennett/citeproc-js/wiki/Home)
implementation of CSL. The citation formatting methods supplied by
`citeproc-js` (`processCitationCluster()` and `makeBibliography()`)
are heavy things by their nature. They are suitable candidates for
running in a web-worker in the browser environment. Unfortunately, the
asynchronous process that runs in a web worker cannot access DOM
methods, and `citeproc-js` depends on these to compile locale and
style code when it instantiates a style.

The JavaScript snippet here provides two methods, `walkStyleToObj()`
and `walkLocaleToObj()`, for converting the respective XML to a
JavaScript object. A web worker running with the `xmljson.js` parser
shipped with `citproc-js` can process these objects as drop-in
replacements for the XML that they represent.

Note that `walkStyleToObj()` returns an object with two keys: one for
the style, and one for a set of locale keys needed to run the style.
The worker should run this method first, report the locale keys back
to the main thread, where the required locales should be converted and
supplied back to the worker.

(This may all seem rather involved, but removing the processor from
the main thread has a pretty dramatic effect on user experience. If
you run `citeproc-js` in the browser, this is definitely worth setting
up.)

Frank Bennett
Nagoya
