# csl-json-walker

This is supporting code for the [citeproc-js](https://bitbucket.org/fbennett/citeproc-js/wiki/Home) implementation of CSL. The citation formatting methods supplied by `citeproc-js` (`processCitationCluster()` and `makeBibliography()`) are heavy things by their nature. They are suitable candidates for running in a web-worker in the browser environment. Unfortunately, the asynchronous process that runs in a web worker cannot access DOM methods, and `citeproc-js` depends on these to compile locale and style code when it instantiates a style.

The JavaScript snippet here provides two methods, `walkLocaleToObj()` and `walkLocaleToObj()`, for converting the respective XML to a JavaScript object. A web worker running with the `xmljson.js` parser shipped with `citproc-js` can process these objects as drop-in replacements for the XML that they represent.

Frank Bennett
Nagoya
