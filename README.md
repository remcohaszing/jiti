# jiti

[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![bundle][bundle-src]][bundle-href]
[![License][license-src]][license-href]

Just-in-Time Typescript and ESM support for Node.js.

> [!IMPORTANT]
> This is the development branch for jiti v2. Check out [jiti/v1](https://github.com/unjs/jiti/tree/v1) for latest stable docs and [unjs/jiti#174](https://github.com/unjs/jiti/issues/174) for the v2 roadmap.

## Features

- Seamless typescript and ESM syntax support
- Seamless interoperability between ESM and CommonJS
- Synchronous API to replace `require()`
- Asynchronous API to replace `import()`
- Super slim and zero dependency
- Smart syntax detection to avoid extra transforms
- Node.js native require cache integration
- Filesystem transpile with hard disk caches
- Custom resolve aliases

## Used by

- [Nitro](https://nitro.unjs.io/) and [UnJS](https://unjs.io/) ecosystem
- [Nuxt](https://nuxt.com/)
- [Docusaurus](https://docusaurus.io/)
- [UnoCSS](https://unocss.dev/)
- [Tailwindcss 3.x](https://tailwindcss.com/)
- [PostCSS loader](https://github.com/webpack-contrib/postcss-loader)
- [Slidev](https://sli.dev/)
- [FormKit](https://formkit.com/)
- [Knip](https://knip.dev/)
- [Histoire](https://histoire.dev/)
- [...55M+ npm monthly downloads](https://www.npmjs.com/package/jiti)
- [...5M+ public repositories](https://github.com/unjs/jiti/network/dependents)
- [ add yours ]

## Usage

### Programmatic

```js
const jiti = require("jiti")(__filename);

// CommonJS mode
jiti("./path/to/file.ts");

// ESM mode
await jiti.import("./path/to/file.ts");
```

You can also pass options as second argument:

```js
const jiti = require("jiti")(__filename, { debug: true });
```

### CLI

```bash
jiti index.ts
# or npx jiti index.ts
```

### Register require hook

```bash
node -r jiti/register index.ts
```

Alternatively, you can register `jiti` as a require hook programmatically:

```js
const jiti = require("jiti")();
const unregister = jiti.register();
```

## Options

### `debug`

- Type: Boolean
- Default: `false`
- Environment Variable: `JITI_DEBUG`

Enable debug to see which files are transpiled

### `cache`

- Type: Boolean | String
- Default: `true`
- Environment Variable: `JITI_CACHE`

Use transpile cache

If set to `true` will use `node_modules/.cache/jiti` (if exists) or `{TMP_DIR}/node-jiti`

### `esmResolve`

- Type: Boolean | String
- Default: `false`
- Environment Variable: `JITI_ESM_RESOLVE`

Using esm resolution algorithm to support `import` condition.

### `transform`

- Type: Function
- Default: Babel (lazy loaded)

Transform function. See [src/babel](./src/babel.ts) for more details

### `sourceMaps`

- Type: Boolean
- Default `false`
- Environment Variable: `JITI_SOURCE_MAPS`

Add inline source map to transformed source for better debugging.

### `interopDefault`

- Type: Boolean
- Default: `false`

Return the `.default` export of a module at the top-level.

### `alias`

- Type: Object
- Default: -
- Environment Variable: `JITI_ALIAS`

Custom alias map used to resolve ids.

### `nativeModules`

- Type: Array
- Default: ['typescript`]
- Environment Variable: `JITI_NATIVE_MODULES`

List of modules (within `node_modules`) to always use native require for them.

### `transformModules`

- Type: Array
- Default: []
- Environment Variable: `JITI_TRANSFORM_MODULES`

List of modules (within `node_modules`) to transform them regardless of syntax.

### `experimentalBun`

- Type: Boolean
- Default: Enabled if `process.versions.bun` exists (Bun runtime)
- Environment Variable: `JITI_EXPERIMENTAL_BUN`

Enable experimental native Bun support for transformations.

## Development

- Clone this repository
- Enable [Corepack](https://github.com/nodejs/corepack) using `corepack enable`
- Install dependencies using `pnpm install`
- Run `pnpm dev`
- Run `pnpm jiti ./test/path/to/file.ts`

## License

MIT. Made with 💖

<!-- Badged -->

[npm-version-src]: https://img.shields.io/npm/v/jiti?style=flat&colorA=18181B&colorB=F0DB4F
[npm-version-href]: https://npmjs.com/package/jiti
[npm-downloads-src]: https://img.shields.io/npm/dm/jiti?style=flat&colorA=18181B&colorB=F0DB4F
[npm-downloads-href]: https://npmjs.com/package/jiti
[bundle-src]: https://img.shields.io/bundlephobia/minzip/jiti?style=flat&colorA=18181B&colorB=F0DB4F
[bundle-href]: https://bundlephobia.com/result?p=jiti
[license-src]: https://img.shields.io/github/license/unjs/jiti.svg?style=flat&colorA=18181B&colorB=F0DB4F
[license-href]: https://github.com/unjs/jiti/blob/main/LICENSE
