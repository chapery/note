# umijs

## scoped-css

### 安装依赖包

```
npm install -D babel-plugin-react-scoped-css scoped-css-loader
```

### 修改配置

```javascript
// .umirc.ts
export default defineConfig({
  chainWebpack(memo, { env, webpack, createCSSRule }) {
    memo.module.rules.get('sass').pre().use('scoped-css').loader('scoped-css-loader')
    memo.module.rules.get('js').uses.get('babel-loader').tap(options => {
      options.plugins.push([
        "babel-plugin-react-scoped-css",
        {
          // 默认值 '.scoped.(sa|sc|c)ss$'
          "include": ".scss$"
        }
      ])
      return options
    })
  }
});
```
