# Vite SVG Vue
Vite plugin to inline SVG files with Vue.js and automatically optimize them with SVGO.

<a href="https://www.npmjs.com/package/vite-svg-vue" target="_blank"><img src="https://img.shields.io/npm/v/vite-svg-vue?style=flat-square" alt="Version"></a>
<a href="https://www.npmjs.com/package/vite-svg-vue" target="_blank"><img src="https://img.shields.io/npm/dw/vite-svg-vue?style=flat-square" alt="Downloads"></a>
<a href="https://github.com/academeet/vite-svg-vue/actions" target="_blank"><img src="https://img.shields.io/github/actions/workflow/status/academeet/vite-svg-vue/e2e.yml?branch=main&label=tests&style=flat-square" alt="Tests"></a>
<a href="https://www.npmjs.com/package/vite-svg-vue" target="_blank"><img src="https://img.shields.io/npm/l/vite-svg-vue?style=flat-square" alt="License"></a>

```vue
<template>
  <MyIcon />
</template>

<script setup>
import MyIcon from './my-icon.svg'
</script>
```

### Install
```bash
npm install vite-svg-vue --save-dev
```

### Setup

#### `vite.config.js`
```js
import svgLoader from 'vite-svg-loader'

export default defineConfig({
  plugins: [vue(), svgLoader()]
})
```
The last step is to import and register the Vue component,  for Vue 3. Notice the different imports for `SvgVue`:



#### Vue 3

```js
// e.g. app.js
import { createApp } from 'vue';
import SvgVue from 'svg-vue3';

const app = createApp({});

app.use(SvgVue);

app.mount('#app');
```

## Usage

To display your SVG files, all you need to do is pass the filename (and path if placed inside a subdirectory) to the Vue component:

```html
<!-- resources/svg/avatar.svg -->
<svg-vue icon="avatar"></svg-vue>

<!-- resources/svg/fontawesome/check.svg -->
<svg-vue icon="fontawesome/check"></svg-vue>

<!-- you can also use a "dot" notation as path -->
<svg-vue icon="fontawesome.check"></svg-vue>
```

## Options

If nothing is passed to the extension inside your svgLoader config in vitee.config.js, the following options should be used:

#### `vite.config.js`
```js
svgLoader({
            svgoConfig:{
                plugins: [
                    {
                      name: 'preset-default',
                    },
                    'removeViewBox',
                    'removeDimensions'
                  ],
              
            }
            
        }),
```


### Default import config
When no explicit params are provided SVGs will be imported as Vue components by default.
This can be changed using the `defaultImport` config setting,
such that SVGs without params will be imported as URLs (or raw strings) instead.

#### `vite.config.js`
```js
svgLoader({
  defaultImport: 'url' // or 'raw'
})
```

### SVGO Configuration
#### `vite.config.js`
```js
svgLoader({
  svgoConfig: {
    multipass: true
  }
})
```

### Disable SVGO
#### `vite.config.js`
```js
svgLoader({
  svgo: false
})
```

### Skip SVGO for a single file
SVGO can be explicitly disabled for one file by adding the `?skipsvgo` suffix:
```js
import IconWithoutOptimizer from './my-icon.svg?skipsvgo'
// <IconWithoutOptimizer />
```

### Use with TypeScript
If you use the loader in a Typescript project, you'll need to import your svg files with the `?component` param: `import MyIcon from './my-icon.svg?component'`.

You'll also need to reference the type definitions:
```ts
/// <reference types="vite-svg-loader" />
```


