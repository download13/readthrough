# Readthrough
Node.js read-through cache implementation, to be used with any cache engine.

![](https://travis-ci.org/kodjevlar/readthrough.svg?branch=master)

## Installation
`npm install readthrough --save`

## Usage

### Setup
```js
const Cache = require('readthrough');

Cache.setup({
  read: function(key) {
    // Your implementation of reading from cache here...
    return Promise.resolve(undefined); // Return undefined on cache misses
  },
  write: function(key, data, ttl) {
    // Your implementation of writing to cache here...
    return Promise.resolve(); // Return promise indicating write result
  },
  enabled: true // Whether or not to enable the readthrough 
});
```

### Readthrough

API:<br/>
`readthrough(entity, identifier, ttl, callback)`

Where `entity` is the name of the entity to get. `identifier` is an object that
identifies the specific entity. `entity` and `identifier` is used to create
the cache key.

`ttl` is the time-to-live value for the entry. `callback` will be executed on
cache misses. Your DB (or whatever) calls goes here.

```js
Cache.readthrough('customer', { id: 1 }, 3600, function() {
  return Promise.resolve({
    name: 'Test',
    email: 'test@test.com'
  });
});
```

