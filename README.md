# vscode-nls


CommonJS module to support externalization and localization. The module only depends on Node.js however its
primary use case is for VSCode extensions.

[![Build Status](https://travis-ci.org/Microsoft/vscode-nls.svg?branch=master)](https://travis-ci.org/Microsoft/vscode-nls)
[![NPM Version](https://img.shields.io/npm/v/vscode-nls.svg)](https://npmjs.org/package/vscode-nls)
[![NPM Downloads](https://img.shields.io/npm/dm/vscode-nls.svg)](https://npmjs.org/package/vscode-nls)

## Usage

```typescript
import * as nls from 'vscode-nls';

let localize = nls.config({ locale: 'de-DE' })();

console.log(localize('keyOne', "Hello World"));
console.log(localize('keyTwo', "Current Date {0}", Date.now()));
```

The `config` call configures the nls module and should only be called once in the applications entry point. You pass in the locale you want to use and whether the resolved locale should be cached for all further calls. The config call returns a function which is used to load a message bundle. During development time the argument should stay empty. There is another tool that helps extracting the message from you sources and create the message bundles autmatically for you. The tools is available [here]().

In secondary modules loaded from the 'main' module no configuration is necessary. However you still need to load the nls module and load the message bundle. This looks like this:

```typescript
import * as nls from 'vscode-nls';

let localize = nls.loadMessageBundle();

console.log(localize('keyOne', "Hello World"));
```

During development time the strings in the code are presented to the user. If the locale is set to 'pseudo' the messages are modified in the following form:

* vowels are doubled
* the string is prefixed with '\uFF3B' (Unicode zenkaku representation for [) and postfixed with '\uFF3D' (Unicode zenkaku representation for ])