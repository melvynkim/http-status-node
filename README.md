HTTP statuses for Node
==========
`http-status-node` is a node wrapper for http status codes.

Usage
-----

Require this module in your code and get a status object by key.
Status objects contain `code`, `message` and `createError` method to create convenient node.js 
`Error` instance with all status data included.  

Example
-----

```

const express = require('express');
const  Q = require('q');
const HTTP_STATUSES = require('http-status-node');
const app = express();

app.get('/', function (req, res) {
  Q
    .try(function () {
      if (!req.param('ok')) {
        throw HTTP_STATUSES.BAD_REQUEST.createError("Not ok");
      }
      res.send("ok", HTTP_STATUSES.OK.code);
    })
    .catch(function(err) {
      res.send(err.message, err.httpStatus.code);
    });
});

const  server = app.listen(3000, function() {
  console.log('Listening on port %d', server.address().port);
});

```
