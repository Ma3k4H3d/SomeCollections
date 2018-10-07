# 以全新的视角来评测公共 CDN

之前在 V2EX 上看到这篇[「用程序猿视野看公共 CDN」](https://www.v2ex.com/t/475746)，感觉写的不仅不详细，还有很多纰漏和错误。可是嘲笑别人写得不好，总得自己写篇更好的才行嘛，所以我就写了这篇对公共 CDN 的评测。

## 参与评测的公共 CDN 服务商

首先，入选的公共 CDN 都必须是积极更新、积极维护的，意味着新浪、百度、又拍 JSCDN 之流是不参与评测的。

* ~~**BootCSS** 国内最著名、使用最广泛的公共 CDN 之一
* **css.loli.net** 由土豪兽兽维护的公共 CDN，`css.net` 的船新升级版本
* **Staticfile** 由七牛维护的公共 CDN 服务
* **75CDN** 由 360 的奇舞团运营的公共 CDN
* **今日头条公共 CDN**
* **jsDelivr** 由 Prospect One 运营，非常快速和非常可靠的公共 CDN
* **CDNJS** 非常著名的公共 CDN，国内大部分公共 CDN 都是和它维护的库同步
* **Unpkg** 著名的公共 CDN，从 NPM 抓取 Package 中的文件
* **Bootstrap CDN** Bootstrap 官方推荐的公共 CDN

## 评测角度

* **HTTPS 和 HTTP2**
* **服务商** 直接关系到公共 CDN 的质量和 SLA
* **节点数量和质量** 关系到终端用户的速度

> 海外的公共 CDN 服务商和中国的公共 CDN 服务商的评判方法不同，中国的从 国内节点 和 海外节点 来衡量，海外的从 全球节点 和 中国节点 来衡量

* **加载速度** 从国内和海外两个部分衡量
* **服务域名和使用的权威 DNS** 决定了公共 CDN 的 SLA 和解析速度

> 公共 CDN 由于频繁调用，解析结果绝大部分都会被递归 DNS 缓存，解析速度受权威 DNS 影响不大；但是通过使用的权威 DNS 也可以看出公共 CDN 服务商的投入多少

* **便捷性** 是否方便开发者使用

> 比如是否提供 Lib 库搜索、是否支持一键复制 URL 或者标签

* * *

注意，本文不会提供类似 ping 速度或者 IP 数量这类数据，因为这些并不是衡量公共 CDN 的标准。

## BootCDN

[官网](https://www.bootcdn.cn/)

* 支持 HTTPS，支持 HTTP2
* 京东云 CDN
* 丰富的国内节点
* 没有海外节点
* 在国内速度还不错，海外的话不敢苟同
* `cdn.bootcss.com`，使用 DNSPod 免费版
* 便捷性：★★★★★

> 开放 API；提供搜索引擎索引；支持一键复制标签和 URL

~~BootCDN 是国内使用最广泛的公共 CDN。BootCDN 之前和又拍云合作。虽然又拍云与其他 CDN 相比有些亮点（WebP 和 H264 自适应、TLS1.3 等），但节点质量实在不敢恭维，海外也只有香港、新加坡、北美、荷兰四个节点（法兰克福被去掉了）。BootCDN 的官方博客还 [记录了一次事故](https://blog.bootcdn.cn/bootcdn-suffered-cc-attack/)，大意是 CC 攻击使得又拍云封禁了不少 BootCDN 的 URL。~~

~~不知道是又拍不再赞助、还是服务质量不能满足需要，BootCDN 今年切换到了京东云 CDN。京东云 CDN 在国内的节点还算数量丰富、覆盖范围也比又拍云好；但是京东云没分配海外节点给 BootCDN，海外会解析到上海电信节点。~~

~~关于 BootCDN 使用 DNSPod 免费版，我个人觉得作为国内使用如此广泛的公共 CDN 用免费版的 DNSPod，毕竟不能保障 SLA；但是话说回来，公共 CDN 毕竟也是免费服务，还是别多嘴了。~~

毫无征兆地，中国最著名的公共 CDN 服务提供商 [BootCDN 于 2018 年 10 月 1 日停止了服务](https://www.v2ex.com/t/494375)。

## css.loli.net

[官网](https://css.loli.net/)

* 支持 HTTPS，支持 HTTP2
* 国内使用阿里云 CDN，海外使用 Cloudflare（Pro Plan）
* 非常丰富的国内节点
* 丰富的海外节点
* 全球速度都很好
* `*.loli.net`，自建权威 DNS
* 便捷性：★★

> 不支持一键复制；至于搜索，可以在 `https://cdnjs.loli.net/ajax/libs/` 用 Ctrl / Coomand + F；

css.loli.net 除了同步 cdnjs 的库，还提供 Google Fonts 和 Gravatar 等服务的反代。

css.loli.net 的前身是兽兽的 `css.net`，后来兽兽改用 `cat.net` 几个子域名，直到现在的 `loli.net`；使用了阿里云 CDN + Cloudflare Pro Plan，全球速度都不错（虽然 Cloudflare 钱不加够是不会分配全部 150 节点的，但是 Pro 已经可以覆盖大部分地区了）。至于自建 DNS，兽兽曾透露过他们每天解析请求多达数十亿，一般的 DNS 服务商不划算。

说到便捷性，css.loli.net 只是提供加速服务，并没有提供类似搜索或者一键复制的功能，而是让开发者将现有的海外公共 CDN 的域名替换为他们的服务域名；虽然数次更换域名难免造成一些不便，但是我依然主力推荐兽兽的公共 CDN 服务。

## Staticfile

[官网](https://staticfile.org/)

* 支持 HTTPS，**不一定** 支持 HTTP2
* 著名的二手 CDN 贩子七牛云 CDN，上游说不准是哪个
* 丰富的国内节点
* **很可能没有** 海外节点
* 国内的速度还是不错的
* `cdn.staticfile.org`，DNSPod 免费版

> 怎么又是 DNSPod 免费版？

* 便捷性：★★★★

> 有搜索引擎，支持一键复制文件 URL

和别的公共 CDN 同步 CDNJS 的 Lib 库不同，Staticfile 自己维护了一个 Lib 库，曾经断更过一年（那时候经常没法用最新版本的库），不过现在继续维护了。

Staticfile 用的 CDN 是七牛。七牛的计费系统曾是 V2EX 工单板块的常客，七牛的配置更新是用来衡量咕咕咕的单位，人们像买彩票一样看七牛会分配哪个上游 CDN，至今坊间依然在流传七牛人工向上游服务商手动提交客户的 SSL。当然我这篇文章并不是为了黑七牛，所以赶紧言归正传。七牛之前给 Staticfile 分配了网宿，所以没有 HTTP2 但是有海外节点，之后全面切换到又拍云、有了 HTTP2 但是海外只剩一个法兰克福，现在新分配了阿里云 CDN 但是没了海外节点，颇有些让人哭笑不得。

即便如此，Staticfile 还算是不错的公共库，加上 Staticfile 诞生比 BootCDN 要早，所以在国内使用也非常广泛。

## 75CDN

[官网](https://cdn.baomitu.com/)

* 支持 HTTPS，支持 HTTP2，提供 SRI（[开启 SRI 教程](https://75team.com/post/75cdn-sri.html)）
* 360 自家服务同款 CDN
* 丰富的国内节点
* 有几个海外节点
* 国内的速度还是不错的
* `lib.baomitu.com`，360 官网同款 DNS
* 便捷性：★★★★★

> 有搜索引擎，支持一键复制文件 URL 和标签

75CDN 是 360 前端团队奇舞团维护的，除了同步 CDNJS 以外，还提供 Google Fonts 本土化（不是单纯的反代）。75CDN 号称首个支持 HTTP2 和 SRI 的公共 CDN（考虑到大前提是在国内的话，还是挺正确的），除此以外还率先支持 ES Module Import，走在了各大公共 CDN 前列。
从服务质量上来看，75CDN 使用的 360 自家服务同款 CDN 和权威 DNS，速度和 SLA 肯定不会低于 BootCDN 或者 Staticfile；但是海外节点目前就香港和北美，聊胜于无。

## 今日头条公共 CDN

[官网](https://cdn.bytedance.com/)

* 支持 HTTPS，**不一定** 支持 HTTP2
* 著名的二手 CDN 贩子七牛云 CDN，上游说不准是哪个
* 丰富的国内节点
* **大量的** 海外节点（s4 子域名除外）
* 全球的速度都不错的
* `s1.pstatp.com` `s2.pstatp.com` `s3.pstatp.com` `s4.pstatp.com`，DNSPod 免费版

> 怎么还是 DNSPod 免费版？

* 便捷性：★★★★★

> 有搜索引擎，提供文件 URL，支持设置缓存响应头时长

说实在的，其实今日头条的公共 CDN（由母公司字节跳动的团队负责运营）本来不应该入选评测的——上游同样是 CDNJS，但是并没有定时同步了，`jquery` 才更新到 `3.2.1`，还大字写了个什么禁止非法网站调用啥的。但是之所以还要再补充关于它的说明主要是这个公共 CDN 非常有趣。
首先他不是直接给你直链，你点击文件以后跳转的链接是随机分配的，可能是受到早期前端优化中域名分片的影响、以及间接实现在多家 CDN 之间的负载均衡吧。s1 域名接的是网宿 CDN，全球版，海外除了网宿自己的节点以外还有 cdnetworks 的节点；s2 和 s3 阿里云 CDN 全球版，海外节点也很丰富的；只有 s4 域名接的是网宿国内版。除此以外还支持指定响应头缓存时长（URL 中有参数）也非常有趣——明明公共库文件都是长期不改变的，直接设置一年甚至两年的 `cache-control` 就行了的。
虽然这个公共库处于年久失修的状态，但是考虑到它接的 CDN 上游都挺有趣的，还是可以考虑体验一下的，但是如果要用于生产环境的话还是留个心眼比较好。

## jsDelivr

[官网](https://www.jsdelivr.com/)

* 支持 HTTPS，支持 HTTP2，提供 SRI
* 网宿、Fastly、Stackpath、Cloudflare Business Plan
* 非常丰富的国内节点
* 非常丰富的海外节点
* 全球的速度都非常优秀
* `cdn.jsdelivr.net`，NS1 和 Rage4 主从 DNS
* 便捷性：★★★★★

> 有搜索引擎，支持一键复制文件 URL 和标签，支持分发 NPM、GitHub、WordPress SVN 的文件

如果有人让我推荐公共 CDN，我一定会推荐 jsDelivr。通过 RUM 实时监测各地服务质量、调度多家 CDN 保障全球加载速度；拥有多层缓存和灾备保障 100 SLA。更重要的是 jsDelivr 有 ICP 备案、接入网宿，很可能是海外公共 CDN 服务中唯一提供中国节点的。

jsDelivr 支持从 NPM、GitHub Tag 和 WordPress SVN 上抓取文件并分发，大大降低了开发者使用的难度——直接发个 Release 就可以用了。jsDelivr 每个月会被调用上百亿次，服务 620+ TB 的流量，意味着如果你不是通过 jsDelivr 加载较为热门的库，那么缓存命中率是不会太理想的。

之前网宿的杭州节点遭到入侵，一干二手 CDN 都被 MITM，jsDelivr 也受到影响、不得不切走网宿，不过问题解决以后又切回来了。这也算是 jsDelivr 的一次事故吧，虽然锅得网宿背；过了一年 jsDelivr 的 GSLB 服务商 Cedexis 又出现故障、不得不暂时将全部解析至 Cloudflare。但不管怎么说，jsDelivr 总体上仍然是非常优秀、SLA 100、值得在生产环境上使用的公共 CDN。

## CDNJS

[官网](https://cdnjs.com/)

* 支持 HTTPS，支持 HTTP2，提供 SRI
* Cloudflare Enterprise Plan
* 没有国内节点（ cloudfalre.com 肯定不会备案，所以没法启用 China Access）
* 非常丰富的海外节点
* 国内的速度很不理想
* 海外的速度非常优秀
* `cdnjs.cloudflare.com`，Cloudflare 官网同款 DNS
* 便捷性：★★★★

> 有搜索引擎，支持一键复制文件 URL 和标签

与其说 CDNJS 是世界上最广泛使用的公共 CDN 服务，或者去探讨 Cloudflare 在海外的加速效果，还不如提一下 CDNJS 对其它公共 CDN 服务的贡献——正如我在前面介绍的那样，国内很多公共 CDN 服务都是在同步 CDNJS 维护的 Lib 库。

CDNJS 的 CDN 由 Cloudflare 赞助，和 Cloudflare 官网同级别的（Enterprise Plan）服务。当然由于众所周知的原因，肯定不推荐面向国内的站点使用这家公共 CDN。考虑一下自己站点访客的主要来源，你会从 CDNJS 的几个镜像中挑选出符合需求的。

## Unpkg

[官网](https://unpkg.com/)

* 支持 HTTPS，支持 HTTP2
* Cloudflare Free Plan
* 没有国内节点
* 非常丰富的海外节点
* 国内的速度很不理想
* 海外的速度非常优秀
* `unpkg.com`，Cloudflare DNS
* 便捷性：★★★

> 有搜索引擎，抓取并分发 NPM 包的文件

开源库、开源框架如果在文档的「Getting Started」中提到 CDN 的话，大多都会提一笔如何使用 Unpkg 加载。前身是 `npmcdn.com` 的 Unpkg 是最早分发 NPM 包的文件的公共 CDN，受到很多开发者的喜爱——Unpkg 可以很方便的直接使用指定版本的开源库。

不过由于 Unpkg 也是使用的 Cloudflare，在国内的速度并不理想，所以开发者大多都是用 Unpkg 开发和测试，并不会用在生产环境部署。国内也有一些 Unpkg 的镜像，但是我还是觉得 jsDelivr 更好用一些。

## Bootstrap CDN

[官网](https://www.bootstrapcdn.com/)

* 支持 HTTPS，支持 HTTP2
* MaxCDN、Stackpath
* 没有国内节点
* 丰富的海外节点
* 国内的速度不太理想
* 不错的海外的速度
* `stackpath.bootstrapcdn.com` `maxcdn.bootstrapcdn.com`，Route53 和 NS1 主从 DNS
* 便捷性：★★★

> 支持一键复制文件 URL 和标签

Bootstrap CDN 是 Bootstrap 官方推荐使用的公共 CDN 服务，因此虽然只提供 Bootstrap、Font Awesome 和 Bootswatch 三个库的加速服务，但是使用人数众多，每月流量消耗都已经达到 PB 级别。

之前 Bootstrap CDN 由 MaxCDN 赞助，后来 Stackpath 合并了 MaxCDN 以后继续提供赞助；两个域名都可以正常使用。国内速度虽然略好于 Cloudflare，但是依然不理想，所以面向国内的站点也不推荐取用 Bootstrap CDN。

> **本文作者  : Sukka**
> **本文采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh) 许可协议。转载和引用时请注意遵守协议！**
> **本文链接  : **[https://blog.skk.moe/post/public-cdn-in-diffrent-views/](https://blog.skk.moe/post/public-cdn-in-diffrent-views/)

本文发表于 2018-08-15 , 最后修改于 2018-09-19

