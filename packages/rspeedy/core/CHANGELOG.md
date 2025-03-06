# @lynx-js/rspeedy

## 0.8.3

### Patch Changes

- Support NPM provenance. ([#30](https://github.com/lynx-family/lynx-stack/pull/30))

- Bump Rsbuild v1.2.15 with Rspack v1.2.7. ([#44](https://github.com/lynx-family/lynx-stack/pull/44))

- Updated dependencies [[`c617453`](https://github.com/lynx-family/lynx-stack/commit/c617453aea967aba702967deb2916b5c883f03bb)]:
  - @lynx-js/chunk-loading-webpack-plugin@0.1.7
  - @lynx-js/webpack-dev-transport@0.1.1
  - @lynx-js/websocket@0.0.4

## 0.8.2

### Patch Changes

- 1abf8f0: feat(rspeedy): support generateStatsFile
- 1abf8f0: Bump Rsbuild v1.2.11 with Rspack v1.2.3

## 0.8.1

### Patch Changes

- 2d15b44: fix: default value of output.filename changes to be `[name].[platform].bundle`.
- 2c88797: Disable tree-shaking in development.
- 1472918: Remove `output.minify.jsOptions.exclude`.
- 9da942e: Fix HMR connection lost after restart development server.
- Updated dependencies [9da942e]
  - @lynx-js/webpack-dev-transport@0.1.0

## 0.8.0

### Minor Changes

- 3319e0f: **BREAKING CHANGE**: Use `cssnano` by default.

  We enable CSS minification in v0.7.0 and use Lightning CSS by default.
  But there are cases that Lightning CSS produce CSS that cannot be used in Lynx.

  Now, the default CSS minifier is switched to `cssnano` using `@rsbuild/plugin-css-minimizer`.

  You can switch to other tools by using:

  ```js
  import { defineConfig } from '@lynx-js/rspeedy'
  import {
    CssMinimizerWebpackPlugin,
    pluginCssMinimizer,
  } from '@rsbuild/plugin-css-minimizer'

  export default defineConfig({
    plugins: [
      pluginCssMinimizer({
        pluginOptions: {
          minify: CssMinimizerWebpackPlugin.esbuildMinify,
          minimizerOptions: {
            /** Custom options */
          },
        },
      }),
    ],
  })
  ```

  See [@rsbuild/plugin-css-minimizer](https://github.com/rspack-contrib/rsbuild-plugin-css-minimizer) for details.

- 3319e0f: **BREAKING CHANGE**: Remove `output.minify.cssOptions`.

  You can use custom options with [@rsbuild/plugin-css-minimizer](https://github.com/rspack-contrib/rsbuild-plugin-css-minimizer):

  ```js
  import { defineConfig } from '@lynx-js/rspeedy'
  import { pluginCssMinimizer } from '@rsbuild/plugin-css-minimizer'

  export default defineConfig({
    plugins: [
      pluginCssMinimizer({
        pluginOptions: {
          minimizerOptions: {
            /** Custom options */
          },
        },
      }),
    ],
  })
  ```

## 0.7.1

### Patch Changes

- 58607e4: Correct the handling of `dev.assetPrefix` to ensure it accurately reflects the `server.port` when the specified port is already in use.

## 0.7.0

### Minor Changes

- e2e23e2: Deprecated `output.filename.template`, use `output.filename.bundle` instead.
- e2e23e2: **BREAKING CHANGE**: Change the default `output.filename` to `[name].lynx.bundle`.
- a589e2e: **BREAKING CHANGE**: Enable CSS minification by default.

  You may turn it off using `output.minify.css: false`:

  ```js
  import { defineConfig } from '@lynx-js/rspeedy'

  export default defineConfig({
    output: {
      minify: {
        css: false,
      },
    },
  })
  ```

  Or you may use [@rsbuild/plugin-css-minimizer](https://github.com/rspack-contrib/rsbuild-plugin-css-minimizer) to use `cssnano` as CSS minimizer.

  ```js
  import { defineConfig } from '@lynx-js/rspeedy'
  import { pluginCssMinimizer } from '@rsbuild/plugin-css-minimizer'

  export default defineConfig({
    plugins: [pluginCssMinimizer()],
  })
  ```

- 525554c: **BREAKING CHANGE**: Bump ts-blank-space to ^0.6.0.

  Drop support for legacy module namespaces, see [microsoft/TypeScript#51825](https://github.com/microsoft/TypeScript/issues/51825) for details.

### Patch Changes

- 59bba00: Bump Rsbuild v1.2.7 with Rspack v1.2.3.
- a589e2e: Add `output.minify.css` and `output.minify.cssOptions`.
- 6de1176: feat(rspeedy/core): Introduce `source.assetsInclude` to allow the inclusion of additional files to be processed as static assets

## 0.6.0

### Minor Changes

- 2f5c499: Bump Rsbuild v1.2.4 with Rspack v1.2.2

### Patch Changes

- 5ead4b8: Support `type: 'reload-server'` in `dev.watchFiles`.

  - The default `type: 'reload-page'` will reload the Lynx page when it detects changes in the specified files.
  - The new `type: 'reload-server'` will restart the development server when it detects changes in the specified files.

  ```js
  import { defineConfig } from '@lynx-js/rspeedy'

  export default defineConfig({
    dev: {
      watchFiles: [
        {
          type: 'reload-server',
          paths: ['public/**/*.txt'],
        },
        {
          type: 'reload-page',
          paths: ['public/**/*.json'],
        },
      ],
    },
  })
  ```

- be9b003: Add `source.exclude`.
- 2643477: Add `performance.removeConsole`.

## 0.5.10

### Patch Changes

- Updated dependencies [65ecd41]
  - @lynx-js/chunk-loading-webpack-plugin@0.1.6

## 0.5.9

### Patch Changes

- cb337de: Add `source.decorators`.

  You may use `source.decorators.version: '2022-03'` for using Stage 3 decorator proposal.

  Or use `source.decorators.version: 'legacy'` for using TypeScript's `experimentalDecorators: true`.

  See [How does this proposal compare to other versions of decorators?](https://github.com/tc39/proposal-decorators?tab=readme-ov-file#how-does-this-proposal-compare-to-other-versions-of-decorators) for details.

  - @lynx-js/chunk-loading-webpack-plugin@0.1.5

## 0.5.8

### Patch Changes

- 30096c9: Exclude minify for `template.js` of lazy bundle to avoid build error.
- Updated dependencies [0067512]
  - @lynx-js/chunk-loading-webpack-plugin@0.1.4

## 0.5.7

### Patch Changes

- 80a892c: Bump Rsbuild v1.1.13.

## 0.5.6

### Patch Changes

- ee6ed69: Bump Rsbuild v1.1.12 with Rspack v1.1.8.
- 8f91e6c: Add `exit` to plugin api.

## 0.5.5

### Patch Changes

- 9279ce1: Bump Rsbuild v1.1.10 with Rspack v1.1.6.
