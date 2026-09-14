# 现场发现

## 配置与企业参数

从应用“打开配置目录”、进程参数和日志定位当前实例，建立“应用设置/覆写 → 合成配置 → 内核”的映射。核实全局与单订阅覆写顺序、列表追加或替换，以及脚本是否再次改写结果。

企业域名和网段优先取自企业文档、VPN 分域配置与用户确认；企业 DNS 还需验证当前网络下可达且能解析目标。单个主机或 IP 不能证明整个父域或大网段都属于企业。

读取配置只提取必要字段；保留本地控制通道的监听和鉴权边界，避免凭据进入日志、命令历史或仓库。

## 平台命令

仅探测相关目标，按本机可用工具选择：

| 平台 | DNS | 路由/接口 |
| --- | --- | --- |
| macOS | `scutil --dns`；`dscacheutil -q host -a name <FQDN>` | `route -n get <IP>`；`ifconfig` |
| Linux | `resolvectl status`；`resolvectl query <FQDN>`；`getent ahosts <FQDN>` | `ip route get <IPv4>`；`ip -6 route get <IPv6>`；`ip addr` |
| Windows | `Get-DnsClientServerAddress`；`Get-DnsClientNrptPolicy`；`Resolve-DnsName <FQDN>` | `Find-NetRoute -RemoteIPAddress <IP>`；`Get-NetIPConfiguration` |

指定 DNS 查询可用 `dig @<DNS-IP> <FQDN> A` / `AAAA` 或 `Resolve-DnsName <FQDN> -Server <DNS-IP>`。它只证明该解析器的响应，不证明系统或应用采用了它；`dig` 也未必遵循系统分域策略。

端口测试用 `nc -vz <host> <port>` 或 `Test-NetConnection <host> -Port <port>`；HTTP 使用带超时的 `curl` 并保留 TLS 校验。按需比较默认请求与临时绕过 HTTP 代理的请求，后者仍可能进入 TUN。

## 判断线索

- 企业 DNS/目标无路由：先恢复办公网或企业 VPN，Clash 分流不能补足连通性。
- 企业 DNS 正确、应用解析错误：检查系统分域策略、Clash DNS 接管、应用 DoH 和缓存。
- 返回活动 fake-ip 范围内地址：检查过滤模式和最终过滤结果。
- 真实 IP 可达但业务失败：检查实际规则命中、代理环境、TLS 和鉴权。
- IPv4 正常而 IPv6 失败：核查 AAAA 与 IPv6 路由，缩小修复范围。

保留正在承载内网流量的隧道。VPN CLI 状态、接口名、公网系统 DNS 和诊断 warning 均是线索，不是业务失败的充分证据。
