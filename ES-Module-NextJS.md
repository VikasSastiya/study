* *   Node.js v24.5.0
*  *    [Table of contents](https://nodejs.org/api/esm.html#toc-picker) 
* *    [Index](https://nodejs.org/api/esm.html#gtoc-picker) 
* *    [Other versions](https://nodejs.org/api/esm.html#alt-docs) 
* *    [Options](https://nodejs.org/api/esm.html#options-picker)

* * *

Table of contents* *   [Modules: ECMAScript modules](https://nodejs.org/api/esm.html#modules-ecmascript-modules)* *   [Introduction](https://nodejs.org/api/esm.html#introduction)
*     * *   [Enabling](https://nodejs.org/api/esm.html#enabling)
*     * *   [Packages](https://nodejs.org/api/esm.html#packages)
*     * *   [`import` Specifiers](https://nodejs.org/api/esm.html#import-specifiers)* *   [Terminology](https://nodejs.org/api/esm.html#terminology)
*     *     * *   [Mandatory file extensions](https://nodejs.org/api/esm.html#mandatory-file-extensions)
*     *     * *   [URLs](https://nodejs.org/api/esm.html#urls)* *   [`file:` URLs](https://nodejs.org/api/esm.html#file-urls)
*     *     *     * *   [`data:` imports](https://nodejs.org/api/esm.html#data-imports)
*     *     *     * *   [`node:` imports](https://nodejs.org/api/esm.html#node-imports)
*     * *   [Import attributes](https://nodejs.org/api/esm.html#import-attributes)
*     * *   [Built-in modules](https://nodejs.org/api/esm.html#built-in-modules)
*     * *   [`import()` expressions](https://nodejs.org/api/esm.html#import-expressions)
*     * *   [`import.meta`](https://nodejs.org/api/esm.html#importmeta)* *   [`import.meta.dirname`](https://nodejs.org/api/esm.html#importmetadirname)
*     *     * *   [`import.meta.filename`](https://nodejs.org/api/esm.html#importmetafilename)
*     *     * *   [`import.meta.url`](https://nodejs.org/api/esm.html#importmetaurl)
*     *     * *   [`import.meta.main`](https://nodejs.org/api/esm.html#importmetamain)
*     *     * *   [`import.meta.resolve(specifier)`](https://nodejs.org/api/esm.html#importmetaresolvespecifier)
*     * *   [Interoperability with CommonJS](https://nodejs.org/api/esm.html#interoperability-with-commonjs)* *   [`import` statements](https://nodejs.org/api/esm.html#import-statements)
*     *     * *   [`require`](https://nodejs.org/api/esm.html#require)
*     *     * *   [CommonJS Namespaces](https://nodejs.org/api/esm.html#commonjs-namespaces)
*     *     * *   [Differences between ES modules and CommonJS](https://nodejs.org/api/esm.html#differences-between-es-modules-and-commonjs)* *   [No `require`, `exports`, or `module.exports`](https://nodejs.org/api/esm.html#no-require-exports-or-moduleexports)
*     *     *     * *   [No `__filename` or `__dirname`](https://nodejs.org/api/esm.html#no-__filename-or-__dirname)
*     *     *     * *   [No Addon Loading](https://nodejs.org/api/esm.html#no-addon-loading)
*     *     *     * *   [No `require.main`](https://nodejs.org/api/esm.html#no-requiremain)
*     *     *     * *   [No `require.resolve`](https://nodejs.org/api/esm.html#no-requireresolve)
*     *     *     * *   [No `NODE_PATH`](https://nodejs.org/api/esm.html#no-node_path)
*     *     *     * *   [No `require.extensions`](https://nodejs.org/api/esm.html#no-requireextensions)
*     *     *     * *   [No `require.cache`](https://nodejs.org/api/esm.html#no-requirecache)
*     * *   [JSON modules](https://nodejs.org/api/esm.html#json-modules)
*     * *   [Wasm modules](https://nodejs.org/api/esm.html#wasm-modules)* *   [Wasm Source Phase Imports](https://nodejs.org/api/esm.html#wasm-source-phase-imports)
*     *     * *   [JavaScript String Builtins](https://nodejs.org/api/esm.html#javascript-string-builtins)
*     *     * *   [Wasm Instance Phase Imports](https://nodejs.org/api/esm.html#wasm-instance-phase-imports)
*     *     * *   [Reserved Wasm Namespaces](https://nodejs.org/api/esm.html#reserved-wasm-namespaces)
*     * *   [Top-level `await`](https://nodejs.org/api/esm.html#top-level-await)
*     * *   [Loaders](https://nodejs.org/api/esm.html#loaders)
*     * *   [Resolution and loading algorithm](https://nodejs.org/api/esm.html#resolution-and-loading-algorithm)* *   [Features](https://nodejs.org/api/esm.html#features)
*     *     * *   [Resolution algorithm](https://nodejs.org/api/esm.html#resolution-algorithm)
*     *     * *   [Resolution Algorithm Specification](https://nodejs.org/api/esm.html#resolution-algorithm-specification)
*     *     * *   [Customizing ESM specifier resolution algorithm](https://nodejs.org/api/esm.html#customizing-esm-specifier-resolution-algorithm)

## Modules: ECMAScript modules[#](https://nodejs.org/api/esm.html#modules-ecmascript-modules)

History

[Stability: 2](https://nodejs.org/api/documentation.html#stability-index) \- Stable

### Introduction[#](https://nodejs.org/api/esm.html#introduction)

ECMAScript modules are [the official standard format](https://tc39.github.io/ecma262/#sec-modules) to package JavaScript code for reuse. Modules are defined using a variety of [`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) and [`export`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) statements.

The following example of an ES module exports a function:

```js
// addTwo.mjs
function addTwo(num) {
  return num + 2;
}

export { addTwo };
```

The following example of an ES module imports the function from `addTwo.mjs`:

```js
// app.mjs
import { addTwo } from './addTwo.mjs';

// Prints: 6
console.log(addTwo(4));
```

Node.js fully supports ECMAScript modules as they are currently specified and provides interoperability between them and its original module format, [CommonJS](https://nodejs.org/api/modules.html).

### Enabling[#](https://nodejs.org/api/esm.html#enabling)

Node.js has two module systems: [CommonJS](https://nodejs.org/api/modules.html) modules and ECMAScript modules.

Authors can tell Node.js to interpret JavaScript as an ES module via the `.mjs` file extension, the `package.json` [`"type"`](https://nodejs.org/api/packages.html#type) field with a value `"module"`, or the [`--input-type`](https://nodejs.org/api/cli.html#--input-typetype) flag with a value of `"module"`. These are explicit markers of code being intended to run as an ES module.

Inversely, authors can explicitly tell Node.js to interpret JavaScript as CommonJS via the `.cjs` file extension, the `package.json` [`"type"`](https://nodejs.org/api/packages.html#type) field with a value `"commonjs"`, or the [`--input-type`](https://nodejs.org/api/cli.html#--input-typetype) flag with a value of `"commonjs"`.

When code lacks explicit markers for either module system, Node.js will inspect the source code of a module to look for ES module syntax. If such syntax is found, Node.js will run the code as an ES module; otherwise it will run the module as CommonJS. See [Determining module system](https://nodejs.org/api/packages.html#determining-module-system) for more details.

### Packages[#](https://nodejs.org/api/esm.html#packages)

This section was moved to [Modules: Packages](https://nodejs.org/api/packages.html).

### `import` Specifiers[#](https://nodejs.org/api/esm.html#import-specifiers)

#### Terminology[#](https://nodejs.org/api/esm.html#terminology)

The _specifier_ of an `import` statement is the string after the `from` keyword, e.g. `'node:path'` in `import { sep } from 'node:path'`. Specifiers are also used in `export from` statements, and as the argument to an `import()` expression.

There are three types of specifiers:

* *   _Relative specifiers_ like `'./startup.js'` or `'../config.mjs'`. They refer to a path relative to the location of the importing file. _The file extension is always necessary for these._
*     
* *   _Bare specifiers_ like `'some-package'` or `'some-package/shuffle'`. They can refer to the main entry point of a package by the package name, or a specific feature module within a package prefixed by the package name as per the examples respectively. _Including the file extension is only necessary for packages without an [`"exports"`](https://nodejs.org/api/packages.html#exports) field._
*     
* *   _Absolute specifiers_ like `'file:///opt/nodejs/config.js'`. They refer directly and explicitly to a full path.
*     

Bare specifier resolutions are handled by the [Node.js module resolution and loading algorithm](https://nodejs.org/api/esm.html#resolution-algorithm-specification). All other specifier resolutions are always only resolved with the standard relative [URL](https://url.spec.whatwg.org/) resolution semantics.

Like in CommonJS, module files within packages can be accessed by appending a path to the package name unless the package's [`package.json`](https://nodejs.org/api/packages.html#nodejs-packagejson-field-definitions) contains an [`"exports"`](https://nodejs.org/api/packages.html#exports) field, in which case files within packages can only be accessed via the paths defined in [`"exports"`](https://nodejs.org/api/packages.html#exports).

For details on these package resolution rules that apply to bare specifiers in the Node.js module resolution, see the [packages documentation](https://nodejs.org/api/packages.html).

#### Mandatory file extensions[#](https://nodejs.org/api/esm.html#mandatory-file-extensions)

A file extension must be provided when using the `import` keyword to resolve relative or absolute specifiers. Directory indexes (e.g. `'./startup/index.js'`) must also be fully specified.

This behavior matches how `import` behaves in browser environments, assuming a typically configured server.

#### URLs[#](https://nodejs.org/api/esm.html#urls)

ES modules are resolved and cached as URLs. This means that special characters must be [percent-encoded](https://nodejs.org/api/url.html#percent-encoding-in-urls), such as `#` with `%23` and `?` with `%3F`.

`file:`, `node:`, and `data:` URL schemes are supported. A specifier like `'https://example.com/app.js'` is not supported natively in Node.js unless using a [custom HTTPS loader](https://nodejs.org/api/module.html#import-from-https).

##### `file:` URLs[#](https://nodejs.org/api/esm.html#file-urls)

Modules are loaded multiple times if the `import` specifier used to resolve them has a different query or fragment.

```js
import './foo.mjs?query=1'; // loads ./foo.mjs with query of "?query=1"
import './foo.mjs?query=2'; // loads ./foo.mjs with query of "?query=2"
```

The volume root may be referenced via `/`, `//`, or `file:///`. Given the differences between [URL](https://url.spec.whatwg.org/) and path resolution (such as percent encoding details), it is recommended to use [url.pathToFileURL](https://nodejs.org/api/url.html#urlpathtofileurlpath-options) when importing a path.

##### `data:` imports[#](https://nodejs.org/api/esm.html#data-imports)

Added in: v12.10.0

[`data:` URLs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) are supported for importing with the following MIME types:

* *   `text/javascript` for ES modules
* *   `application/json` for JSON
* *   `application/wasm` for Wasm

```js
import 'data:text/javascript,console.log("hello!");';
import _ from 'data:application/json,"world!"' with { type: 'json' };
```

`data:` URLs only resolve [bare specifiers](https://nodejs.org/api/esm.html#terminology) for builtin modules and [absolute specifiers](https://nodejs.org/api/esm.html#terminology). Resolving [relative specifiers](https://nodejs.org/api/esm.html#terminology) does not work because `data:` is not a [special scheme](https://url.spec.whatwg.org/#special-scheme). For example, attempting to load `./foo` from `data:text/javascript,import "./foo";` fails to resolve because there is no concept of relative resolution for `data:` URLs.

##### `node:` imports[#](https://nodejs.org/api/esm.html#node-imports)

History

`node:` URLs are supported as an alternative means to load Node.js builtin modules. This URL scheme allows for builtin modules to be referenced by valid absolute URL strings.

```js
import fs from 'node:fs/promises';
```

### Import attributes[#](https://nodejs.org/api/esm.html#import-attributes)

History

[Import attributes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import/with) are an inline syntax for module import statements to pass on more information alongside the module specifier.

```js
import fooData from './foo.json' with { type: 'json' };

const { default: barData } =
  await import('./bar.json', { with: { type: 'json' } });
```

Node.js only supports the `type` attribute, for which it supports the following values:

Attribute `type`

Needed for

`'json'`

[JSON modules](https://nodejs.org/api/esm.html#json-modules)

The `type: 'json'` attribute is mandatory when importing JSON modules.

### Built-in modules[#](https://nodejs.org/api/esm.html#built-in-modules)

[Built-in modules](https://nodejs.org/api/modules.html#built-in-modules) provide named exports of their public API. A default export is also provided which is the value of the CommonJS exports. The default export can be used for, among other things, modifying the named exports. Named exports of built-in modules are updated only by calling [`module.syncBuiltinESMExports()`](https://nodejs.org/api/module.html#modulesyncbuiltinesmexports).

```js
import EventEmitter from 'node:events';
const e = new EventEmitter();
```

```js
import { readFile } from 'node:fs';
readFile('./foo.txt', (err, source) => {
  if (err) {
    console.error(err);
  } else {
    console.log(source);
  }
});
```

```js
import fs, { readFileSync } from 'node:fs';
import { syncBuiltinESMExports } from 'node:module';
import { Buffer } from 'node:buffer';

fs.readFileSync = () => Buffer.from('Hello, ESM');
syncBuiltinESMExports();

fs.readFileSync === readFileSync;
```

### `import()` expressions[#](https://nodejs.org/api/esm.html#import-expressions)

[Dynamic `import()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) is supported in both CommonJS and ES modules. In CommonJS modules it can be used to load ES modules.

### `import.meta`[#](https://nodejs.org/api/esm.html#importmeta)

* *   Type: [<Object>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

The `import.meta` meta property is an `Object` that contains the following properties. It is only supported in ES modules.

#### `import.meta.dirname`[#](https://nodejs.org/api/esm.html#importmetadirname)

History

* *   Type: [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The directory name of the current module.

This is the same as the [`path.dirname()`](https://nodejs.org/api/path.html#pathdirnamepath) of the [`import.meta.filename`](https://nodejs.org/api/esm.html#importmetafilename).

> **Caveat**: only present on `file:` modules.

#### `import.meta.filename`[#](https://nodejs.org/api/esm.html#importmetafilename)

History

* *   Type: [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The full absolute path and filename of the current module, with symlinks resolved.

This is the same as the [`url.fileURLToPath()`](https://nodejs.org/api/url.html#urlfileurltopathurl-options) of the [`import.meta.url`](https://nodejs.org/api/esm.html#importmetaurl).

> **Caveat** only local modules support this property. Modules not using the `file:` protocol will not provide it.

#### `import.meta.url`[#](https://nodejs.org/api/esm.html#importmetaurl)

* *   Type: [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The absolute `file:` URL of the module.

This is defined exactly the same as it is in browsers providing the URL of the current module file.

This enables useful patterns such as relative file loading:

```js
import { readFileSync } from 'node:fs';
const buffer = readFileSync(new URL('./data.proto', import.meta.url));
```

#### `import.meta.main`[#](https://nodejs.org/api/esm.html#importmetamain)

Added in: v24.2.0

[Stability: 1.0](https://nodejs.org/api/documentation.html#stability-index) \- Early development

* *   Type: [<boolean>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) `true` when the current module is the entry point of the current process; `false` otherwise.

Equivalent to `require.main === module` in CommonJS.

Analogous to Python's `__name__ == "__main__"`.

```js
export function foo() {
  return 'Hello, world';
}

function main() {
  const message = foo();
  console.log(message);
}

if (import.meta.main) main();
// `foo` can be imported from another module without possible side-effects from `main`
```

#### `import.meta.resolve(specifier)`[#](https://nodejs.org/api/esm.html#importmetaresolvespecifier)

History

[Stability: 1.2](https://nodejs.org/api/documentation.html#stability-index) \- Release candidate

* *   `specifier` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The module specifier to resolve relative to the current module.
* *   Returns: [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The absolute URL string that the specifier would resolve to.

[`import.meta.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import.meta/resolve) is a module-relative resolution function scoped to each module, returning the URL string.

```js
const dependencyAsset = import.meta.resolve('component-lib/asset.css');
// file:///app/node_modules/component-lib/asset.css
import.meta.resolve('./dep.js');
// file:///app/dep.js
```

All features of the Node.js module resolution are supported. Dependency resolutions are subject to the permitted exports resolutions within the package.

**Caveats**:

* *   This can result in synchronous file-system operations, which can impact performance similarly to `require.resolve`.
* *   This feature is not available within custom loaders (it would create a deadlock).

**Non-standard API**:

When using the `--experimental-import-meta-resolve` flag, that function accepts a second argument:

* *   `parent` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [<URL>](https://nodejs.org/api/url.html#the-whatwg-url-api) An optional absolute parent module URL to resolve from. **Default:** `import.meta.url`

### Interoperability with CommonJS[#](https://nodejs.org/api/esm.html#interoperability-with-commonjs)

#### `import` statements[#](https://nodejs.org/api/esm.html#import-statements)

An `import` statement can reference an ES module or a CommonJS module. `import` statements are permitted only in ES modules, but dynamic [`import()`](https://nodejs.org/api/esm.html#import-expressions) expressions are supported in CommonJS for loading ES modules.

When importing [CommonJS modules](https://nodejs.org/api/esm.html#commonjs-namespaces), the `module.exports` object is provided as the default export. Named exports may be available, provided by static analysis as a convenience for better ecosystem compatibility.

#### `require`[#](https://nodejs.org/api/esm.html#require)

The CommonJS module `require` currently only supports loading synchronous ES modules (that is, ES modules that do not use top-level `await`).

See [Loading ECMAScript modules using `require()`](https://nodejs.org/api/modules.html#loading-ecmascript-modules-using-require) for details.

#### CommonJS Namespaces[#](https://nodejs.org/api/esm.html#commonjs-namespaces)

History

CommonJS modules consist of a `module.exports` object which can be of any type.

To support this, when importing CommonJS from an ECMAScript module, a namespace wrapper for the CommonJS module is constructed, which always provides a `default` export key pointing to the CommonJS `module.exports` value.

In addition, a heuristic static analysis is performed against the source text of the CommonJS module to get a best-effort static list of exports to provide on the namespace from values on `module.exports`. This is necessary since these namespaces must be constructed prior to the evaluation of the CJS module.

These CommonJS namespace objects also provide the `default` export as a `'module.exports'` named export, in order to unambiguously indicate that their representation in CommonJS uses this value, and not the namespace value. This mirrors the semantics of the handling of the `'module.exports'` export name in [`require(esm)`](https://nodejs.org/api/modules.html#loading-ecmascript-modules-using-require) interop support.

When importing a CommonJS module, it can be reliably imported using the ES module default import or its corresponding sugar syntax:

```js
import { default as cjs } from 'cjs';
// Identical to the above
import cjsSugar from 'cjs';

console.log(cjs);
console.log(cjs === cjsSugar);
// Prints:
//   <module.exports>
//   true
```

This Module Namespace Exotic Object can be directly observed either when using `import * as m from 'cjs'` or a dynamic import:

```js
import * as m from 'cjs';
console.log(m);
console.log(m === await import('cjs'));
// Prints:
//   [Module] { default: <module.exports>, 'module.exports': <module.exports> }
//   true
```

For better compatibility with existing usage in the JS ecosystem, Node.js in addition attempts to determine the CommonJS named exports of every imported CommonJS module to provide them as separate ES module exports using a static analysis process.

For example, consider a CommonJS module written:

```js
// cjs.cjs
exports.name = 'exported';
```

The preceding module supports named imports in ES modules:

```js
import { name } from './cjs.cjs';
console.log(name);
// Prints: 'exported'

import cjs from './cjs.cjs';
console.log(cjs);
// Prints: { name: 'exported' }

import * as m from './cjs.cjs';
console.log(m);
// Prints:
//   [Module] {
//     default: { name: 'exported' },
//     'module.exports': { name: 'exported' },
//     name: 'exported'
//   }
```

As can be seen from the last example of the Module Namespace Exotic Object being logged, the `name` export is copied off of the `module.exports` object and set directly on the ES module namespace when the module is imported.

Live binding updates or new exports added to `module.exports` are not detected for these named exports.

The detection of named exports is based on common syntax patterns but does not always correctly detect named exports. In these cases, using the default import form described above can be a better option.

Named exports detection covers many common export patterns, reexport patterns and build tool and transpiler outputs. See [cjs-module-lexer](https://github.com/nodejs/cjs-module-lexer/tree/2.0.0) for the exact semantics implemented.

#### Differences between ES modules and CommonJS[#](https://nodejs.org/api/esm.html#differences-between-es-modules-and-commonjs)

##### No `require`, `exports`, or `module.exports`[#](https://nodejs.org/api/esm.html#no-require-exports-or-moduleexports)

In most cases, the ES module `import` can be used to load CommonJS modules.

If needed, a `require` function can be constructed within an ES module using [`module.createRequire()`](https://nodejs.org/api/module.html#modulecreaterequirefilename).

##### No `__filename` or `__dirname`[#](https://nodejs.org/api/esm.html#no-__filename-or-__dirname)

These CommonJS variables are not available in ES modules.

`__filename` and `__dirname` use cases can be replicated via [`import.meta.filename`](https://nodejs.org/api/esm.html#importmetafilename) and [`import.meta.dirname`](https://nodejs.org/api/esm.html#importmetadirname).

##### No Addon Loading[#](https://nodejs.org/api/esm.html#no-addon-loading)

[Addons](https://nodejs.org/api/addons.html) are not currently supported with ES module imports.

They can instead be loaded with [`module.createRequire()`](https://nodejs.org/api/module.html#modulecreaterequirefilename) or [`process.dlopen`](https://nodejs.org/api/process.html#processdlopenmodule-filename-flags).

##### No `require.main`[#](https://nodejs.org/api/esm.html#no-requiremain)

To replace `require.main === module`, there is the [`import.meta.main`](https://nodejs.org/api/esm.html#importmetamain) API.

##### No `require.resolve`[#](https://nodejs.org/api/esm.html#no-requireresolve)

Relative resolution can be handled via `new URL('./local', import.meta.url)`.

For a complete `require.resolve` replacement, there is the [import.meta.resolve](https://nodejs.org/api/esm.html#importmetaresolvespecifier) API.

Alternatively `module.createRequire()` can be used.

##### No `NODE_PATH`[#](https://nodejs.org/api/esm.html#no-node_path)

`NODE_PATH` is not part of resolving `import` specifiers. Please use symlinks if this behavior is desired.

##### No `require.extensions`[#](https://nodejs.org/api/esm.html#no-requireextensions)

`require.extensions` is not used by `import`. Module customization hooks can provide a replacement.

##### No `require.cache`[#](https://nodejs.org/api/esm.html#no-requirecache)

`require.cache` is not used by `import` as the ES module loader has its own separate cache.

### JSON modules[#](https://nodejs.org/api/esm.html#json-modules)

History

JSON files can be referenced by `import`:

```js
import packageConfig from './package.json' with { type: 'json' };
```

The `with { type: 'json' }` syntax is mandatory; see [Import Attributes](https://nodejs.org/api/esm.html#import-attributes).

The imported JSON only exposes a `default` export. There is no support for named exports. A cache entry is created in the CommonJS cache to avoid duplication. The same object is returned in CommonJS if the JSON module has already been imported from the same path.

### Wasm modules[#](https://nodejs.org/api/esm.html#wasm-modules)

History

Importing both WebAssembly module instances and WebAssembly source phase imports is supported.

Both of these integrations are in line with the [ES Module Integration Proposal for WebAssembly](https://github.com/webassembly/esm-integration).

#### Wasm Source Phase Imports[#](https://nodejs.org/api/esm.html#wasm-source-phase-imports)

[Stability: 1.2](https://nodejs.org/api/documentation.html#stability-index) \- Release candidate

Added in: v24.0.0

The [Source Phase Imports](https://github.com/tc39/proposal-source-phase-imports) proposal allows the `import source` keyword combination to import a `WebAssembly.Module` object directly, instead of getting a module instance already instantiated with its dependencies.

This is useful when needing custom instantiations for Wasm, while still resolving and loading it through the ES module integration.

For example, to create multiple instances of a module, or to pass custom imports into a new instance of `library.wasm`:

```js
import source libraryModule from './library.wasm';

const instance1 = await WebAssembly.instantiate(libraryModule, importObject1);

const instance2 = await WebAssembly.instantiate(libraryModule, importObject2);
```

In addition to the static source phase, there is also a dynamic variant of the source phase via the `import.source` dynamic phase import syntax:

```js
const dynamicLibrary = await import.source('./library.wasm');

const instance = await WebAssembly.instantiate(dynamicLibrary, importObject);
```

#### JavaScript String Builtins[#](https://nodejs.org/api/esm.html#javascript-string-builtins)

[Stability: 1.2](https://nodejs.org/api/documentation.html#stability-index) \- Release candidate

Added in: v24.5.0

When importing WebAssembly modules, the [WebAssembly JS String Builtins Proposal](https://github.com/WebAssembly/js-string-builtins) is automatically enabled through the ESM Integration. This allows WebAssembly modules to directly use efficient compile-time string builtins from the `wasm:js-string` namespace.

For example, the following Wasm module exports a string `getLength` function using the `wasm:js-string` `length` builtin:

```text
(module
  ;; Compile-time import of the string length builtin.
  (import "wasm:js-string" "length" (func $string_length (param externref) (result i32)))

  ;; Define getLength, taking a JS value parameter assumed to be a string,
  ;; calling string length on it and returning the result.
  (func $getLength (param $str externref) (result i32)
    local.get $str
    call $string_length
  )

  ;; Export the getLength function.
  (export "getLength" (func $get_length))
)
```

```js
import { getLength } from './string-len.wasm';
getLength('foo'); // Returns 3.
```

Wasm builtins are compile-time imports that are linked during module compilation rather than during instantiation. They do not behave like normal module graph imports and they cannot be inspected via `WebAssembly.Module.imports(mod)` or virtualized unless recompiling the module using the direct `WebAssembly.compile` API with string builtins disabled.

Importing a module in the source phase before it has been instantiated will also use the compile-time builtins automatically:

```js
import source mod from './string-len.wasm';
const { exports: { getLength } } = await WebAssembly.instantiate(mod, {});
getLength('foo'); // Also returns 3.
```

#### Wasm Instance Phase Imports[#](https://nodejs.org/api/esm.html#wasm-instance-phase-imports)

[Stability: 1.1](https://nodejs.org/api/documentation.html#stability-index) \- Active development

Instance imports allow any `.wasm` files to be imported as normal modules, supporting their module imports in turn.

For example, an `index.js` containing:

```js
import * as M from './library.wasm';
console.log(M);
```

executed under:

```bash
node index.mjs
```

would provide the exports interface for the instantiation of `library.wasm`.

#### Reserved Wasm Namespaces[#](https://nodejs.org/api/esm.html#reserved-wasm-namespaces)

Added in: v24.5.0

When importing WebAssembly module instances, they cannot use import module names or import/export names that start with reserved prefixes:

* *   `wasm-js:` \- reserved in all module import names, module names and export names.
* *   `wasm:` \- reserved in module import names and export names (imported module names are allowed in order to support future builtin polyfills).

Importing a module using the above reserved names will throw a `WebAssembly.LinkError`.

### Top-level `await`[#](https://nodejs.org/api/esm.html#top-level-await)

Added in: v14.8.0

The `await` keyword may be used in the top level body of an ECMAScript module.

Assuming an `a.mjs` with

```js
export const five = await Promise.resolve(5);
```

And a `b.mjs` with

```js
import { five } from './a.mjs';

console.log(five); // Logs `5`
```

```bash
node b.mjs # works
```

If a top level `await` expression never resolves, the `node` process will exit with a `13` [status code](https://nodejs.org/api/process.html#exit-codes).

```js
import { spawn } from 'node:child_process';
import { execPath } from 'node:process';

spawn(execPath, [
  '--input-type=module',
  '--eval',
  // Never-resolving Promise:
  'await new Promise(() => {})',
]).once('exit', (code) => {
  console.log(code); // Logs `13`
});
