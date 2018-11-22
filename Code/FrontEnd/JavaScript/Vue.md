# Vue

## Tips

- 自定义 webpack 配置
    - 在`import Vue from 'vue'`之前时需在webpack配置
    ```javascript
    resolve: {
    alias: {
    'vue\$': 'vue/dist/vue.esm.js',
    }
    },
    ```
