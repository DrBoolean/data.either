Monads: Either
==============

[![Build Status](https://secure.travis-ci.org/folktale/monads.either.png?branch=master)](https://travis-ci.org/folktale/monads.either)
[![NPM version](https://badge.fury.io/js/monads.either.png)](http://badge.fury.io/js/monads.either)
[![Dependencies Status](https://david-dm.org/folktale/monads.either.png)](https://david-dm.org/folktale/monads.either)
[![experimental](http://hughsk.github.io/stability-badges/dist/experimental.svg)](http://github.com/hughsk/stability-badges)


The `Either(a, b)` monad represents the logical disjunction between `a` and
`b`. In other words, `Either` may contain either a value of type `a` or a value
of type `b`, at any given time. This particular implementation is biased on the
right value (`b`), thus projections will take the right value over the left
one.

A common use of this monad is to represent computations that may fail, when you
want to provide additional information on the failure. This can force failures
and their handling to be explicit, and avoid the problems associated with
throwing exceptions — non locality, abnormal exits, etc.

Furthermore, being a monad, `Either(a, b)` can be composed in manners similar
to other monads, by using the generic sequencing and composition operations
provided for the common interface in [Fantasy Land][].


## Example

```js
var Either = require('monads.either')

// + type: String -> Either(Error, String)
function read(path) {
  return exists(path)?    Either.Right(readFile(path))
  :      /* otherwise */  Either.Left(new Error(path + ' does not exist.'))
}

var intro = read('intro.json')
var outro = read('outro.json')

intro.map(function(a) {
  outro.map(function(b) {
    console.log(intro + outro)
  }).orElse(logFailure)
}).orElse(logFailure)
```


## Installing

The easiest way is to grab it from NPM. If you're running in a Browser
environment, you can use [Browserify][]

    $ npm install monads.either


### Using with CommonJS

If you're not using NPM, [Download the latest release][release], and require
the `monads.either.umd.js` file:

```js
var Either = require('monads.either')
```


### Using with AMD

[Download the latest release][release], and require the `monads.either.umd.js`
file:

```js
require(['monads.either'], function(Either) {
  ( ... )
})
```


### Using without modules

[Download the latest release][release], and load the `monads.either.umd.js`
file. The properties are exposed in the global `folktale.monads.Either` object:

```html
<script src="/path/to/monads.either.umd.js"></script>
```


### Compiling from source

If you want to compile this library from the source, you'll need [Git][],
[Make][], [Node.js][], and run the following commands:

    $ git clone git://github.com/folktale/monads.either.git
    $ cd monads.either
    $ npm install
    $ make bundle
    
This will generate the `dist/monads.either.umd.js` file, which you can load in
any JavaScript environment.

    
## Documentation

You can [read the documentation online][docs] or build it yourself:

    $ git clone git://github.com/folktale/monads.either.git
    $ cd monads.either
    $ npm install
    $ make documentation

Then open the file `docs/literate/index.html` in your browser.


## Platform support

This library assumes an ES5 environment, but can be easily supported in ES3
platforms by the use of shims. Just include [es5-shim][] :)


## Licence

Copyright (c) 2013 Quildreen Motta.

Released under the [MIT licence](https://github.com/folktale/monads.either/blob/master/LICENCE).

<!-- links -->
[Fantasy Land]: https://github.com/fantasyland/fantasy-land
[Browserify]: http://browserify.org/
[release]: https://github.com/folktale/monads.either/releases/download/v0.2.0/monads.either-0.2.0.tar.gz
[Git]: http://git-scm.com/
[Make]: http://www.gnu.org/software/make/
[Node.js]: http://nodejs.org/
[es5-shim]: https://github.com/kriskowal/es5-shim
[docs]: http://folktale.github.io/monads.either
