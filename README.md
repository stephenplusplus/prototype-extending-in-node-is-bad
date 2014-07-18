### Node dependency clashing (Native prototype extending)
> Think twice, please!

###### [https://github.com/stephenplusplus/prototype-extending-in-node-is-bad/blob/master/index.js#L1-2](https://github.com/stephenplusplus/prototype-extending-in-node-is-bad/blob/master/index.js#L1-2):
```js
require('_s');
require('dep');
```

Flipping these two lines will break the app.

*Note: this was just a quick way for me to explain how prototypes can clash in a Node app. If you can extend this example, add an entirely new one, or link me to a great article or example elsewhere, I'll be happy to point this repo to that resource. Thanks!*
