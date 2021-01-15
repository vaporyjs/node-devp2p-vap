# SYNOPSIS 
[![NPM Package](https://img.shields.io/npm/v/merkle-patricia-tree.svg?style=flat-square)](https://www.npmjs.org/package/merkle-patricia-tree)
[![Build Status](https://img.shields.io/travis/vaporyjs/merkle-patricia-tree.svg?branch=master&style=flat-square)](https://travis-ci.org/vaporyjs/merkle-patricia-tree)
[![Coverage Status](https://img.shields.io/coveralls/vaporyjs/merkle-patricia-tree.svg?style=flat-square)](https://coveralls.io/r/vaporyjs/merkle-patricia-tree)
[![Gitter](https://img.shields.io/gitter/room/vapory/vaporyjs-lib.svg?style=flat-square)](https://gitter.im/vapory/vaporyjs-lib) or #vaporyjs on freenode  

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)  

This is an implementation of the modified merkle patricia tree as specified in the [Vapory's yellow paper](http://gavwood.com/Paper.pdf).

> The modified Merkle Patricia tree (trie) provides a persistent data structure to map between arbitrary-length binary data (byte arrays). It is defined in terms of a mutable data structure to map between 256-bit binary fragments and arbitrary-length binary data. The core of the trie, and its sole requirement in terms of the protocol specification is to provide a single 32-byte value that identifies a given set of key-value pairs.   
  \- Vapory's yellow paper  

The only backing store supported is LevelDB through the ```levelup``` module.

# INSTALL
 `npm install merkle-patricia-tree`

# USAGE

## Initialization and Basic Usage

```javascript
var Trie = require('merkle-patricia-tree'),
levelup = require('levelup'),
db = levelup('./testdb'),
trie = new Trie(db); 

trie.put('test', 'one', function () {
  trie.get('test', function (err, value) {
    if(value) console.log(value.toString())
  });
});
```

## Merkle Proofs

```javascript
Trie.prove(trie, 'test', function (err, prove) {
  if (err) return cb(err)
  Trie.verifyProof(trie.root, 'test', prove, function (err, value) {
    if (err) return cb(err)
    console.log(value.toString())
    cb()
  })
})
```

# API
[./docs/](./docs/index.md)

# TESTING
`npm test`

# REFERENCES

- ["Exploring Vapory's state trie with Node.js"](https://wanderer.github.io/vapory/nodejs/code/2014/05/21/using-vaporys-tries-with-node/) blog post
- ["Merkling in Vapory"](https://blog.vapory.org/2015/11/15/merkling-in-vapory/) blog post
- [Vapory Trie Specification](https://github.com/vapory/wiki/wiki/Patricia-Tree) Wiki
- ["Understanding the vapory trie"](https://easythereentropy.wordpress.com/2014/06/04/understanding-the-vapory-trie/) blog post
- ["Trie and Patricia Trie Overview"](https://www.youtube.com/watch?v=jXAHLqQthKw&t=26s) Video Talk on Youtube

# LICENSE
MPL-2.0
