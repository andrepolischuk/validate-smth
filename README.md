# validate-smth [![Build Status][travis-image]][travis-url]

  > Tool for compose validation functions

## Install

```sh
npm install --save validate-smth
```

## Usage

  Sync

```js
var validate = require('validate-smth');

var validateString = validate()
  .use(function (value) {
    return typeof value === 'string';
  }, 'type');

validateString(100); // 'type'
validateString('world'); // null
```

  Async

```js
var validate = require('validate-smth');

var validateString = validate()
  .use(function (value, next) {
    setTimeout(function () {
      next(typeof value === 'string');
    }, 500);
  }, 'type');

validateString(100, function (err) {
  err; // 'type'
});

validateString('world', function (err) {
  err; // null
});
```

  Mix

```js
var validate = require('validate-smth');

var validateString = validate()
  .use(function (value) {
    return typeof value === 'string';
  }, 'type')
  .use(function (value, next) {
    setTimeout(function () {
      next(value.length === 5);
    }, 500);
  }, 'length');

validateString(100, function (err) {
  err; // 'type'
});

validateString('awesome', function (err) {
  err; // 'length'
});

validateString('world', function (err) {
  err; // null
});
```

## License

  MIT

[travis-url]: https://travis-ci.org/andrepolischuk/validate-smth
[travis-image]: https://travis-ci.org/andrepolischuk/validate-smth.svg?branch=master
