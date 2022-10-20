# @kwai-explore/picture

用于展示多种图片格式的 picture 组件。

## 使用

> 建议配合 (vite-plugin-image-presets) 使用

### 安装 [vite-plugin-image-presets](github.com/ElMassimo/vite-plugin-image-presets)

`pnpm add -D vite-plugin-image-presets` 

 ### 建议配置

 `vite.config.ts`

 ```ts
 import imagePresets, { formatPreset } from 'vite-plugin-image-presets';
 
 // ...
  plugins: [
    vue(),
    imagePresets({
      modern: formatPreset({
        formats: {
          avif: {},
          webp: {},
          original: {},
        },
        loading: 'lazy',
      }),
    }),
  ],
 ```

添加类型：
 
 `vite-env.d.ts`

 ```ts
 declare module '*?preset=modern' {
  const src: import('vue').ImgHTMLAttributes[];
  // vue2.7 换成：
  // const src: import('vue/types/jsx').ImgHTMLAttributes[];
  export default src;
}
 ```

### 安装依赖

`pnpm add @kwai-explore/picture`

### 在代码中使用

> Picture 组件接受的属性跟 `img` 相同

```vue
<script setup lang="ts">
import Picture from '@kwai-explore/picture';
import examplePic from './components/example.jpg?preset=modern';
</script>

<template>
  <Picture :src="examplePic"></Picture>
</template>
```

数据不能用插件生成时（比如接口种的数据），样例 `src` 属性是(注意顺序)

```json
  [{
    type: 'image/webp',
    srcset: '/assets/logo.ffc730c4.webp 48w, /assets/logo.1f874174.webp 96w',
  },
  {
    type: 'image/jpeg',
    srcset: '/assets/logo.063759b1.jpeg 48w, /assets/logo.81d93491.jpeg 96w',
    src: '/assets/logo.81d93491.jpeg',
    class: 'img thumb',
    loading: 'lazy',
  ]
```

### 对应的行为

开发环境（`vite dev`) 初次请求图片资源时需要进行格式转换，图片的加载时间比较长。

生产环境（`vite build`) 会把需要的图片格式都构建出来。

## 兼容性

vue >= 2.7
