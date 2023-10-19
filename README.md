<p align="center">
<img src="https://socialify.git.ci/nonzzz/vite-plugin-compression/image?description=1&font=KoHo&language=1&logo=https%3A%2F%2Fcamo.githubusercontent.com%2F61e102d7c605ff91efedb9d7e47c1c4a07cef59d3e1da202fd74f4772122ca4e%2F68747470733a2f2f766974656a732e6465762f6c6f676f2e737667&name=1&pattern=Solid&theme=Auto" width="640" height="320" />
</p>

[![codecov](https://codecov.io/gh/nonzzz/vite-plugin-compression/branch/master/graph/badge.svg?token=NG4475OP6B)](https://codecov.io/gh/nonzzz/vite-compression-plugin)

## Install

```bash

$ yarn add vite-plugin-compression2 -D

# or

$ npm install vite-plugin-compression2 -D

```

## Usage

```js
import { defineConfig } from 'vite'

import { compression } from 'vite-plugin-compression2'

export default defineConfig({
  plugins: [
    // ...your plugin
    compression()
  ]
})
```

## Options

| params                 | type                                          | default           | description                                                    |
| ---------------------- | --------------------------------------------- | ----------------- | -------------------------------------------------------------- |
| `include`              | `string \| RegExp \| Array<string \| RegExp>` | `-`               | Include all assets matching any of these conditions.           |
| `exclude`              | `string \| RegExp \| Array<string \| RegExp>` | `-`               | Exclude all assets matching any of these conditions.           |
| `threshold`            | `number`                                      | `0`               | Only assets bigger than this size are processed (in bytes)     |
| `algorithm`            | `string\| function`                           | `gzip`            | The compression algorithm                                      |
| `compressionOptions`   | `Record<string,any>`                          | `{}`              | Compression options for `algorithm`(details see `zlib module`) |
| `deleteOriginalAssets` | `boolean`                                     | `false`           | Whether to delete the original assets or not                   |
| `skipIfLargerOrEqual`  | `boolean`                                     | `false`            | Whether to skip the compression if the result is larger than or equal to the original file |
| `filename`             | `string`                                      | `[path][base].gz` | The target asset filename                                      |

## Q & A

> Why not vite-plugin-compression

- `vite-plugin-compression` no longer maintenance.

> Why vite-plugin-compression2

- `vite-plugin-compression2` has minimal dependencies and better performance.

> Can i custom the compression algorithm?

- Yes, you can see the unit test case.

> Can i generate multiple compressed assets with difference compression algorithm?

```js
import { defineComponent } from 'vite'
import { compression } from 'vite-plugin-compression2'

export default defineComponent({
  plugins: [
    // ...your plugin
    compression(),
    compression({ algorithm: 'brotliCompress', exclude: [/\.(br)$/, /\.(gz)$/], deleteOriginalAssets: true })
  ]
})
```

- You should set `exclude` for the latest compression plugin. ( Because in the full bundle process. Bundle chunk is shared. And
  there are write (delete) operations on the bundle inside the plugin. So you should ignore the compressed chunk :) If you want delete
  the original assets you also follow the way.


### Others

If you want to further optimize the bundle size. You can take a look [vite-plugin-cdn2](https://github.com/nonzzz/vite-plugin-cdn)

### LICENSE

[MIT](./LICENSE)

### Author

Kanno
