# splitChunks研究

是commentChunks的替代品，也是加强。

### 推荐的默认的配置

webpack可以自动分离chunks在下述几种情况：

1. 新的chunk可以被共享，或者chunk来自node_modules文件夹中；
2. 新的chunk在gzip和minimize之前，大于30kb；
3. 按需加载的chunk时，设置的并行请求的最大值小于等于5
4. 初始化页面时，设置的并行请求的最大值小于等于3

```js
optimization: {
    splitChunks: {
      chunks: 'async',
      minSize: 30000,
      maxSize: 0,
      minChunks: 1,
      maxAsyncRequests: 5,
      maxInitialRequests: 3,
      automaticNameDelimiter: '~',
      name: true,
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          priority: -10
        },
        default: {
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true
        }
      }
    }
  }
```

### 自己配置

当然我们也可以自己配置。

