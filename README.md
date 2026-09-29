# VPS测评：从线路、性能到价格，拆解 DMIT 节点、套餐与限制

做 VPS 测评，真正值得看的其实不是“几核、几 GB”这一行参数，而是这些资源在真实网络环境里能不能稳定工作：访问中国大陆的延迟怎么样，晚高峰会不会抖，磁盘是不是拖后腿，流量怎么算，IP 好不好用，以及出了问题能不能退款。

这也是我这次看 DMIT 的重点。目标链接对应的是 **DMIT**，当前官网的 Cloud Instance 仍然围绕洛杉矶、香港、东京三个节点，以及 Premium、Eyeball、Tier 1 三种网络路线展开。官网还把硬件进一步拆成 AS3、AN4、AN5 三代平台。

先给一个很实际的判断框架：**如果你的 VPS 主要服务中国大陆用户，线路通常比“多 1 核还是多 2 GB 内存”更值得优先研究；如果用户主要在美国、欧洲或全球分布，又没有中国大陆访问需求，Tier 1 这类更便宜的路线反而更容易算清成本。** DMIT 自己对三种网络的定位也是这样划分的。

[👉 查看 DMIT 当前 VPS 方案](https://bit.ly/DmiT)

## 先看懂 VPS 测评：别被 10Gbps 和“CN2”两个词带跑

VPS 测评里最容易出现的误区，就是把“带宽端口”“线路名称”“测速峰值”当成同一个指标。

比如一台机器写着 10Gbps，并不代表你从中国大陆某个家庭宽带下载文件就能长期跑到 10Gbps。实际体验还会受到访问运营商、目的地、时段、路由变化、测速节点负载和单线程能力影响。近期一篇 2026 年 8 月的 DMIT LAX Premium 实测就是很好的例子：部分中国大陆省份的 TCP 测试表现稳定，但具体到某些 UDP 路径和特定测速节点，仍然会出现明显差异。

所以一篇有用的 VPS 测评，至少要拆开看：

**网络路线**：去程、回程走什么网络，是否针对中国大陆做优化。

**延迟与丢包**：不能只看一次 Ping，最好看高峰时段、多个运营商和多个城市。

**CPU 与磁盘**：vCPU 数量只是起点，硬件代际和 NVMe 存储会直接影响网站、数据库、编译和虚拟化类任务。

**流量规则**：普通 Transfer 和 `Max (IN, OUT)` 不是一个概念。后者意味着入站和出站流量采用双向统计上限。

**IP 质量**：原生 IP、地理位置、邮件声誉、流媒体或第三方服务解锁能力，都可能比 CPU 参数更影响某些实际用途。

**售后与退款**：真正准备长期使用时，这一项经常被价格表遮住，但反而是最值得先读的地方。

DMIT 当前 Cloud Instance 页面明确写明所有计划提供免费即时部署和 root 权限，同时支持常见 Linux 镜像、自动备份、即时快照和 SSH Key 认证。

## DMIT 的三种网络路线，差异到底在哪

DMIT 当前官网将网络分成 Premium、Eyeball 和 Tier 1 三档，而且不是简单的“快、中、慢”，本质上是不同的路由策略。

### Premium：你买的主要是中国大陆访问路径

Premium 使用中国电信 CN2 GIA，并结合 DMIT 自有网络及其他高质量转接。官网对它的描述重点是更低延迟、更少跳数和更低丢包，同时明确把中国大陆和亚太访问质量作为核心使用场景。

香港节点当前官方给出的参考值约为 **15ms 到中国大陆、0.1% 以下丢包**；东京则给出约 **28ms** 的中国大陆参考延迟。官方同时强调，这些是参考测量，实际结果仍取决于访问网络、路线与时间。

这里要注意“参考值”三个字。它不是 SLA，也不是承诺你的所有用户都会看到同样数字。

### Eyeball：牺牲一部分路由保障，换更低价格

Eyeball 使用面向中国大陆的 CMI/CMIN2 等“合理努力”路线，但不具备 Premium 那样的路由保证。DMIT 把它定位成中国与全球用户混合的博客、API、SaaS、远程开发等场景。

HKG Eyeball 现在仍明确标为 **Beta**。官网提醒该产品和路由仍在调试优化中，表现可能变化，并且不建议用于高度依赖稳定性的生产工作负载。

这个提示非常重要。很多 VPS 测评只会告诉你“某条线路便宜多少”，却不会把 Beta 状态写进结论。

### Tier 1：国际业务优先，别为不需要的中国优化付钱

Tier 1 不针对中国大陆做专门路由优化，而是强调亚太、北美、欧洲之间的全球连接和带宽。DMIT 自己把它定位给备份、归档、CI/CD、监控、VPN/中转，以及普通全球计算工作负载。

所以你看到它的价格明显低于 Premium，不应该直接理解成“性能差很多”。更准确的解释是：**两者解决的问题不同。**

如果服务器本身就在服务美国用户，或者只是作为跨区域构建节点，花钱购买针对中国大陆的高质量路线，并不一定能转化成业务上的实际收益。

## 硬件平台也要看：AS3、AN4、AN5 有什么区别

当前官网已经把硬件代际说得比较清楚。

**AN5** 使用 AMD EPYC 9005 系列，Zen 5 架构、DDR5 内存以及 NVMe Gen5 存储，定位是最高单核和多核性能。

**AN4** 使用 AMD EPYC 9004 系列，也就是 Zen 4，官网把它描述为更成熟的通用型平台，适合网站、应用和开发环境。

**AS3** 使用 AMD EPYC 7003 系列，也就是 Zen 3，当前定位更偏预算、测试、开发和一般工作负载。

这三代不应该简单理解成“新的一定值得买，老的一定不能买”。真正需要结合的是：**价格差多少、你的任务是否 CPU 敏感、存储是否敏感、以及这台机器主要服务哪里。**

另外，LAX 的 AS3 目前官网有非常明确的提示：仍在建设和优化期间，可能出现较低的磁盘性能以及低于成熟平台的 SLA。

这类限制应该直接写进 VPS 测评里，而不是藏在脚注。

## DMIT 全套餐对比表

下面三张表合计覆盖当前官方定价/节点页面公开展示的 Cloud Instance VPS 套餐，包括当前可下单和页面明确显示缺货的组合。价格统一按官网当前公开美元价格记录；DMIT 自己也提醒，产品和价格可能因调整而出现页面更新滞后，因此最终下单仍应以结算页为准。

### 洛杉矶 LAX

| 套餐 | 网络 / 平台 | 核心配置 | 流量 / 带宽 | 价格 | 状态 / 购买 |
| --- | --- | --- | --- | --- | --- |
| TINY | Premium / AS3 | 1 vCore / 2GB / 20GB SSD | 1000GB / 1Gbps | $10.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| Pocket | Premium / AS3 | 2 vCore / 2GB / 40GB SSD | 1500GB / 4Gbps | $16.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| STARTER | Premium / AS3 | 2 vCore / 2GB / 80GB SSD | 3000GB / 10Gbps | $34.90/月 | 可下单 · [ 查看当前价格](https://bit.ly/DmiT) |
| MINI | Premium / AS3 | 4 vCore / 4GB / 80GB SSD | 5000GB / 10Gbps | $62.90/月 | 可下单 · [ 进入套餐页](https://bit.ly/DmiT) |
| MICRO | Premium / AS3 | 4 vCore / 4GB / 160GB SSD | 7000GB / 10Gbps | $87.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MEDIUM | Premium / AS3 | 6 vCore / 8GB / 160GB SSD | 15000GB / 10Gbps | $199.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| MINI | Premium / AN4 | 4 vCore / 4GB / 80GB SSD | 5000GB / 10Gbps | $72.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MICRO | Premium / AN4 | 4 vCore / 4GB / 160GB SSD | 7000GB / 10Gbps | $102.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MEDIUM | Premium / AN4 | 6 vCore / 8GB / 160GB SSD | 15000GB / 10Gbps | $239.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| LARGE | Premium / AN4 | 8 vCore / 16GB / 320GB SSD | 25000GB / 10Gbps | $459.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| GIANT | Premium / AN4 | 12 vCore / 24GB / 640GB SSD | 50000GB / 10Gbps | $929.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MINI | Premium / AN5 | 4 vCore / 4GB / 80GB SSD | 5000GB / 10Gbps | $79.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| MICRO | Premium / AN5 | 4 vCore / 4GB / 160GB SSD | 7000GB / 10Gbps | $110.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MEDIUM | Premium / AN5 | 6 vCore / 8GB / 160GB SSD | 15000GB / 10Gbps | $289.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| LARGE | Premium / AN5 | 8 vCore / 16GB / 320GB SSD | 25000GB / 10Gbps | $499.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| GIANT | Premium / AN5 | 12 vCore / 24GB / 640GB SSD | 50000GB / 10Gbps | $1009.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| TINY | Eyeball / AS3 | 1 vCore / 2GB / 20GB SSD | 1500GB / 2Gbps | $10.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| Pocket | Eyeball / AS3 | 2 vCore / 2GB / 40GB SSD | 3000GB / 4Gbps | $16.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| STARTER | Eyeball / AS3 | 2 vCore / 2GB / 80GB SSD | 5000GB / 10Gbps | $34.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MINI | Eyeball / AS3 | 4 vCore / 4GB / 80GB SSD | 10000GB / 10Gbps | $62.90/月 | 可下单 · [ 进入方案](https://bit.ly/DmiT) |
| MICRO | Eyeball / AS3 | 4 vCore / 4GB / 160GB SSD | 14000GB / 10Gbps | $87.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| MEDIUM | Eyeball / AS3 | 6 vCore / 8GB / 160GB SSD | 30000GB / 10Gbps | $199.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MINI | Eyeball / AN4 | 4 vCore / 4GB / 80GB SSD | 10000GB / 10Gbps | $72.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MICRO | Eyeball / AN4 | 4 vCore / 4GB / 160GB SSD | 14000GB / 10Gbps | $102.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MEDIUM | Eyeball / AN4 | 6 vCore / 8GB / 160GB SSD | 30000GB / 10Gbps | $239.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| LARGE | Eyeball / AN4 | 8 vCore / 16GB / 320GB SSD | 50000GB / 10Gbps | $459.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| GIANT | Eyeball / AN4 | 12 vCore / 24GB / 640GB SSD | 100000GB / 10Gbps | $929.90/月 | 缺货 · [ 查看当前库存](https://bit.ly/DmiT) |
| MINI | Eyeball / AN5 | 4 vCore / 4GB / 80GB SSD | 10000GB / 10Gbps | $79.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| MICRO | Eyeball / AN5 | 4 vCore / 4GB / 160GB SSD | 14000GB / 10Gbps | $110.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MEDIUM | Eyeball / AN5 | 6 vCore / 8GB / 160GB SSD | 30000GB / 10Gbps | $289.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| LARGE | Eyeball / AN5 | 8 vCore / 16GB / 320GB SSD | 50000GB / 10Gbps | $499.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| GIANT | Eyeball / AN5 | 12 vCore / 24GB / 640GB SSD | 100000GB / 10Gbps | $1009.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| V2C2G | Tier 1 / AN5 Volume | 2 vCore / 2GB / 40GB SSD | 5000GB Max(IN, OUT) / 10Gbps | $14.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| V2C4G | Tier 1 / AN5 Volume | 2 vCore / 4GB / 80GB SSD | 10000GB Max(IN, OUT) / 10Gbps | $23.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| V4C4G | Tier 1 / AN5 Volume | 4 vCore / 4GB / 120GB SSD | 20000GB Max(IN, OUT) / 10Gbps | $36.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| V4C8G | Tier 1 / AN5 Volume | 4 vCore / 8GB / 160GB SSD | 40000GB Max(IN, OUT) / 10Gbps | $52.90/月 | 可下单 · [ 进入方案](https://bit.ly/DmiT) |
| V8C16G | Tier 1 / AN5 Volume | 8 vCore / 16GB / 240GB SSD | 80000GB Max(IN, OUT) / 10Gbps | $119.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| V12C24G | Tier 1 / AN5 Volume | 12 vCore / 24GB / 320GB SSD | 160000GB Max(IN, OUT) / 10Gbps | $199.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| G2C4G | Tier 1 / AN5 General | 2 vCore / 4GB / 80GB SSD | 4000GB Max(IN, OUT) / 10Gbps | $16.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| G4C8G | Tier 1 / AN5 General | 4 vCore / 8GB / 160GB SSD | 8000GB Max(IN, OUT) / 10Gbps | $36.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| G8C16G | Tier 1 / AN5 General | 8 vCore / 16GB / 320GB SSD | 12000GB Max(IN, OUT) / 10Gbps | $79.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| G12C24G | Tier 1 / AN5 General | 12 vCore / 24GB / 480GB SSD | 240000GB Max(IN, OUT) / 10Gbps | $119.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| G16C32G | Tier 1 / AN5 General | 16 vCore / 32GB / 640GB SSD | 320000GB Max(IN, OUT) / 10Gbps | $199.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| WEE | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 1000GB Max(IN, OUT) | $36.90/年 | 可下单 · [ 查看年付方案](https://bit.ly/DmiT) |
| TINY | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 2000GB Max(IN, OUT) | $6.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| STARTER | Tier 1 / AS3 | 2 vCore / 2GB / 40GB SSD | 4000GB Max(IN, OUT) | $12.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MINI | Tier 1 / AS3 | 2 vCore / 4GB / 80GB SSD | 8000GB Max(IN, OUT) | $21.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MICRO | Tier 1 / AS3 | 4 vCore / 4GB / 120GB SSD | 16000GB Max(IN, OUT) | $32.90/月 | 可下单 · [ 进入方案](https://bit.ly/DmiT) |
| MEDIUM | Tier 1 / AS3 | 4 vCore / 8GB / 160GB SSD | 32000GB Max(IN, OUT) | $49.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| LARGE | Tier 1 / AS3 | 8 vCore / 16GB / 320GB SSD | 64000GB Max(IN, OUT) | $99.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| GIANT | Tier 1 / AS3 | 8 vCore / 24GB / 640GB SSD | 128000GB Max(IN, OUT) | $199.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |

LAX 当前价格和缺货状态来自官方洛杉矶节点价格表；其中 AS3 页面有额外的“仍在建设与优化中”提示。

### 香港 HKG

| 套餐 | 网络 / 平台 | 核心配置 | 流量 / 带宽 | 价格 | 状态 / 购买 |
| --- | --- | --- | --- | --- | --- |
| MINI | Premium / AN5 | 4 vCore / 4GB / 80GB SSD | 1500GB / 1Gbps | $149.90/月 | 可下单 · [ 查看香港 Premium](https://bit.ly/DmiT) |
| MICRO | Premium / AN5 | 4 vCore / 4GB / 160GB SSD | 2000GB / 1Gbps | $199.90/月 | 可下单 · [ 查看当前方案](https://bit.ly/DmiT) |
| MEDIUM | Premium / AN5 | 6 vCore / 8GB / 160GB SSD | 2500GB / 1Gbps | $279.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| LARGE | Premium / AN5 | 8 vCore / 16GB / 320GB SSD | 3000GB / 1Gbps | $359.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| GIANT | Premium / AN5 | 12 vCore / 24GB / 640GB SSD | 6000GB / 1Gbps | $759.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| TINY | Eyeball / AS3 | 1 vCore / 1GB / 20GB SSD | 500GB / 1Gbps | $39.90/月 | 可下单 · [ 查看 HKG Eyeball](https://bit.ly/DmiT) |
| STARTER | Eyeball / AS3 | 1 vCore / 2GB / 40GB SSD | 1000GB / 1Gbps | $79.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| MINI | Eyeball / AS3 | 2 vCore / 4GB / 60GB SSD | 1500GB / 1Gbps | $126.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MICRO | Eyeball / AS3 | 4 vCore / 4GB / 80GB SSD | 2000GB / 1Gbps | $179.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MEDIUM | Eyeball / AS3 | 4 vCore / 8GB / 160GB SSD | 2500GB / 1Gbps | $239.90/月 | 可下单 · [ 进入套餐](https://bit.ly/DmiT) |
| WEE | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 1000GB Max(IN, OUT) | $36.90/年 | 可下单 · [ 查看年付方案](https://bit.ly/DmiT) |
| TINY | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 2000GB Max(IN, OUT) | $6.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| STARTER | Tier 1 / AS3 | 1 vCore / 2GB / 40GB SSD | 4000GB Max(IN, OUT) | $12.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MINI | Tier 1 / AS3 | 2 vCore / 2GB / 60GB SSD | 8000GB Max(IN, OUT) | $21.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MICRO | Tier 1 / AS3 | 4 vCore / 4GB / 80GB SSD | 16000GB Max(IN, OUT) | $32.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| MEDIUM | Tier 1 / AS3 | 4 vCore / 8GB / 160GB SSD | 32000GB Max(IN, OUT) | $49.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| LARGE | Tier 1 / AS3 | 8 vCore / 16GB / 320GB SSD | 64000GB Max(IN, OUT) | $99.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| GIANT | Tier 1 / AS3 | 8 vCore / 24GB / 640GB SSD | 128000GB Max(IN, OUT) | $199.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |

香港当前公开页面明确写着：**AN5 目前只提供 Premium，AS3 目前用于 Eyeball 和 Tier 1。** 另外，HKG Eyeball 仍处于 Beta。

### 东京 TYO

| 套餐 | 网络 / 平台 | 核心配置 | 流量 / 带宽 | 价格 | 状态 / 购买 |
| --- | --- | --- | --- | --- | --- |
| TINY | Premium / AS3 | 1 vCore / 1GB / 20GB SSD | 500GB / 1Gbps | $21.90/月 | 可下单 · [ 查看东京 Premium](https://bit.ly/DmiT) |
| STARTER | Premium / AS3 | 1 vCore / 2GB / 40GB SSD | 1000GB / 1Gbps | $45.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| MINI | Premium / AS3 | 2 vCore / 4GB / 60GB SSD | 2000GB / 1Gbps | $89.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MICRO | Premium / AS3 | 4 vCore / 4GB / 80GB SSD | 4000GB / 1Gbps | $189.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MEDIUM | Premium / AS3 | 4 vCore / 8GB / 160GB SSD | 6000GB / 1Gbps | $320.90/月 | 可下单 · [ 进入套餐](https://bit.ly/DmiT) |
| LARGE | Premium / AS3 | 8 vCore / 16GB / 320GB SSD | 8000GB / 1Gbps | $429.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| GIANT | Premium / AS3 | 8 vCore / 24GB / 640GB SSD | 15000GB / 1Gbps | $829.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| WEE | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 1000GB Max(IN, OUT) | $36.90/年 | 可下单 · [ 查看年付方案](https://bit.ly/DmiT) |
| TINY | Tier 1 / AS3 | 1 vCore / 1GB / 20GB SSD | 2000GB Max(IN, OUT) | $6.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| STARTER | Tier 1 / AS3 | 1 vCore / 2GB / 40GB SSD | 4000GB Max(IN, OUT) | $12.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| MINI | Tier 1 / AS3 | 2 vCore / 2GB / 60GB SSD | 8000GB Max(IN, OUT) | $21.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |
| MICRO | Tier 1 / AS3 | 4 vCore / 4GB / 80GB SSD | 16000GB Max(IN, OUT) | $32.90/月 | 可下单 · [ 查看方案](https://bit.ly/DmiT) |
| MEDIUM | Tier 1 / AS3 | 4 vCore / 8GB / 160GB SSD | 32000GB Max(IN, OUT) | $49.90/月 | 可下单 · [ 查看套餐](https://bit.ly/DmiT) |
| LARGE | Tier 1 / AS3 | 8 vCore / 16GB / 320GB SSD | 64000GB Max(IN, OUT) | $99.90/月 | 可下单 · [ 查看配置](https://bit.ly/DmiT) |
| GIANT | Tier 1 / AS3 | 8 vCore / 24GB / 640GB SSD | 128000GB Max(IN, OUT) | $199.90/月 | 可下单 · [ 查看价格](https://bit.ly/DmiT) |

东京官方当前价格页公开的是 Premium 与 Tier 1 两类，Premium 给出的中国大陆参考延迟约 28ms；官网同样强调实际延迟会随路线、访问网络和时段变化。

## 从价格看，DMIT 的“便宜”其实藏在路线选择里

把上面的套餐放在一起看，会发现一个很明显的现象：

LAX Tier 1 AS3 的 TINY 只有 **$6.90/月**，WEE 甚至是 **$36.90/年**；而 LAX Premium AN5 从 MINI 就到 **$79.90/月**，香港 Premium AN5 的 MINI 则是 **$149.90/月**。

这不是简单的“同样配置，价格差很多”。

网络等级和硬件等级同时改变了。

例如 LAX Premium 的 AN5 MINI 是 4 vCore、4GB、80GB SSD、5000GB、10Gbps，价格 $79.90；同一节点的 Tier 1 AS3 MINI 是 2 vCore、4GB、80GB SSD、8000GB Max(IN, OUT)，价格 $21.90。前者明显多花的钱，主要不是买 SSD，而是买不同的网络定位以及更高代际硬件。

所以比较 VPS 时，千万别拿 `$21.90` 和 `$79.90` 直接写成“谁性价比更高”。它们服务的是不同场景。

更合理的比较方式是：

> 中国大陆用户占大多数：先比较 Premium 与 Eyeball 的网络差异，再看 CPU 与流量。
> 全球业务、备份、开发机：先看 Tier 1 的流量与存储，再决定是否需要更高代际硬件。
> 高并发数据库或 CPU 敏感任务：优先关注 AN5 与具体 vCPU/RAM/磁盘组合。

## LAX、HKG、TYO，到底应该怎么选

这三个节点的差异，不只是“离谁更近”。

### LAX：美国业务 + 中国大陆访问的折中路线

洛杉矶是 DMIT 当前最强调全球互联能力的节点之一。官网给出的 LAX 网络聚合能力达到 **3.8Tbps**，并连接中国电信 AS4809、中国联通 AS9929、中国移动国际 AS58807，同时 Premium 路线使用 CN2 GIA。

对于中国大陆访问美国服务、跨太平洋 API、美国站点、游戏服务和跨境业务来说，LAX 的用途相对广。

近期第三方 2026 年 8 月实测也观察到，LAX Premium 在北京、上海、广州的多个 TCP 样本里，三网回程以 CN2 GIA 为主；但个别 UDP 路径和测速目标存在异常，说明“线路好”依然不等于每一个协议、每一个 ISP、每一个测速点都完全相同。

### HKG：纯中国大陆访问场景下，物理距离天然有优势

香港节点位于 Equinix HK2，官方参考延迟约 15ms 到深圳，同时给出 0.1% 以下的中国大陆参考丢包率。

但价格也明显更高。

当前 HKG Premium AN5 MINI 是 **$149.90/月**，同一节点的 Eyeball MINI 是 **$126.90/月**，Tier 1 AS3 MINI 只有 **$21.90/月**。

这里最值得注意的不是绝对价格，而是 HKG Eyeball 目前还在 Beta。拿它做实验、个人项目和对稳定性要求没那么苛刻的服务，可以把这个状态算进成本；真正生产环境则不应该忽略官网本身的提示。

### TYO：亚洲跨区域场景值得单独看

东京 Premium 当前从 $21.90/月的 TINY 起步，最高公开到 $829.90/月的 GIANT；Tier 1 则从 $6.90/月起。

东京节点对日本、韩国以及更广泛的亚太用户很自然，同时官网给出的中国大陆参考延迟约 28ms。

如果业务同时面向日本、东亚和中国大陆，东京在地理位置上通常比 LAX 更适合作为区域节点；但这句话只能作为部署思路，不应该替代真实线路测试。

## 真正做 VPS 测评，建议这样测

### 先测路由，再谈速度

可以从服务器执行基础 Ping 和 MTR：

bash
ping -c 20 目标IP
mtr -rwzc 100 目标IP


不要只测一个公共 DNS。

最好分别针对你真正的用户群，例如中国电信、中国联通、中国移动，以及实际业务所在地的公网节点。你会很快发现：平均延迟相近，不代表路径质量相同。

### CPU 不要只看 vCore 数量

VPS 的 4 vCore，并不能自动等价于另一台 VPS 的 4 vCore。

DMIT 当前 AN5 使用 EPYC 9005、AN4 使用 EPYC 9004、AS3 使用 EPYC 7003，这种硬件代际差异会直接反映在 CPU 密集型任务上。

一个基础 Linux 测试环境可以这样做：

bash
sysbench cpu --threads=$(nproc) --cpu-max-prime=20000 run


测试时不要把一次运行结果当成“永久性能”。重复几次、不同时间运行，比截一张漂亮分数图更有参考价值。

### 磁盘测试别只测顺序读写

网站、数据库、容器和编译任务通常更在乎随机 IO 和延迟。可以用 fio 做简单测试：

bash
fio --name=randread \
    --filename=testfile \
    --size=2G \
    --bs=4k \
    --iodepth=32 \
    --rw=randread \
    --direct=1 \
    --runtime=60 \
    --time_based \
    --group_reporting


尤其是 LAX AS3 当前仍处于优化阶段，官网已经明确提示磁盘性能可能下降，因此如果你的工作负载对磁盘特别敏感，不要只看 CPU 型号。

### 带宽测速要测试“你的路线”

10Gbps 端口只说明虚拟网卡或接口上限。

它不意味着：

* 中国大陆家庭用户一定能跑到 10Gbps；
* 单线程一定能跑满；
* 晚高峰一定和凌晨一样；
* 所有 ISP 和协议都走同一路由。

这正是近期 LAX 第三方测试里出现不同表现的原因之一。

### IP 质量最好独立检查

建站、邮件、流媒体、AI 平台这些场景，经常会遇到一个很现实的问题：服务器性能正常，但 IP 本身被某个平台判定为高风险、代理或数据中心 IP。

这类结果受 IP 段、第三方数据库和平台自身策略影响，不适合写成“DMIT 全部套餐都保证解锁”。本次核验也没有把某个具体流媒体或 AI 平台的解锁当成套餐级保证。

## 用户评价怎么看：有负面反馈，但样本很小

这部分尤其容易被营销文章写歪。

截至本轮检索，Trustpilot 上 DMIT 显示 **2.6/5，只有 4 条评价**；页面自己也明确提醒，这样的评价数量很少，可能不能代表全部客户。近 12 个月的评价中有多条负面反馈，集中在断线、退款和客服处理体验等问题。

另一方面，近期独立 VPS 测评并非全部负面。例如 2026 年 8 月对 LAX Premium 的网络测试，多个大陆城市的 TCP 样本确实显示出较好的优化回程，但同一测试也发现具体 UDP 路径和个别测速目标会出现明显差异。

这两类证据其实可以同时成立。

网络测试回答的是“某个时间、某台机器、某条线路表现如何”；用户评论回答的是“某些客户遇到了什么售后或服务问题”。它们不是同一种数据，不应该互相替代。

因此，DMIT 的口碑更适合写成：**网络路线方面存在不少正向实测，售后体验则存在较明显的个别负面反馈，同时公开评价样本非常有限。**

## 退款政策：购买前一定要看这几个限制

DMIT 当前官方退款文档给出的规则，比很多价格页上的一句“可退款”具体得多。

新购买的服务，在 **购买后 3 天内且 VM 流量使用不超过 30GB** 的条件下，可以申请全额退款；此外，新订单在 **30 天内** 还存在按剩余价值计算的部分退款机制。退款通常会扣除支付网关手续费。

同时也存在明确的不可退款情形，例如续费订单、部分滥用情况、某些 DDoS 或 IP 地理位置相关争议，以及重复退款等情况。

这个规则对 VPS 购买其实很实用。

因为网络路线是否适合你，很多时候不是看官方宣传就能决定，而是要在自己的运营商、自己的访问地点上实际跑一次。3 天、30GB 的窗口，至少给了测试空间。

但别理解成“先随便买，发现不喜欢都能退”。**退款有条件，而且是新购订单规则，不应该默认适用于续费。**

## 优惠码这件事，别拿旧文章里的代码直接结账

这一轮检索能找到不少所谓“永久优惠码”“2026 最新优惠”，但其中很多页面要么是第三方优惠聚合站，要么引用历史活动页，无法在 DMIT 当前官方促销页面直接核验。

DMIT 当前服务条款只确认会不定期发布折扣码，并且折扣码有适用范围限制。

因此，这篇 VPS 测评不把搜索到但无法在当前官方页面确认的折扣码写成“现行优惠”。

对买家而言，最安全的做法也很简单：**以结账时实际显示的优惠后价格为准，而不是以某篇去年文章里的“永久 7 折”作为预算依据。**

[👉 查看当前 DMIT 价格与可用库存](https://bit.ly/DmiT)

## DMIT 有没有免费版、团队版、企业版？

按当前公开 Cloud Instance 价格体系来看，并没有像一些通用云平台那样公开排列 Free、Basic、Team、Enterprise 这类套餐。

DMIT 当前把业务拆成 Cloud Instance、BareMetal、IP Transit 和 Colocation；其中本文 VPS 测评对应的是 Cloud Instance。

也就是说，不要拿“有没有免费套餐”去套它的产品逻辑。DMIT 的公开 VPS 价格主要围绕节点、网络和硬件配置展开。

这也解释了为什么它的套餐表看起来有点“工程师味”：你不是先选一个营销档位，再一步步加功能，而是先判断网络，再判断平台和资源。

## 什么类型的项目更适合用哪一档

个人博客、轻量网站、测试环境，如果用户主要在中国大陆，可以优先比较 LAX Premium AS3、LAX Eyeball AS3 和更便宜的 Tier 1；不要一上来就买最高配置。

跨境业务、API、SaaS、远程开发，更值得在 Premium 与 Eyeball 之间做路线选择。DMIT 官方对 Eyeball 的定位本身就覆盖 API、SaaS 和远程开发。

备份、归档、CI/CD、监控、全球中转这类任务，Tier 1 往往更符合“资源够用就好”的逻辑，因为这些场景不一定需要中国大陆专门优化的路由。

数据库、高并发网站、编译和 CPU 密集型应用，则应该认真看 AN5 和具体内存容量，而不是只看月租。DMIT 当前对 AN5 的定位就是更高的单核、多核以及 NVMe Gen5 存储性能。

## 最容易被忽略的三个购买细节

**第一，流量单位不一样。**

普通计划写的是 Transfer，而 Tier 1 某些方案写的是 `Max (IN, OUT)`。这会直接影响你怎么计算下载、备份和中转成本。不要把两个数字放在一起就当成同一种配额。

**第二，库存和价格会变。**

官方定价页面本身已经提示产品和价格可能因为调整而出现更新滞后，而且当前部分 LAX AN4 Premium 和 Eyeball 方案明确显示 Out of Stock。

**第三，Beta 和平台建设状态要写进购买决策。**

HKG Eyeball 是 Beta，LAX AS3 仍在建设优化，这两个状态都不是小字里的装饰信息。

## 结论：这次 VPS 测评真正值得记住的，是“先选路线，再选配置”

DMIT 当前的产品结构并不适合用一句“贵”或“便宜”概括。

它真正的定价逻辑是：

**你先为网络路线付钱，再为硬件代际付钱，最后才是 vCPU、内存、SSD 和流量。**

Premium 负责更强的中国大陆和亚太路由；Eyeball 在成本与中国访问之间做折中；Tier 1 则把重点放回全球网络、带宽和成本。硬件方面，AN5、AN4、AS3 分别对应新一代、高度成熟的通用平台以及更偏预算的方案。

真正做 VPS 测评时，与其问“DMIT 到底好不好”，不如问三个更有用的问题：

我的用户在哪里？

我的工作负载到底吃 CPU、磁盘还是网络？

我为什么需要这条更贵的路线？

答案明确之后，套餐反而会变得简单。

目前公开价格里，LAX Tier 1 AS3 可以低到 **$6.90/月**，而 LAX Premium AN5 MINI 是 **$79.90/月**；香港 Premium 的起步档又明显更贵。

这意味着所谓“VPS 性价比”，根本不是一个脱离场景的数字。

如果你需要的是中国大陆访问质量，低价国际线路省下来的钱，可能最终会花在更高的延迟、丢包和排查时间上；如果你根本不需要中国优化，那么花更多钱买 Premium 反而可能是在买用不上的东西。

[👉 查看 DMIT 当前全部 VPS 方案](https://bit.ly/DmiT)

### 常见问题

#### DMIT 的 VPS 主要优势是什么？

从当前官网产品设计看，核心优势集中在 **网络路线选择、亚太/中国大陆连接质量、AMD EPYC 硬件以及自助式 Cloud Instance**。Premium、Eyeball、Tier 1 三种线路可以让不同用途的用户按网络需求付费，而不是所有人都购买同一套网络。

#### DMIT 的 VPS 贵吗？

要看拿什么比较。

与普通国际 Tier 1 VPS 相比，Premium 线路的价格明显更高；但 DMIT 当前也提供 LAX/HKG/TYO 的 Tier 1 方案，其中部分入门配置价格很低。因此，“DMIT 贵”只适用于某些网络档位，不能套到整个产品线。

#### 中国大陆访问应该选哪条线路？

优先从 Premium、Eyeball 和 Tier 1 的网络差异开始判断。DMIT 官方对 Premium 的定位就是中国大陆和亚太访问质量；Eyeball 则是折中路线；Tier 1 不提供中国大陆专门优化。

#### HKG Eyeball 能不能用于生产环境？

官网当前仍标记为 Beta，并明确提醒产品和网络路由仍在调优，对高度依赖稳定性的生产业务不作推荐。

#### DMIT 可以退款吗？

可以，但不是“无条件退款”。新购服务在 3 天内且 VM 流量不超过 30GB 时，可申请全额退款；30 天内还存在部分退款规则，同时有续费订单和其他不可退款情形。

#### VPS 测评应该先看什么？

如果主要面向中国大陆，建议先看实际路线、延迟、丢包和高峰期稳定性；再看 CPU、磁盘、流量和价格。端口写 1Gbps 或 10Gbps，只能算配置的一部分，不能直接等同于你的最终下载速度。近期 LAX 第三方测试也观察到了不同城市、协议和测速节点之间的差异。
