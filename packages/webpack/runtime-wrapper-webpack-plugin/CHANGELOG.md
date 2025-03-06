# @lynx-js/runtime-wrapper-webpack-plugin

## 0.0.8

### Patch Changes

- Support NPM provenance. ([#30](https://github.com/lynx-family/lynx-stack/pull/30))

- Updated dependencies [[`c617453`](https://github.com/lynx-family/lynx-stack/commit/c617453aea967aba702967deb2916b5c883f03bb)]:
  - @lynx-js/webpack-runtime-globals@0.0.5

## 0.0.7

### Patch Changes

- 1abf8f0: Set the default `targetSdkVersion` to 3.2.

## 0.0.6

### Patch Changes

- 26258c7: Shim `fetch` using `lynx.fetch`.

## 0.0.5

### Patch Changes

- Updated dependencies [3bf5830]
  - @lynx-js/webpack-runtime-globals@0.0.4

## 0.0.4

### Patch Changes

- 649b978: Add `globDynamicComponentEntry` for background script.

  |             |     Before      |     After      |
  | :---------: | :-------------: | :------------: |
  | Main Bundle | defined(global) | Defined(local) |
  | Lazy Bundle | defined(global) | Defined(local) |

- f5913e5: Inject `RuntimeGlobals.lynxChunkEntries` to ensure getting correct entryName in lazy bundles.
- Updated dependencies [f5913e5]
  - @lynx-js/webpack-runtime-globals@0.0.3

## 0.0.3

### Patch Changes

- be5d731: Override `Promise` using `lynx.Promise`.
- 3fae00a: Add `injectVars` option.
