# jsdeliver-proxy
使用cloudflare worker反代jsdeliver被污染的CDN

## 部署

在cloudflare主页找到Worker 进入后选择创建服务 选择启动器**请选择HTTP处理程序**（其他的没测试 但应该工作）

创建后在跳转的页面选择**快速编辑** 将[index.js](https://github.com/GuihongWang/jsdeliver-proxy/blob/main/index.js)这个链接里的js里的字符粘贴到worker的编辑器里

点击**保存并部署** 即可在全球部署![](https://file.marisa.ml/images/?/images/2022/05/21/y80XW3N8sj/01186AB7AD4DAE67D5D7EF16E99B3650.jpg) ~~并引起全球温室效应~~（bushi）

最后在worker编辑器的右侧的发送按钮的左侧 输入    `你的worker地址/npm/yandex-metrica-watch/tag.js`       显示 绿灯 200 OK 即为正常

## 绑定域名

先去[XIU2/CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest) 找一个最优ip 或者使用1.1.1.1

打开cloudflare主页 随便找一个域名 打开 DNS 页

创建一个记录 填上一个你喜欢 又记得住的名称 类型选择A 
IPV4地址填前面最优ip 或者 1.1.1.1 然后按确定

然后跳转到 Worker 页

添加路由 路由填你刚才创建的域名记录（例:test.example.com 是一个路由) 
服务选你创建的worker名 环境直接选第一个 

下面的**请求限制失败模式** 可以选择 

故障时自动关闭（阻止）：
免费的每日100,000次请求用完之后 会关闭一天这个worker 再次请求会返回错误

或者

出故障时自动打开（继续）：
免费的每日100,000次请求用完之后 会重新引导到fastly.jsdeliver.net


# 注意

在浏览器直接访问js文件的时候 你的worker地址 花了太长时间进行响应是正常的

## 对比

| 对比 用✔/❌或者% | Cloudflare Worker | 官方CDN 未污染前 | 官方CDN |
|  ----  | ----  | ----  | ----  |
| 本地易用性 | ❌ 无Gui | ✔ | ✔ |
| 访问性 | ✔ 可以使用国内的节点 |✔多家CDN加成 速度几乎是比worker比肩的境外CDN |❌已污染 |
| 限制 | ❌每日只有100,000请求 |✔ 几乎全球快速响应 |❌ 当局DNS污染 |
| 稳定性 | 65% 使用默认域名时 时常不稳定（昨天部署 今天就有问题了）|99.99% 即便是维护也是无痛级别的 |0% 可能已挂 |
