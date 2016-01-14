httpx
===========
http(s) module with power.

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][codecov-image]][codecov-url]
[![David deps][david-image]][david-url]
[![npm download][download-image]][download-url]

[npm-image]: https://img.shields.io/npm/v/httpx.svg?style=flat-square
[npm-url]: https://npmjs.org/package/httpx
[travis-image]: https://img.shields.io/travis/JacksonTian/httpx.svg?style=flat-square
[travis-url]: https://travis-ci.org/JacksonTian/httpx
[codecov-image]: https://codecov.io/github/JacksonTian/httpx/coverage.svg?branch=master
[codecov-url]: https://codecov.io/github/JacksonTian/httpx?branch=master
[david-image]: https://img.shields.io/david/JacksonTian/httpx.svg?style=flat-square
[david-url]: https://david-dm.org/JacksonTian/httpx
[download-image]: https://img.shields.io/npm/dm/httpx.svg?style=flat-square
[download-url]: https://npmjs.org/package/httpx

## Installation

```bash
$ npm install httpx --save
```

## Usage

```js
'use strict';

var httpx = require('httpx');

httpx.request('http://www.baidu.com/').then((response) => {
  response.pipe(process.stdout);

  response.on('end', () => {
    process.stdout.write('\n');
  });
}, (err) => {
  // on error
});
```

Or `co`.

```js
co(function* () {
  var response = yield httpx.request('http://www.baidu.com/');

  response.pipe(process.stdout);

  response.on('end', () => {
    process.stdout.write('\n');
  });
});
```

Or async/await.

```js
(async function () {
  var response = await httpx.request('http://www.baidu.com/');

  response.pipe(process.stdout);

  response.on('end', () => {
    process.stdout.write('\n');
  });
})();
```

## API

`httpx.request(url[, options])`

- **url** String | Object - The URL to request, either a String or a Object that return by [url.parse](http://nodejs.org/api/url.html#url_url_parse_urlstr_parsequerystring_slashesdenotehost).
- ***options*** Object - Optional
    - ***method*** String - Request method, defaults to `GET`. Could be `GET`, `POST`, `DELETE` or `PUT`.
    - ***data*** String | [Buffer](http://nodejs.org/api/buffer.html) - Manually set the content of payload. If set, `data` will be ignored.
    - ***contentType*** String - Type of request data. Could be `json`. If it's `json`, will auto set `Content-Type: application/json` header.
    - ***headers*** Object - Request headers.
    - ***timeout*** Number - Request timeout in milliseconds. Defaults to `exports.TIMEOUT`. Include remote server connecting timeout and response timeout. When timeout happen, will return `ConnectionTimeout` or `ResponseTimeout`.
    - ***agent*** [http.Agent](http://nodejs.org/api/http.html#http_class_http_agent) - HTTP/HTTPS Agent object.
      Set `false` if you does not use agent.
    - ***beforeRequest*** Function - Before request hook, you can change every thing here.

## License
The MIT license
