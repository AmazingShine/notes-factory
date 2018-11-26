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
- vue渲染完毕再显示页面
    ```html
    <div id='app' v-cloak>
    ```
    ```css
    [v-cloak] {
        display: none;
    }
    ```
