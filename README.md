# jsdeliver-proxy
使用cloudflare worker反代jsdeliver被污染的CDN

## 部署

在cloudflare主页找到Worker 进入后选择创建服务 选择启动器**请选择HTTP处理程序**（其他的没测试 但应该工作）

创建后在跳转的页面选择**快速编辑** 将[index.js](https://github.com/GuihongWang/jsdeliver-proxy/blob/main/index.js)这个链接里的js里的字符粘贴到worker的编辑器里

点击**保存并部署** 即可在全球部署![](https://file.marisa.ml/images/?/images/2022/05/21/y80XW3N8sj/01186AB7AD4DAE67D5D7EF16E99B3650.jpg) ~~并引起全球温室效应~~（bushi）

最后在worker编辑器的右侧的发送按钮的左侧 输入    `你的worker地址/npm/yandex-metrica-watch/tag.js`       显示 绿灯 200 OK 即为正常

# 注意

在浏览器直接访问js文件的时候 你的worker地址 花了太长时间进行响应是正常的
