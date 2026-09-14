# 配置与验收

## 按证据选字段

以下为常见 Mihomo 语义；不确定时核对当前版本的官方文档或本机帮助。

| 问题 | 候选修改 | 边界 |
| --- | --- | --- |
| 企业域名需返回真实 IP | `dns.fake-ip-filter` | 先确认过滤模式；blacklist、whitelist、rule 的语义不同 |
| 企业域名发往错误 DNS | `dns.nameserver-policy` 指向可达企业 DNS | 保留其他域的解析路径 |
| 企业流量命中代理 | 前置精确 `DOMAIN` 或已确认范围的 `DOMAIN-SUFFIX` DIRECT | fake-ip 排除不决定分流 |
| 按 IP 访问的企业目标被代理 | 必要的 `IP-CIDR` / `IP-CIDR6` DIRECT | `no-resolve` 不主动解析域名，不能替代域名规则 |
| DIRECT 二次解析绕过策略 | 检查 `direct-nameserver` 和版本支持的 `direct-nameserver-follow-policy` | 验证实际解析路径 |
| 未代理应用确需接管 | 评估 TUN、DNS hijack 与路由 | 单独授权并验证 VPN 兼容性 |

企业 DNS 默认只用于分域策略；加入全局 `nameserver`、`fallback` 或 `direct-nameserver` 可能将无关查询发往企业 DNS，需说明影响。启用 DNS `respect-rules` 或上游代理时，追踪 DNS 请求自身的路径，避免解析与代理连接形成循环依赖。

RFC1918 地址不等于企业归属，`11.0.0.0/8` 不是私网，`198.18.0.0/15` 常用于 fake-ip；按证据选择必要范围，而非整体设为企业 DIRECT。

## 最终配置示例

仅展示形状，不是覆盖模板。替换文档占位值，保留现有无关字段；实际覆写语法依应用版本而定。`+.corp.example` 的匹配语义需当前内核支持，单个主机用精确匹配。

```yaml
dns:
  # 仅适用于 blacklist 排除语义
  fake-ip-filter:
    - '+.corp.example'
  nameserver-policy:
    '+.corp.example': ['192.0.2.53']
rules:
  # 放在会截获该域的规则之前
  - DOMAIN-SUFFIX,corp.example,DIRECT
```

## 应用与验收

常见校验命令为 `<kernel> -t -f <candidate.yaml>`，使用实际运行内核，并按现有启动方式提供资源目录。校验对象是完整合成配置，不是 merge 片段。

优先用应用支持的重载入口；直接调用 API 前核实当前实例、协议及鉴权。API 重载不代表持久化成功，`/configs` 也未必暴露完整 DNS/规则，需结合生成配置和请求结果确认。

验收覆盖以下结果：

- 企业 DNS、系统及实际应用解析符合预期；要求真实 IP 时不落入活动 fake-ip 范围。
- 目标命中预期 DIRECT，实际办公网/VPN 路径和必要 IPv6 路径可达。
- 目标端口、用户原始业务及原先可用的公网/代理目标通过。302/401 只证明服务响应，不代表业务成功。
- 经应用重新生成后，补丁仍在且目标复测通过。

怀疑缓存时先用新进程重试，扩大清理范围前确认影响。回滚恢复持久化来源再生成和重载，仅恢复运行 YAML 可能再次丢失；恢复失败应保留备份并报告未生效状态。
