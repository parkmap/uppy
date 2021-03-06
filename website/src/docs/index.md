---
title: "Getting Started"
type: docs
permalink: docs/
alias: api/
order: 0
---

Uppy is a sleek, modular file uploader that integrates seemlessly with any framework. It fetches files from local disk, Google Drive, Dropbox, Instagram, remote URLs, cameras and other exciting locations, and then uploads them to the final destination. It’s fast, easy to use and let's you worry about more important problems than building a file uploader.

Uppy consists of a core module and [various plugins](/docs/plugins/) for selecting, manipulating and uploading files. Here’s how it works:

```js
const Uppy = require('uppy/lib/core')
const Dashboard = require('uppy/lib/plugins/Dashboard')
const Tus = require('uppy/lib/plugins/Tus')
 
const uppy = Uppy({ autoProceed: false })
  .use(Dashboard, {
    trigger: '#select-files'
  })
  .use(Tus, {endpoint: '//master.tus.io/files/'})
  .run()
 
uppy.on('core:success', (files) => {
  console.log(`Upload complete! We’ve uploaded these files: ${files}`)
})
```

[Try it live](/examples/dashboard/)

Drag and Drop, Webcam, basic file manipulation (adding metadata), uploading via tus resumable uploads or XHR/Multipart is all possible using just the uppy client module.

Adding [Uppy Server](/docs/server/) to the mix enables remote sources, such as Instagram, Google Drive and Dropbox. Uploads from remote sources are handled server-to-serber,(so a 5 GB video won’t be eating into your mobile data plan. Files are removed from Uppy Server after an upload is complete, or after a reasonable timeout. Access tokens also don’t stick around for long, for security reasons.

## Installation

``` bash
$ npm install uppy
```

We recommend installing from NPM and then using a module bundler such as [Webpack](http://webpack.github.io/), [Browserify](http://browserify.org/) or [Rollup.js](http://rollupjs.org/).

If you like, you can also use a pre-built bundle, for example from [unpkg CDN](https://unpkg.com/uppy/). In that case `Uppy` will attach itself to the global `window.Uppy` object.

> ⚠️ The bundle currently consists of most Uppy plugins, so this method is not  recommended for production, as your users will have to download all plugins, even if you are using just a few.

1\. Add a script to the bottom of `<body>`:

``` html
<script src="https://unpkg.com/uppy"></script>
```

2\. Add CSS to `<head>`:
``` html
<link href="https://unpkg.com/uppy/dist/uppy.min.css" rel="stylesheet">
```

3\. Initialize:

``` html
<script>
  var uppy = Uppy.Core({ autoProceed: false })
  uppy.use(Uppy.DragDrop, {target: '.UppyDragDrop'})
  uppy.use(Uppy.Tus, {endpoint: '//master.tus.io/files/'})
  uppy.run()
</script>
```

## Documentation

- [Uppy](/docs/uppy/) — full list of options, methods and events.
- [Plugins](/docs/plugins/) — list of Uppy plugins and their options.
- [Server](/docs/server/) — setting up and running an uppy-server instance, which adds support for Instagram, Dropbox, Google Drive and other remote sources.
- [React](/docs/react/) — components to integrate uppy UI plugins with react apps.
- Architecture & Making a Plugin — how to write a plugin for Uppy [documentation in progress].

## Browser Support

<a href="https://saucelabs.com/u/transloadit-uppy">
  <img src="https://saucelabs.com/browser-matrix/transloadit-uppy.svg" alt="Sauce Test Status"/>
</a>

Note: we aim to support IE10+ and recent versions of Safari, Edge, Chrome, Firefox and Opera. IE6 on the chart above means we recommend setting Uppy to target a `<form>` element, so when Uppy has not yet loaded or is not supported, upload still works. Even on the refrigerator browser. Or, yes, IE6.
