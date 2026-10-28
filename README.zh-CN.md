[English](README.md) | [简体中文](README.zh-CN.md)

# sweepsa — 免费二进制版本

一款适用于软件定义无线电的扫频频谱分析仪。在运行 Pluto 风格固件并搭载 Zynq ARM 的 **AD936x 开发板**上，它通过板载 ARM 调用芯片的 **fastlock** 配置文件来切换本振频率。桌面端提供仪器风格的前面板，包括迹线、标记、检波器、推导 RBW、保持模式、瀑布图，以及带视频触发的零扫宽模式。也可以通过电脑 USB 接口使用 **HackRF One**，并利用其固件扫频模式。

此仓库仅提供**二进制发布版本**。请从 [Releases](../../releases) 下载。

| 压缩包 | 内容 |
|---|---|
| `sweepsa-<ver>-macos-arm64.tar.gz` | `sweepui`、`sweep_client`、`launch.py`、`sweepd` |
| `sweepsa-<ver>-linux-x86_64.tar.gz` | `sweepui`、`sweep_client`、`launch.py`、`sweepd` |
| `sweepsa-<ver>-windows-x86_64.zip` | `sweepui.exe`、`sweepd` |
| `sweepsa-<ver>-sweepd-armv7.tar.gz` | 仅包含供开发板使用的 `sweepd` |
| `sweepsa-<ver>-sweepd-relink-kit.tar.gz` | `sweepd` 的 LGPL 重新链接工具包（见下文） |
| `libusb-<ver>-source.tar.bz2` | macOS 和 Windows 版本中所附 libusb 的源代码 |

## 快速开始

```sh
tar xzf sweepsa-*-macos-arm64.tar.gz && cd sweepsa-*-macos-arm64
xattr -dr com.apple.quarantine .     # 仅限 macOS：这些构建版本未经公证
./sweepui                            # 合成信号源，无需无线电设备
pip3 install --user pyserial && ./launch.py   # 通过 USB 连接开发板：部署 sweepd 并建立连接
```

使用 HackRF One：运行 `./sweepui --hackrf`。macOS 和 Windows 压缩包中附带 libhackrf；Linux 用户请安装发行版提供的 `libhackrf0`/`hackrf` 软件包。

每个压缩包内的 `README.txt` 都包含详细说明，包括手动运行方法和 macOS USB 网络连接说明。

## 扫频速度

在 AntSDR E310 和 LibreSDR（AD936x，Pluto 风格固件）上实测：

| 扫宽 | 扫频时间 |
|---|---|
| 70 MHz – 6 GHz | 约 500–800 ms |
| 数百 MHz | 约 10–60 ms |

作为对比，HackRF One 在 sweepsa 中扫完全频段约需 730 ms，两者在全频段上处于同一水平。fastlock 在 AD936x 开发板上带来的是：每段 40–56 MHz 带宽、无缝隙的快速扫频，并且由板载 ARM 完成，而不是经过 USB 或网络链路控制。

**这不是经过校准的测量仪器。** 电平单位为 dBFS；加载幅度校正之前，界面会始终显示 UNCAL（未校准）标记。

## 许可证

可免费使用并重新分发未经修改的版本。详见 [LICENSE.txt](LICENSE.txt)。
`sweepd` 与 libiio 和 glibc 静态链接（LGPL-2.1）。每个发布版本中的 `sweepd-relink-kit` 压缩包都包含目标文件、libiio 源代码，以及一个用于重新链接到修改版库的脚本。macOS 和 Windows 版本将 libhackrf（BSD-3-Clause）和 libusb（LGPL-2.1）作为独立库随附，由 `sweepui` 在运行时加载。你可以自由替换这些库；每个发布版本都附有 libusb 的源代码。

## 源代码

sweepsa 目前是免费的闭源软件，我计划在之后公开源代码。
