# 高可用性 NAS 配置指南
## 期望受众

- 有一些 Linux 使用经验的用户

## 原则

1. 尽可能简单：无法理解的复杂系统行为可能降低可靠性
   - 使用受支持的 stable 发行版本，如 Debian stable，并日常更新
   - 软件尽可能放到 Docker 里面，并按最小权限原则运行，日常更新 base image
   - 宿主机的服务应尽可能少
2. 存储：RAID + 异地备份
   - 取决于实现，RAID 5 / RAID 6 掉盘后重建需要读取全盘，为控制总的不可恢复错误概率请谨慎计算后选择
   - 定期异地备份（e.g. 云服务，不连接电脑的磁盘），降低系统性风险
3. 监控
   - 每日发送系统状态数据到 {邮箱/微信/短信}，避免监控系统损坏而不知道情况的发生
   - 关键性能数据（CPU Load, Mem, 磁盘 I/O, 磁盘 S.M.A.R.T 信息, Uptime）和日志 dump
4. 网络安全
   - DROP 掉不需要的端口 (IPv4 和 **IPv6**)
   - 推荐 iptables 和 ip6tables，Debian 可以使用 ipconfig-persistent
   - ssh 采用 publickey 登录方式，禁用密码登录
   - 部分关键服务采用 OpenVPN 登录后可见
5. 电源安全
   - UPS 和自动关机

## 实现

### 系统配置参考

TODO