# @lynx-js/react

## 0.105.1

### Patch Changes

- Support NPM provenance. ([#30](https://github.com/lynx-family/lynx-stack/pull/30))

- feat: add compiler only version of addComponentElement, it does not support spread props but have no runtime overhead, use it by: ([#15](https://github.com/lynx-family/lynx-stack/pull/15))

  ```js
  pluginReactLynx({
    compat: {
      addComponentElement: {
        compilerOnly: true,
      },
    },
  });
  ```

- Fix error `createRef is not a function` ([#16](https://github.com/lynx-family/lynx-stack/pull/16))

- Support `MIXED` target for worklet, it will be used by unit testing frameworks, etc. ([#27](https://github.com/lynx-family/lynx-stack/pull/27))

## 0.105.0

### Minor Changes

- 1abf8f0: Support `estimated-main-axis-size-px`

  NOTE: This changes behavior of `transformReactLynx` so certain features (like lazy bundle) will be BROKEN if version mismatch.

- 1abf8f0: Support JSXSpread on `<list-item/>` component.

  NOTE: This changes behavior of `transformReactLynx` so certain features (like lazy bundle) will be BROKEN if version mismatch.

### Patch Changes

- 1abf8f0: Update readme.
- 1abf8f0: Save some bytes if `<page/>` is not used.
- 1abf8f0: Should escape newline character in jsx

## 0.104.1

### Patch Changes

- 9ce9ec0: Fix argument cannot be accessed correctly in default exported MTS functions.
- 99a4de6: Change TypeScript configuration to improve tree-shaking by setting `verbatimModuleSyntax: false`.

  This change allows the bundler to properly remove unused imports and type-only imports, resulting in smaller bundle sizes. For example:

  ```ts
  // These imports will be removed from the final bundle
  import type { Foo } from 'xyz';
  import { type Bar } from 'xyz';
  import { xyz } from 'xyz'; // When xyz is not used
  ```

  See [TypeScript - verbatimModuleSyntax](https://www.typescriptlang.org/tsconfig/#verbatimModuleSyntax) for details.

## 0.104.0

### Minor Changes

- 575e804: Remove misleading API `createRoot`

### Patch Changes

- 797ff68: Workaround the `cannot find module './snapshot/event.js'` error avoid tree-shaking `event.js` in development.
- 1bf9271: fix(react): default `compat` in transform to `false`

## 0.103.5

### Patch Changes

- 74e0ea3: Supports new `__MAIN_THREAD__` and `__BACKGROUND__` macro as an alternative to `__LEPUS__` and `__JS__`.

## 0.103.4

### Patch Changes

- 89a9f7a: Improve the speed of MTS.

## 0.103.3

### Patch Changes

- 4e94846: Fix variables being renamed in MTS.
- 297c6ea: Fix the issue that when `runOnBackground()`'s parameter is not legal, it will still report an error in the rendering process of the background thread even though it won't actually be called.

  ```tsx
  function App() {
    const f = undefined;

    function mts() {
      'main thread';
      // throws in background rendering
      f && runOnBackground(f)();
    }
  }
  ```

- 763ad4e: Stop reporting ctx id in the `ctx not found` error.
- 480611d: Avoid error from changing theme.
- 3bf5830: Avoid overriding `processEvalResult`.

## 0.103.2

### Patch Changes

- 580ce54: Fix snapshot not found in HMR updates.

## 0.103.1

### Patch Changes

- 80a4e38: Use hooks `useLynxGlobalEventListener` to make `useInitData` addListener as early as possible. This will fix the issue that `onDataChanged` has been called before the event listener is added.
- 8aa3979: Fix generating wrong JavaScript when using a variable multiple times in the main thread script.
- 318245e: Avoid snapshot ID conflict between different templates and bundles.
- b520862: Remove unnecessary sideEffects to reduce bundle size.
- 7cd840c: Integrate with `@lynx-js/types`.

## 0.103.0

### Minor Changes

- a30c83d: Add `compat.removeComponentAttrRegex`.

  ```js
  import { pluginReactLynx } from '@lynx-js/react-rsbuild-plugin';
  import { defineConfig } from '@lynx-js/rspeedy';

  export default defineConfig({
    plugins: [
      pluginReactLynx({
        compat: {
          removeComponentAttrRegex: 'YOUR REGEX',
        },
      }),
    ],
  });
  ```

  NOTE: This feature is deprecated and will be removed in the future. Use codemod instead.

- 5f8d492: Deprecate `compat.simplifyCtorLikeReactLynx2`

### Patch Changes

- ca3a639: Fix `cssId` collision issue when hash generated `@jsxCSSId` for jsx snapshot hit the range of auto increased cssId of `@file`.
- 8fbea78: Fix 'main thread' and 'background only' directives not working in export default declarations.
- ff18049: Bump swc_core v0.109.2.

  This would add `/*#__PURE__*/` to the output of TypeScript `enum`. See [swc-project/swc#9558](https://github.com/swc-project/swc/pull/9558) for details.

## 0.102.0

### Minor Changes

- e3be842: Fix some attribute updating of nodes in list does not take effect
- 2e6b549: Add ability to be compat with pre-0.99 version of ReactLynx

### Patch Changes

- 75725cb: Fix a memory leak in MTS.
- 09e0ec0: Reduce the size of `background.js`.
- 9e40f33: Slightly improve MTS execution speed.
- f24599e: Fix the infinite mount and unmount loops of lazy bundle when its JS file fails to execute.

## 0.101.0

### Minor Changes

- 6730c58: Change the snapshot transform result by adding `cssId` and `entryName`.

  <table>
    <thead>
      <tr>
        <th>Remove Scoped CSS(Default)</th>
        <th>Scoped CSS</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>
          <pre><code>
  createSnapshot(
    $uid,
    $create,
    $update,
    $slot,
    /** cssId */ undefined,
    /** entryName */ globDynamicComponentEntry
  );
          </code></pre>
        </td>
        <td>
          <pre><code>
  createSnapshot(
    $uid,
    $create,
    $update,
    $slot,
    /** cssId */ 0x3da39a,
    /** entryName */ globDynamicComponentEntry
  );
          </code></pre>
        </td>
      </tr>
    </tbody>
  </table>

  This requires `@lynx-js/react-rsbuild-plugin` v0.5.1 to work.

  - Inject `globDynamicComponentEntry` for background script. ([#311](https://github.com/lynx-wg/lynx-stack/pull/311))
  - Inject `globDynamicComponentEntry` for main thread script. ([#312](https://github.com/lynx-wg/lynx-stack/pull/312))

- efbb7d4: Support Gesture.

  Gesture Handler is a set of gesture handling capabilities built on top of the Main Thread Script. It currently supports drag, inertial scrolling, long press, and tap gestures for `<view>`, `<scroll-view>`, `<list>`, and `<text>`. In the future, it will also support multi-finger zoom, multi-finger rotation, and other gesture capabilities.

  ```tsx
  import { useGesture, PanGesture } from '@lynx-js/gesture-runtime';

  function App() {
    const pan = useGesture(PanGesture);

    pan
      .onBegin((event, stateManager) => {
        'main thread';
        // some logic
      })
      .onUpdate((event, stateManager) => {
        'main thread';
        // some logic
      })
      .onEnd((event, stateManager) => {
        'main thread';
        // some logic
      });

    return <view main-thread:gesture={pan}></view>;
  }
  ```

### Patch Changes

- b2032eb: Better DCE.

  Now DCE can remove dead branch:

  ```ts
  function f() {
    if (__LEPUS__) {
      return;
    }

    console.log('not __LEPUS__'); // This can be removed now
  }
  ```

- 45edafa: Support using `import()` with variables.

## 0.100.0

### Minor Changes

- 587a782: Release `@lynx-js/react` v0.100.0

### Patch Changes

- a335490: Fix an issue where events might not fire after calling `ReloadTemplate`.
