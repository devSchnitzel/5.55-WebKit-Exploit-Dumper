# fresh-up

> Refreshes NodeJS module when its file is modified

As you know NodeJS caches values returned by ``require`` function. When you call ``require('foo')`` twice or more it returns the same object. **fresh-up** watches and clears the cache (via ``delete require.cache[modulePath]``) when the file of the module is modified. The only argument is an absolute path to the module.

```
npm install --save fresh-up
```

Example:
```js
const freshUp = require('fresh-up');

// require.resolve returns absolute path to ./bar
freshUp(require.resolve('./bar'));

function foo() {
    const bar = require('./bar'); // returns another value only if ./bar is changed
    bar();
}

// foo can be called by any async function
setInterval(() => {
    foo();
}, 500);
```
