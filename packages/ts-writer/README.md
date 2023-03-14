<br />

[![Issues](https://img.shields.io/github/issues/arthurfiorette/tinylibs?logo=github&label=Issues)](https://github.com/arthurfiorette/tinylibs/issues)
[![Stars](https://img.shields.io/github/stars/arthurfiorette/tinylibs?logo=github&label=Stars)](https://github.com/arthurfiorette/tinylibs/stargazers)
[![License](https://img.shields.io/github/license/arthurfiorette/tinylibs?logo=githu&label=License)](https://github.com/arthurfiorette/tinylibs/blob/main/LICENSE)
[![Codecov](https://codecov.io/gh/arthurfiorette/tinylibs/branch/main/graph/badge.svg?token=ML0KGCU0VM)](https://codecov.io/gh/arthurfiorette/tinylibs)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Farthurfiorette%2Ftinylibs.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Farthurfiorette%2Ftinylibs?ref=badge_shield)
[![Join the chat at https://gitter.im/tinylibs-js-org/community](https://badges.gitter.im/tinylibs-js-org/community.svg)](https://gitter.im/tinylibs-js-org/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Speed Blazing](https://img.shields.io/badge/speed-blazing%20%F0%9F%94%A5-brightgreen.svg)](https://twitter.com/acdlite/status/974390255393505280)

[![Latest Version](https://img.shields.io/npm/v/ts-writer)](https://www.npmjs.com/package/ts-writer)
[![Downloads](https://img.shields.io/npm/dw/ts-writer)](https://www.npmjs.com/package/ts-writer)
[![JsDelivr](https://data.jsdelivr.com/v1/package/npm/ts-writer/badge?style=rounded)](https://www.jsdelivr.com/package/npm/ts-writer)
[![Bundlephobia](https://img.shields.io/bundlephobia/minzip/ts-writer/latest?style=flat)](https://bundlephobia.com/package/ts-writer@latest)
[![Packagephobia](https://packagephobia.com/badge?p=ts-writer@latest)](https://packagephobia.com/result?p=ts-writer@latest)

<br />

<div align="center">
  <pre>
  <h1>🖨️<br />TS Writer</h1>
  </pre>
  <br />
</div>

<h3 align="center">
  <code>TS Writer</code> is 1Kb a simple yet powerful typescript source code writer and collector.
  <br />
  <br />
</h3>

<br />

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Installing](#installing)
  - [Node](#node)
  - [Browser](#browser)
  - [Url Import](#url-import)
- [Getting Started](#getting-started)
- [Api](#api)
- [License](#license)

<br />

## Installing

### Node

```sh
npm install ts-writer # or yarn add ts-writer
```

```js
const { TsWriter } = require('ts-writer');
import { TsWriter } from 'ts-writer';
```

### Browser

```html
<script
  crossorigin
  src="https://cdn.jsdelivr.net/npm/ts-writer@latest/dist/index.umd.js"
></script>
```

```js
const { TsWriter } = window.tsWriter;
```

### Url Import

```ts
import { TsWriter } from 'https://cdn.skypack.dev/ts-writer@latest';
```

<br />

## Getting Started

You can use **ts-writer** to generate javascript source code at runtime anywhere in your
code by writing typescript! Simply create an instance of `TsWriter` and use the `write`
method to write anywhere you want, just passing the filename of each piece of code.

```js
import { TsWriter } from 'ts-writer';

const writer = new TsWriter(require.resolve('../tsconfig.json'));

const MyComment = writer.template`${{
  comment: 'this will be a comment'
}} /* ${'comment'} */`;

writer.write`${{
  // first object is the variables to be used in the template, as well the filename
  filename: 'index.ts',
  property: 'hello',
  deep: {
    property: ['ignore', 'world']
  },
  object: {
    a: 1,
    b: '2',
    c: true,
    d: null
  },
  double(a: number) {
    return a * 2;
  },
  myGeneratedClass: class myGeneratedClass {
    constructor() {
      console.log('hello world');
    }
    hello() {
      console.log('hello');
    }
  }
}}

// Type checked and auto-completed!
export const ${'property'} = '${'deep.property.1'}}';

// Json stringifies the object
export const object = ${'object'};

// You can also send classes, functions and etc (they will lose their types)
export function ${'double'};
export class ${'myGeneratedClass'};

// You can map over arrays and pre-parse some code
${MyComment}
${[1, 2, 3].map((item) => writer.template`${{ item }} // ${'item'}`)}
`;

const files = writer.transpile();

files['index.js']; // js code
files['index.ts']; // d.ts code
```

<br />

## Api

- `writer.template` - Simple template function that combines its arguments and the result
  can be used inside `write` and `writeHeader` method.

- `writer.write` - Generates the code to be written in the provided file. The first
  argument is an object with the variables to be used in the template, as well the
  filename. The rest of the arguments are the templates to be written in the file.

- `writer.write` - Generates the code to be written in the **BEGINNING** provided file.
  The first argument is an object with the variables to be used in the template, as well
  the filename. The rest of the arguments are the templates to be written in the file.

- `writer.clear` - Clears all collected source and outputs

- `writer.transpile` - Collects all sources created by `write` and `writeHeader` and
  transpile them to javascript and d.ts files. Returns a `Record<filename, content>`

<br />

## License

Licensed under the **MIT**. See [`LICENSE`](LICENSE) for more informations.

[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Farthurfiorette%2Ftinylibs.svg?type=small)](https://app.fossa.com/projects/git%2Bgithub.com%2Farthurfiorette%2Ftinylibs?ref=badge_small)

<br />