# requireES

Load [ES Modules](http://www.ecma-international.org/ecma-262/6.0/#sec-modules) in [AMD](https://github.com/amdjs/amdjs-api)-like way in browser.

[rollup.browser.js](https://github.com/rollup/rollup) is required.


## Usage

Import the scripts of `requireES` and `rollup.browser.js`.
```html
<script src="rollup.browser.js"></script>
<script src="requireES.js"></script>
```

Config it in the same way as [AMD config](https://github.com/amdjs/amdjs-api/wiki/Common-Config).
```js
requireES.config({
    baseUrl: '..',
    paths: {
        'echarts': 'dist/echarts',
        'data': 'test/data',
        'extension': 'dist/extension'
    },
    packages: [
        {...}, ...
    ],
    urlArgs: +new Date(),
    sourceMap: true // Enable sourceMap for debugging. `false` by default.
});
```

Load modules.
```js
requireES([
    'xxx/esModuleA',
    'yyy/esModuleB'
], function (moduleA, moduleB) {
    ...
});
```


## Why use it?

We have upgraded the source code of [echarts](https://github.com/ecomfe/echarts) and [zrender](https://github.com/ecomfe/zrender) from AMD to ES Module for tree shaking by [rollup](https://github.com/rollup/rollup). Then we need to run unit tests and examples, where ES modules should be loaded and run in browser, including browsers that do not support ES module yet. ES module loaders like [systemjs](https://github.com/systemjs/systemjs) are better choices for this task in general, but this project is an alternative if you have found that in some situations other ES module loaders are not suitable for your project.


## Caution

+ It just provides AMD-like API, but not an AMD loader. For example, modules are not shared between different calling of `requireES(...)`.

+ Whether import `*` or `default` is determined by the module itself. That is, if the module (like `xxx/SomeClz`) only export `default` , it imports `default`, otherwise (like `xxx/util`) it imports `*`.
