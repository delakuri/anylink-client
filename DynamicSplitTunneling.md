## 动态拆分隧道

本项目支持根据域名动态拆分隧道（Dynamic Split Tunneling），分为域名包含或者域名排除两种方式，二者不能同时使用，仅可使用一种方案，

- 域名包含：仅指定的域名流量走VPN，未指定的域名流量不使用VPN
- 域名排除：默认全部流量走VPN，仅指定的域名不使用VPN

两种方式均支持顶级域名下的子域名自动生效，比如若指定 xyz.com ，则 `www.xyz.com`、`img.xyz.com` 等子域名自动使用相应的路由方案。

由于需要根据 DNS 流量进行动态分析，需要服务端下发 DNS ，本客户端自动将 DNS 加入包含路由，即 DNS 会走 VPN（思科 anyconnect 客户端可能会安装系统级别的全局流量过滤服务，DNS 可以不放在包含路由内），无论哪种客户端，都具有一定的额外开销，且不支持手机端，因此，仅推荐在必要的情况下使用动态域名分流。

具体使用可参考 [AnyLink](https://github.com/bjdgyc/anylink) 服务端后台配置，需要说明的是，由于路由设置中如果包含路由为空或者 all，则为全局路由，因此若使用域名包含方案，路由设置那里至少应该随便填写一个不为 all 的路由。