### Node dependency clashing (Native prototype extending)
> Think twice, please!

#### Structure

The dependency tree for this app looks like:

```
test-app@0.0.0
├── _s@2.0.0
└─┬ dep@1.0.0
  └── _s@1.0.0
```

So, in words, our app needs `_s` version 2, but we have a dependency (`_dep`) that needs `_s` version 1.

`_s` is a module that extends a native prototype:

```js
Array.prototype._s = function () { /* ... */ };
```

Between `_s` version 1 and 2, the API has changed. So, what happens when your app `require`s both versions? Nothing good!

To cause an error (and then fix it), [these lines from `index.js`](https://github.com/stephenplusplus/prototype-extending-in-node-is-bad/blob/master/index.js#L1-2) can be re-ordered:
```js
require('_s');
require('dep');
```

#### Reading Material

Here are some articles on the subject:

- [What's wrong with extending the DOM](http://perfectionkills.com/whats-wrong-with-extending-the-dom)
- [Extending builtin natives. Evil or not?](http://perfectionkills.com/extending-native-builtins/)

--
*Note: this was just a quick way for me to explain how prototypes can clash in a Node app. If you can extend this example, add an entirely new one, or link me to a great article or example elsewhere, I'll be happy to point this repo to that resource. Thanks!*
