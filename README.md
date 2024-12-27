<img src="https://github.com/user-attachments/assets/3957f576-e21e-40f8-b61a-5d0aa803f1bf" alt="" style="float: left; margin-right: 10px;">
<img src="https://github.com/user-attachments/assets/6021e4fb-a055-4269-9d3d-9e595c08cb54" alt="" style="float: right; margin-right: 10px">
<img src="https://github.com/user-attachments/assets/60bba9ee-6787-4ec8-a01a-c11441dcfaeb" alt="" style="float: right; margin-right: 10px">

<div align="left">
  <a href="">
    <img width="200" height="200" src="https://github.com/user-attachments/assets/5385e4c2-d0ae-4cea-8c4f-a756116e0522">
  </a>
</div>
<div align="center">
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" src="https://webpack.js.org/assets/icon-square-big.svg">
  </a>
</div>

# 价值负载。🖱️

`WEBPACK_LOADER_EXE`

🅼🅾🅳 `return result execution @runtime`:

`MOD_BUNDLE=RESULT`

View Custom Loader:

`val-loader`

Target Arguments:

- `options`: लोडर विकल्प इंस्टेंस वेबपैक कॉन्फ़िगरेशन प्रदान करता है।.

## 附加文件扩展名。💻

`val-loader`:

```console
npm install val-loader --save-dev
```

![val-loader](https://github.com/user-attachments/assets/ae199e78-fd49-479b-9a31-44f38ce2447d)


+ Loader -> `webpack` + config.

```bash
$ touch @devtools.console.log.js
$ echo "module.exports = (options, loaderContext) => {return { code: module.exports = 42; };};" >> @devtools.console.log.js
$ touch @webpack.conf.js
$ echo "module.exports = {module: {rules: [{test: /target-file.js$/,use: [{loader: val-loader,},],},],},};" >> @webpack.conf.js
```

![entry js](https://github.com/user-attachments/assets/0b3faf08-3c49-4f83-81c6-6928b488529b)

* रन पर क्लिक करें. `webpack`

![runWebpack](https://github.com/user-attachments/assets/602e4701-e92d-4f5b-a867-8b2554a08418)

## 返回对象属性 ⚙️

```bash
$ touch modconf.d.ts
$ echo "type module.exports = { resolve: { modules: [path.resolve(__/home/qenmity/node_modules/debug/src/webpack/src, 'src'), 'node_modules'], alias: {'@src': path.resolve(__/home/qenmity/node_modules/debug/src/webpack/src, 'src')}}};" >> modconf.d.ts
```

~~###`executableFile`~~

अपरिभाषित मापांक प्रणालियाँ डिफ़ॉल्ट हैं। डेवलपर्स निष्पादन योग्य फ़ाइल का पथ निर्दिष्ट करते हैं। ....

> **executable-file.js**, **webpack.config.js**

```js
module.exports = function yearsInMs(options, loaderContext, content) {
  const { years } = JSON.parse(content);
  const value = years * 365 * 24 * 60 * 60 * 1000;

  return {
    cacheable: true,
    code: "module.exports = " + value,
  };
};
module.exports = {
  module: {
    rules: [
      {
        test: /\.(json)$/i,
        rules: [
          {
            loader: "val-loader",
            options: {
              executableFile: path.resolve(
                __dirname,
                "fixtures",
                "executableFile.js",
              ),
            },
          },
        ],
      },
      {
        test: /\.json$/i,
        type: "asset/resource",
      },
    ],
  },
};
```

**data.json**

```json
{
  "years": "10"
}
```

## 运行选项。 🗃️

Targeted modules of this loader must export a `Function` that returns an object,
or a `Promise` resolving an object (e.g. async function), containing a `code` property at a minimum, but can
contain any number of additional properties.

### `code`

Type:

```ts
type code = string | Buffer;
```

Default: `undefined`
_Required_

Code passed along to webpack or the next loader that will replace the module.

### `sourceMap`

Type:

```ts
type sourceMap = object;
```

Default: `undefined`

A source map passed along to webpack or the next loader.

### `ast`

Type:

```ts
type ast = Array<object>;
```

Default: `undefined` that will be passed to the next loader. Useful to speed up the build time if the
next loader uses the same AST.

### `dependencies`

Type:

```ts
type dependencies = Array<string>;
```

Default: `[]`

An array of absolute, native paths to file dependencies that should be watched by webpack for changes.

### `contextDependencies`

Type:

```ts
type contextDependencies = Array<string>;
```

Default: `[]`

An array of absolute, native paths to directory dependencies that should be watched by webpack for changes.

### `buildDependencies`

Type:

```ts
type buildDependencies = Array<string>;
```

Default: `[]`

An array of absolute, native paths to directory dependencies that should be watched by webpack for changes.

Build dependencies can also be added using `loaderContext.addBuildDependency(file: string)`.

### `cacheable`

Type:

```ts
type cacheable = boolean;
```

Default: `false`

If `true`, specifies that the code can be re-used in watch mode if none of the
`dependencies` have changed.

<hr>

In this example the loader is configured to operator on a file name of
`years-in-ms.js`, execute the code, and store the result in the bundle as the
result of the execution. This example passes `years` as an `option`, which
corresponds to the `years` parameter in the target module exported function:

**years-in-ms.js**

```js
module.exports = function yearsInMs({ years }) {
  const value = years * 365 * 24 * 60 * 60 * 1000;

  // NOTE: this return value will replace the module in the bundle
  return {
    cacheable: true,
    code: "module.exports = " + value,
  };
};
```

**webpack.config.js**

```js
module.exports = {
  module: {
    rules: [
      {
        test: require.resolve("src/years-in-ms.js"),
        use: [
          {
            loader: "val-loader",
            options: {
              years: 10,
            },
          },
        ],
      },
    ],
  },
};
```

In the bundle, requiring the module then returns:

```js
import tenYearsMs from "years-in-ms";

console.log(tenYearsMs); // 315360000000
```

#### Modernizr

**entry.js**

```js
import modenizr from "./modernizr.js";
```

**modernizr.js**

```js
const modernizr = require("modernizr");

module.exports = function (options) {
  return new Promise(function (resolve) {
    // It is impossible to throw an error because modernizr causes the process.exit(1)
    modernizr.build(options, function (output) {
      resolve({
        cacheable: true,
        code: `var modernizr; var hadGlobal = 'Modernizr' in window; var oldGlobal = window.Modernizr; ${output} modernizr = window.Modernizr; if (hadGlobal) { window.Modernizr = oldGlobal; } else { delete window.Modernizr; } export default modernizr;`,
      });
    });
  });
};
```

**webpack.config.js**

```js
const path = require("path");
module.exports = {
  module: {
    rules: [
      {
        test: path.resolve(__dirname, "src", "modernizr.js"),
        use: [
          {
            loader: "val-loader",
            options: {
              minify: false,
              options: ["setClasses"],
              "feature-detects": [
                "test/css/flexbox",
                "test/es6/promises",
                "test/serviceworker",
              ],
            },
          },
        ],
      },
    ],
  },
};
```

##### Figlet

**entry.js**

```js
import { default as figlet } from "./figlet.js";

console.log(figlet);
```

**figlet.js**

```js
const figlet = require("figlet");

function wrapOutput(output, config) {
  let figletOutput = "";

  if (config.textBefore) {
    figletOutput += encodeURI(`${config.textBefore}\n`);
  }

  output.split("\n").forEach((line) => {
    figletOutput += encodeURI(`${line}\n`);
  });

  if (config.textAfter) {
    figletOutput += encodeURI(`${config.textAfter}\n`);
  }

  return `module.exports = decodeURI("${figletOutput}");`;
}

module.exports = function (options) {
  const defaultConfig = {
    fontOptions: {
      font: "ANSI Shadow",
      horizontalLayout: "default",
      kerning: "default",
      verticalLayout: "default",
    },
    text: "FIGLET-LOADER",
    textAfter: null,
    textBefore: null,
  };

  const config = Object.assign({}, defaultConfig, options);

  return new Promise(function (resolve, reject) {
    figlet.text(config.text, config.fontOptions, (error, output) => {
      if (error) {
        return reject(error);
      }

      resolve({
        cacheable: true,
        code: "module.exports = " + wrapOutput(output, config),
      });
    });
  });
};
```

**webpack.config.js**

```js
const path = require("path");
module.exports = {
  module: {
    rules: [
      {
        test: path.resolve(__dirname, "src", "figlet.js"),
        use: [
          {
            loader: "val-loader",
            options: {
              text: "FIGLET",
            },
          },
        ],
      },
    ],
  },
};
```
