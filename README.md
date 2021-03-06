# RAML Generator

[![NPM version][npm-image]][npm-url]
[![NPM downloads][downloads-image]][downloads-url]
[![Build status][travis-image]][travis-url]
[![Test coverage][coveralls-image]][coveralls-url]

Generate files from a RAML document and Handlebars templates.

## Installation

```
npm install raml-generator --save
```

## Usage

The module accepts a map of Handlebars templates, partials and helpers, and exports a function that can be used to generate files from a RAML object and user data. For an example module, take a look at the [raml-javascript-generator](https://github.com/mulesoft-labs/raml-javascript-generator).

### JavaScript Usage

Create the generator function from an object specification. The returned object accepts two parameters, the RAML object and user package information.

```js
var fs = require('fs')
var generator = require('raml-generator')

module.exports = generator({
  templates: {
    'index.js': fs.readFileSync(__dirname + '/templates/index.js.hbs', 'utf8')
  },
  helpers: {
    stringify: require('javascript-stringify')
  }
}) //=> [Function]
```

### Handlebars

Inside the Handlebars templates, the [RAML interface](https://github.com/mulesoft-labs/js-raml-object-interface) is exposed as Handlebars data.

```hbs
var baseUri = {{stringify baseUri}}
```

The user data is automatically provided as the Handlebars compile context.

### Bin Script

A `bin` script is provided for you to use with your custom generator. Just require `raml-generator/bin` and pass in the generator function (from above), package information (`package.json`) and `process.argv`.

```js
#!/usr/bin/env node

var bin = require('raml-generator/bin')

var generator = /* The generator function */

bin(generator, require('./package.json'), process.argv)
```

## License

Apache License 2.0

[npm-image]: https://img.shields.io/npm/v/raml-generator.svg?style=flat
[npm-url]: https://npmjs.org/package/raml-generator
[downloads-image]: https://img.shields.io/npm/dm/raml-generator.svg?style=flat
[downloads-url]: https://npmjs.org/package/raml-generator
[travis-image]: https://img.shields.io/travis/mulesoft-labs/raml-generator.svg?style=flat
[travis-url]: https://travis-ci.org/mulesoft-labs/raml-generator
[coveralls-image]: https://img.shields.io/coveralls/mulesoft-labs/raml-generator.svg?style=flat
[coveralls-url]: https://coveralls.io/r/mulesoft-labs/raml-generator?branch=master
