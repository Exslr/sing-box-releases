# sing-box-releases

English | [简体中文](README.zh-CN.md)

Automated builds of [reF1nd/sing-box](https://github.com/reF1nd/sing-box), a fork of
[sing-box](https://github.com/SagerNet/sing-box). Released artifacts are renamed from
`reF1nd` to `Exslr`; the upstream repositories, branches and source tags they are built
from keep their original names. Builds are in
[Releases](https://github.com/Exslr/sing-box-releases/releases).

> **This is a personal build, for me and a few friends.** It is not a distribution, it
> is not promoted anywhere, and it is not maintained for a wider audience — builds
> happen when I happen to run them.
>
> If you ended up here and are looking for sing-box, please get it from
> [reF1nd/sing-box](https://github.com/reF1nd/sing-box) or
> [SagerNet/sing-box](https://github.com/SagerNet/sing-box) instead. That is where the
> actual work is done, and where you will find releases that are properly maintained.
> All credit belongs to the upstream authors; this repository only runs their code
> through a build pipeline and renames the output.

## Which file do I want?

### Command line

| Platform | File |
|---|---|
| Linux x86-64 | `sing-box-<version>-linux-amd64-<variant>.tar.gz` |
| Linux ARM64 | `sing-box-<version>-linux-arm64-<variant>.tar.gz` |
| Windows | `sing-box-<version>-windows-<amd64\|amd64v3\|arm64>.zip` |
| macOS (Apple Silicon) | `sing-box-<version>-darwin-arm64.tar.gz` |

Linux ships three variants. Pick `purego` unless you know you want another:

- **purego** — no libc dependency, runs anywhere. Ships `libcronet.so` next to the
  binary; keep the two together.
- **glibc** — for regular distributions (Debian, Ubuntu, Fedora, Arch…).
- **musl** — for musl-based systems such as Alpine and OpenWrt.

`amd64v3` targets Haswell (2013) and newer CPUs. The plain `amd64` build runs on any
x86-64 machine.

Intel Macs are not built. macOS on Apple Silicon can run the `darwin-arm64` binary
natively.

### Android

| File | Use it when |
|---|---|
| `SFA-<version>-universal.apk` | You are not sure — works on every supported device |
| `SFA-<version>-arm64-v8a.apk` | 64-bit ARM, i.e. essentially every phone since 2019 |
| `SFA-<version>-armeabi-v7a.apk` | Older 32-bit ARM devices |

x86 and x86_64 APKs are not published, so emulators are not supported.

### Windows desktop client

| File | Use it when |
|---|---|
| `SFW-<version>-x64.exe` | Intel or AMD |
| `SFW-<version>-arm64.exe` | Snapdragon and other ARM devices |

32-bit x86 is not built.

## Code signing

The Windows installer is signed with a **self-signed certificate**, so Windows
SmartScreen shows an "unknown publisher" warning on first run. Choose *More info* →
*Run anyway*, or add the certificate to your Trusted Publishers to silence it
permanently. Android APKs are signed with a private keystore, which is how every
Android app is signed — nothing extra to do there.

## Relationship to upstream

Only the version string is renamed: `1.14.1-reF1nd` upstream becomes `1.14.1-Exslr`
here. Source is always fetched from `reF1nd/sing-box` by its original tag.

The Windows desktop client also renames its install directory, service and IPC
endpoint, so **it cannot be installed alongside the upstream reF1nd build** — the two
would fight over the same TUN device. Uninstall `sing-box-reF1nd` before installing
`sing-box-Exslr`.

Builds are triggered manually. `build-stable.yml` tracks the `reF1nd-stable` branch and
publishes a release; `build-testing.yml` tracks `reF1nd-testing` and publishes a
pre-release. Released files carry GitHub build provenance attestations and can be
verified against this repository:

```
gh attestation verify <file> --repo Exslr/sing-box-releases
```

## License

[GPL-3.0-or-later](LICENSE), inherited from sing-box. This repository contains build
automation only.
