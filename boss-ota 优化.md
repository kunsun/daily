# boss-ota 优化

### 针对项目：
1. boss-ota
2. boss-ota-archive

### 为何要优化：
* 和其他项目的开发环境不一致
* 没有做线上编译

### 优化内容：
1. 本地server端口统一为8080
2. 页面路由和线上保持一致，如 https://preview.apk.10046.mi.com/pay/buy_card_home 不必改为https://preview.apk.10046.mi.com/buy_card_home.html 调试。
3. 增加线上编译，不需要对boss-ota-archive进行git操作