# sing-box-releases

[English](README.md) | 简体中文

[reF1nd/sing-box](https://github.com/reF1nd/sing-box) 的自动构建。该项目是
[sing-box](https://github.com/SagerNet/sing-box) 的一个分支。发布的产物名称由
`reF1nd` 改为 `Exslr`,构建所依据的上游仓库、分支和源码标签保持原名。

构建产物见 [Releases](https://github.com/Exslr/sing-box-releases/releases)。

## 该下载哪个?

### 命令行

| 平台 | 文件 |
|---|---|
| Linux x86-64 | `sing-box-<版本>-linux-amd64-<变体>.tar.gz` |
| Linux ARM64 | `sing-box-<版本>-linux-arm64-<变体>.tar.gz` |
| Windows | `sing-box-<版本>-windows-<amd64\|amd64v3\|arm64>.zip` |
| macOS(Apple 芯片) | `sing-box-<版本>-darwin-arm64.tar.gz` |

Linux 提供三种变体,不确定就选 `purego`:

- **purego** — 不依赖 libc,任何发行版都能跑。压缩包内附带 `libcronet.so`,
  请与主程序放在一起。
- **glibc** — 适用于常规发行版(Debian、Ubuntu、Fedora、Arch 等)。
- **musl** — 适用于 Alpine、OpenWrt 等基于 musl 的系统。

`amd64v3` 针对 Haswell(2013 年)及更新的 CPU 做了指令集优化;普通 `amd64`
版本可在任意 x86-64 机器上运行。

不提供 Intel 芯片的 Mac 构建。Apple 芯片的 macOS 直接使用 `darwin-arm64` 即可。

### Android

| 文件 | 适用情况 |
|---|---|
| `SFA-<版本>-universal.apk` | 拿不准就用这个,所有受支持的设备都能装 |
| `SFA-<版本>-arm64-v8a.apk` | 64 位 ARM,2019 年之后的手机基本都是 |
| `SFA-<版本>-armeabi-v7a.apk` | 较老的 32 位 ARM 设备 |

不发布 x86 与 x86_64 的 APK,因此不支持模拟器。

### Windows 桌面客户端

| 文件 | 适用情况 |
|---|---|
| `SFW-<版本>-x64.exe` | Intel 或 AMD |
| `SFW-<版本>-arm64.exe` | 骁龙等 ARM 设备 |

不提供 32 位 x86 版本。

## 代码签名

Windows 安装包使用**自签名证书**,因此首次运行时 SmartScreen 会提示"未知发布者"。
点击 *更多信息* → *仍要运行* 即可;也可以把证书加入"受信任的发布者"来彻底消除提示。
Android APK 使用私有 keystore 签名 —— 所有 Android 应用都是这样签的,无需额外处理。

## 与上游的关系

仅重命名版本号:上游的 `1.14.1-reF1nd` 在这里是 `1.14.1-Exslr`。源码始终按原始标签
从 `reF1nd/sing-box` 拉取。

Windows 桌面客户端还重命名了安装目录、系统服务和进程间通信端点,因此
**无法与上游 reF1nd 版本共存** —— 两者会争抢同一个 TUN 设备。安装
`sing-box-Exslr` 前请先卸载 `sing-box-reF1nd`。

构建为手动触发。`build-stable.yml` 跟踪 `reF1nd-stable` 分支并发布正式版,
`build-testing.yml` 跟踪 `reF1nd-testing` 分支并发布预发布版。发布的文件均带有
GitHub 构建来源证明(build provenance attestation),可对照本仓库验证:

```
gh attestation verify <文件> --repo Exslr/sing-box-releases
```

## 许可证

[GPL-3.0-or-later](LICENSE),继承自 sing-box。本仓库仅包含构建流程,
所有源代码均归上游项目所有。
