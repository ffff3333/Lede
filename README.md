# x86_64 OpenWrt 固件（自动构建）

基于 [OpenWrt 25.12](https://github.com/openwrt/openwrt/tree/openwrt-25.12) 的 x86_64 自用固件，通过 GitHub Actions 每周六自动编译并发布 Release。

## 特性

- **平台**：x86_64 通用（虚拟机 + 主流物理机）
- **镜像格式**：SquashFS + Ext4，GZIP 压缩，GRUB BIOS/EFI 双引导
- **代理**：OpenClash、Passwall、cloudflared（Zero Trust）
- **VPN**：OpenVPN、WireGuard
- **主题**：Argon（含中文语言包）
- **安全强化**：
  - 内核：Stack Protector (Strong)、KPTI、Hardened Usercopy、SLAB Freelist Random/Hardened、Structleak/Stackleak GCC 插件
  - 防火墙：firewall4 + nftables（含硬件 offload）
  - banIP 黑名单、fail2ban
- **网络驱动**：e1000/e1000e/igb/igc/r8169/vmxnet3/virtio
- **监控**：Netdata、Statistics、nlbwmon 流量监控
- **其他**：SQM 流量整形、DDNS、ACME 自动证书、ttyd 网页终端、attendedsysupgrade 在线升级

## 默认设置

| 项目 | 值 |
|---|---|
| 管理 IP | `192.168.100.1` |
| 分区 | 内核 128MB / 根分区 1GB |
| 包管理器 | apk（25.12 新默认） |
| 时区 | Asia/Shanghai |

## 使用

### 下载固件

前往 [Releases](../../releases) 页面下载最新固件：

- `*-squashfs-combined-efi.img.gz` — UEFI 引导（推荐）
- `*-squashfs-combined.img.gz` — 传统 BIOS 引导

解压后写入盘/U 盘即可：

```bash
gzip -d openwrt-*-x86-64-generic-squashfs-combined-efi.img.gz
# 物理机（假设目标盘为 /dev/sdX）
sudo dd if=openwrt-*.img.gz of=/dev/sdX bs=4M conv=fsync
# PVE / ESXi 可直接转换 img 为 vmdk 使用
```

### 手动触发构建

Actions → Openwrt Builder → Run workflow。定时构建为每周六 UTC 10:00（北京时间 18:00）。

## 致谢

感谢 [P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)、[vernesong/OpenClash](https://github.com/vernesong/OpenClash)、[Openwrt-Passwall](https://github.com/Openwrt-Passwall) 及所有相关开源项目作者！

## License

[MIT](LICENSE)
