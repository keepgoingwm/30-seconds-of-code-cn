---
title: promisify
tags: function,promise,intermediate
---

Converts an asynchronous function to return a promise.

把一个异步函数转换为返回promise的函数（很适合将Node中回调模式的函数转为promise）。

- Use currying to return a function returning a `Promise` that calls the original function.
- Use the `...rest` operator to pass in all the parameters.
- *In Node 8+, you can use [`util.promisify`](https://nodejs.org/api/util.html#util_util_promisify_original)*

- 使用柯里化来返回一个调用原函数并且返回`Promise`的函数。
- 使用 `...rest` 操作符来传入所有参数。
- *在Node 8+环境，你可以直接使用[`util.promisify`](https://nodejs.org/api/util.html#util_util_promisify_original)*

```js
const promisify = func => (...args) =>
  new Promise((resolve, reject) =>
    func(...args, (err, result) => (err ? reject(err) : resolve(result)))
  );
```

```js
const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(() => console.log('Hi!')); // // Promise resolves after 2s
```
