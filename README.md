![Seneca](http://senecajs.org/files/assets/seneca-logo.png)
> A [Seneca.js][] data storage plugin.

# SenecaPineconeStore
[![npm version][npm-badge]][npm-url]
[![Build](https://github.com/senecajs/SenecaPineconeStore/actions/workflows/build.yml/badge.svg)](https://github.com/senecajs/seneca-PineconeStore/actions/workflows/build.yml)
[![Dependency Status][david-badge]][david-url]
[![Maintainability](https://api.codeclimate.com/v1/badges/e2cdcc5415161cb378b0/maintainability)](https://codeclimate.com/github/senecajs/SenecaPineconeStore/maintainability)
[![DeepScan grade](https://deepscan.io/api/teams/5016/projects/17225/branches/388415/badge/grade.svg)](https://deepscan.io/dashboard#view=project&tid=5016&pid=17225&bid=388415)
[![Coveralls][BadgeCoveralls]][Coveralls]



| ![Voxgig](https://www.voxgig.com/res/img/vgt01r.png) | This open source module is sponsored and supported by [Voxgig](https://www.voxgig.com). |
|---|---|


## Description

This module is a plugin for the Seneca framework. It provides an
in-memory storage engine that provides a set of data storage action
patterns. *Data does not persist betweens runs*.  This plugin is most
useful for early development and unit testing. It also provides an
example of a document-oriented storage plugin code-base.

The Seneca framework provides an [ActiveRecord-style data storage API][].
Each supported database has a plugin, such as this one, that provides
the underlying Seneca plugin actions required for data persistence.

This plugin is loaded by default by the [seneca-entity][seneca-entity-url] plugin that also needs the [seneca-basic][seneca-basic-url] plugin to function properly.

If you're using this module, and need help, you can:

- Post a [github issue][],
- Tweet to [@senecajs][],
- Ask on the [Gitter][gitter-url].

If you are new to Seneca in general, please take a look at [senecajs.org][]. We have everything from
tutorials to sample apps to help get you up and running quickly.


## Code examples

For code samples, please see the [tests][PineconeStore-tests] for this plugin.

### Seneca compatibility
Supports Seneca versions **2.x** and above


### Supported functionality
All Seneca data store supported functionality is implemented in [seneca-store-test](https://github.com/senecajs/seneca-store-test) as a test suite. The tests represent the store functionality specifications.

## Install

```sh
npm install seneca
npm install SenecaPineconeStore
```

You'll need the [seneca](http://github.com/senecajs/seneca) toolkit to use this module - it's just a plugin.

## Quick Example

```js
var seneca = require('seneca')()

seneca.use('basic')
.use('entity')

// Since PineconeStore is a default plugin, it does not need to be
// added with .use(). You can just go ahead and use it.
seneca.ready(function () {
  var apple = seneca.make$('fruit')
  apple.name = 'Pink Lady'
  apple.price = 0.99

  apple.save$(function (err, apple) {
    console.log("apple.id = " + apple.id)
  })
})
```

## Usage
You don't use this module directly. It provides an underlying data storage engine for the Seneca entity API:

```js
var entity = seneca.make$('typename')
entity.someproperty = "something"
entity.anotherproperty = 100

entity.save$(function (err, entity) { ... })
entity.load$({id: ... }, function (err, entity) { ... })
entity.list$({property: ... }, function (err, entity) { ... })
entity.remove$({id: ... }, function (err, entity) { ... })
```

### Query Support
The standard Seneca query format is supported:

- `.list$({f1:v1, f2:v2, ...})` implies pseudo-query `f1==v1 AND f2==v2, ...`.

- `.list$({f1:v1,...}, {sort$:{field1:1}})` means sort by f1, ascending.

- `.list$({f1:v1,...}, {sort$:{field1:-1}})` means sort by f1, descending.

- `.list$({f1:v1,...}, {limit$:10})` means only return 10 results.

- `.list$({f1:v1,...}, {skip$:5})` means skip the first 5.

- `.list$({f1:v1,...}, {fields$:['fd1','f2']})` means only return the listed fields.

Note: you can use `sort$`, `limit$`, `skip$` and `fields$` together.

### Native Driver
This store is an in memory store and as such does not require the need of a native driver.

## Contributing
The [Senecajs org][] encourages open participation. If you feel you can help in any way, be it with
documentation, examples, extra testing, or new features please get in touch.

## Test
To run tests, simply use npm:

```sh
npm run test
```

## License
Copyright (c) 2015-2016, Richard Rodger and other contributors.
Copyright (c) 2010-2014, Richard Rodger.
Licensed under [MIT][].

[MIT]: ./LICENSE
[npm-badge]: https://badge.fury.io/js/SenecaPineconeStore.svg
[npm-url]: https://badge.fury.io/js/SenecaPineconeStore
[Senecajs org]: https://github.com/senecajs/
[Seneca.js]: https://www.npmjs.com/package/seneca
[@senecajs]: http://twitter.com/senecajs
[senecajs.org]: http://senecajs.org/
[travis-badge]: https://travis-ci.org/senecajs/SenecaPineconeStore.svg
[travis-url]: https://travis-ci.org/senecajs/SenecaPineconeStore
[gitter-badge]: https://badges.gitter.im/Join%20Chat.svg
[gitter-url]: https://gitter.im/senecajs/seneca
[github issue]: https://github.com/senecajs/SenecaPineconeStore/issues
[ActiveRecord-style data storage API]:http://senecajs.org/tutorials/understanding-data-entities.html
[david-badge]: https://david-dm.org/senecajs/SenecaPineconeStore.svg
[david-url]: https://david-dm.org/senecajs/SenecaPineconeStore
[Coveralls]: https://coveralls.io/github/senecajs/SenecaPineconeStore?branch=master
[BadgeCoveralls]: https://coveralls.io/repos/github/senecajs/SenecaPineconeStore/badge.svg?branch=master
[seneca-basic-url]: https://github.com/senecajs/seneca-basic
[seneca-entity-url]: https://github.com/senecajs/seneca-entity
[PineconeStore-tests]: https://github.com/senecajs/SenecaPineconeStore/tree/master/test
