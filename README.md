# fill-range [![NPM version](https://img.shields.io/npm/v/fill-range.svg?style=flat)](https://www.npmjs.com/package/fill-range) [![NPM downloads](https://img.shields.io/npm/dm/fill-range.svg?style=flat)](https://npmjs.org/package/fill-range) [![Build Status](https://img.shields.io/travis/jonschlinkert/fill-range.svg?style=flat)](https://travis-ci.org/jonschlinkert/fill-range)

> Fill in a range of numbers or letters, optionally passing an increment or `step` to use, or create a regex-compatible range with `options.toRegex`

## Install

Install with [npm](https://www.npmjs.com/):

```sh
$ npm install --save fill-range
```

## Usage

Expands numbers and letters, optionally using a `step` as the last argument. _(Numbers may be defined as JavaScript numbers or strings)_.

```js
var fill = require('fill-range');

console.log(fill('a', 'e'));
//=> ['a', 'b', 'c', 'd', 'e']

console.log(fill(0, 25, 5));
//=> [ 0, 5, 10, 15, 20, 25 ]

console.log(fill('a', 'e', {toRegex: true}));
//=> '[a-e]'

console.log(fill('a', 'z', 3, {toRegex: true}));
//=> 'a|d|g|j|m|p|s|v|y'

console.log(fill('1', '100', {toRegex: true}));
//=> '[1-9]|[1-9][0-9]|100'
```

Create regex-compatible ranges (returns a string, which can be used however you need to create a regex):

```js
console.log(fill('a', 'e', {toRegex: true}));
//=> '[a-e]'

console.log(fill('a', 'z', 3, {toRegex: true}));
//=> 'a|d|g|j|m|p|s|v|y'

console.log(fill('1', '100', {toRegex: true}));
//=> '[1-9]|[1-9][0-9]|100'
```

**Params**

```js
fill(start, stop, step, options, fn);
```

* `start`: **{String|Number}** the number or letter to start with
* `end`: **{String|Number}** the number or letter to end with
* `step`: **{String|Number}** optionally pass the step to use. works for letters or numbers.
* `options`: **{Object}**:
  - `toRegex`: return a regex-compatible string (still returned as an array for consistency)
  - `step`: pass the step on the options as an alternative to passing it as an argument
  - `strict`: `undefined` by default, set to true to throw errors on invalid ranges.
* `fn`: **{Function}** optionally [pass a function](#custom-function) to modify each character. This can also be defined as `options.transform`

**Examples**

```js
fill(1, 3)
//=> ['1', '2', '3']

fill('1', '3')
//=> ['1', '2', '3']

fill('0', '-5')
//=> [ '0', '-1', '-2', '-3', '-4', '-5' ]

fill(-9, 9, 3)
//=> [ '-9', '-6', '-3', '0', '3', '6', '9' ])

fill('-1', '-10', '-2')
//=> [ '-1', '-3', '-5', '-7', '-9' ]

fill('1', '10', '2')
//=> [ '1', '3', '5', '7', '9' ]

fill('a', 'e')
//=> ['a', 'b', 'c', 'd', 'e']

fill('a', 'e', 2)
//=> ['a', 'c', 'e']

fill('A', 'E', 2)
//=> ['A', 'C', 'E']
```

### Invalid ranges

When an invalid range is passed, `null` is returned.

```js
fill('1.1', '2');   // decimals not supported in ranges
//=> null

fill('a', '2');     // unmatched values
//=> null

fill(1, 10, 'foo'); // invalid step
//=> null
```

If you want errors to be throw, set `options.strict` to true.

### Custom function

Optionally pass a custom function as the third or fourth argument or on `options.transform`.

```js
fill('a', 'e', function (val, isNumber, pad, i) {
  if (!isNumber) {
    return String.fromCharCode(val) + i;
  }
  return val;
});
//=> ['a0', 'b1', 'c2', 'd3', 'e4']
```

## About

### Related projects

* [braces](https://www.npmjs.com/package/braces): Fastest brace expansion for node.js, with the most complete support for the Bash 4.3 braces… [more](https://github.com/jonschlinkert/braces) | [homepage](https://github.com/jonschlinkert/braces "Fastest brace expansion for node.js, with the most complete support for the Bash 4.3 braces specification.")
* [expand-range](https://www.npmjs.com/package/expand-range): Fast, bash-like range expansion. Expand a range of numbers or letters, uppercase or lowercase. See… [more](https://github.com/jonschlinkert/expand-range) | [homepage](https://github.com/jonschlinkert/expand-range "Fast, bash-like range expansion. Expand a range of numbers or letters, uppercase or lowercase. See the benchmarks. Used by micromatch.")
* [micromatch](https://www.npmjs.com/package/micromatch): Glob matching for javascript/node.js. A drop-in replacement and faster alternative to minimatch and multimatch. | [homepage](https://github.com/jonschlinkert/micromatch "Glob matching for javascript/node.js. A drop-in replacement and faster alternative to minimatch and multimatch.")
* [to-regex-range](https://www.npmjs.com/package/to-regex-range): Returns a regex-compatible range from two numbers, min and max, with 855,412 generated unit tests… [more](https://github.com/jonschlinkert/to-regex-range) | [homepage](https://github.com/jonschlinkert/to-regex-range "Returns a regex-compatible range from two numbers, min and max, with 855,412 generated unit tests to validate it's accuracy! Useful for creating regular expressions to validate numbers, ranges, years, etc. Returns a string, allowing the returned value to ")

### Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](../../issues/new).

### Building docs

_(This document was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme) (a [verb](https://github.com/verbose/verb) generator), please don't edit the readme directly. Any changes to the readme must be made in [.verb.md](.verb.md).)_

To generate the readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm install -g verb verb-generate-readme && verb
```

### Running tests

Install dev dependencies:

```sh
$ npm install -d && npm test
```

### Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

### License

Copyright © 2016, [Jon Schlinkert](https://github.com/jonschlinkert).
Released under the [MIT license](https://github.com/jonschlinkert/fill-range/blob/master/LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.1.30, on September 14, 2016._