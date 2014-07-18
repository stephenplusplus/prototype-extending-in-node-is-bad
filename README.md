### Node dependency clashing (Native prototype extending)
> Think twice, please!

#### This Example
This is a simple example of how extending a native prototype (`String.prototype.yourMethod`, `Array.prototype.yourMethod`, etc) can not only interfere with other modules that made the same methods, but even with yourself, when an app relies on multiple versions of your module (by way of its dependencies).

#### Structure

The dependency tree for this app looks like:

```
test-app@0.0.0
├── proto-extender@2.0.0
└─┬ dep@1.0.0
  └── proto-extender@1.0.0
```

So, in words, our app needs `proto-extender` version 2, but we have a dependency (`_dep`) that needs `proto-extender` version 1.

`proto-extender` is a module that extends a native prototype:

```js
Array.prototype['proto-extender'] = function () { /* ... */ };
```

Between `proto-extender` version 1 and 2, the API has changed. So, what happens when your app `require`s both versions? Nothing good!

To cause an error (and then fix it), [these lines from `index.js`](https://github.com/stephenplusplus/prototype-extending-in-node-is-bad/blob/master/index.js#L1-2) can be re-ordered:
```js
require('proto-extender');
require('dep');
```

#### Reading Material

- *[Tweet]* [Asking for a friend: Is there a definitive article explaining why modifying prototypes of builtins is a Bad Idea?](https://twitter.com/passy/status/490144973560766464)
- *[Article]* [What's wrong with extending the DOM](http://perfectionkills.com/whats-wrong-with-extending-the-dom)
- *[Article]* [Extending builtin natives. Evil or not?](http://perfectionkills.com/extending-native-builtins/)

--
*Note: this was just a quick way for me to explain how prototypes can clash in a Node app. If you can extend this example, add an entirely new one, or link me to a great article or example elsewhere, I'll be happy to point this repo to that resource. Thanks!*
