express-busboy
--------------

A simple `body-parser` like module for express that
uses [`connect-busboy`](https://github.com/mscdex/connect-busboy) under the hood.

It's designed to be more of a "drop in" replacement for `body-parser`.
With it populating `req.body`, there is very minimal code change needed to use it.

usage
-----

```js
var bb = require('express-busboy');
var app = express();

bb.extend(app);
```

The module will populate `req.body` and `req.files` like the `body-parser` module does.

configuration
-------------

```js
bb.extend(app, {
    //busboy options can go here
});
```

file uploads
------------

By default file uploads are disabled, the `req.files` object will always be empty. You can activate them with:

```js
bb.extend(app, {
    upload: true,
    path: '/path/to/save/files',
    allowedPath: /./
});
```

`path` will default to: `os.tmpdir()/express-busboy/<uuid>/<the field name>/<filename>`.

allowedPath can contain a regular expression limiting the upload function to given urls. For example `/^\/upload$/` would only allow uploads in the /upload path.


You can have a function returning true/false if you prefer that:

```js
options.allowedPath = function(url) {
    return url == '/upload';
}
```

build
-----

[![Build Status](https://travis-ci.org/yahoo/express-busboy.svg?branch=master)](https://travis-ci.org/yahoo/express-busboy)
