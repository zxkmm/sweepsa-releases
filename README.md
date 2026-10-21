[English](README.md) | [简体中文](README.zh-CN.md)

# About Open Source

I've been building free and open-source software and hardware for years, and I've learned a lot of what would happen if blindly open now.

To the best of my knowledge, this project respects the licenses of the libraries it uses.

I've put a lot of time into this project, and I want to keep maintaining it for as long as I can. My concern is that if I open-source it now, someone could take the code, sell a modified version, and get famous and rich off it, while nobody ever hears about me or this original repo.

**And this software is already free anyway**

So before releasing the source, I'd like the project (and me) to gain a bit more visibility first. Here's my promise: **once this repo reaches 1,000 stars, I'll open-source it.**

# sweepsa — free binaries

A swept spectrum analyzer for software-defined radios. On **AD936x boards
running Pluto-style firmware** with a Zynq ARM, it hops the LO with the chip's
**fastlock** profiles from the board's own ARM. The desktop shows an
instrument-style front panel: traces, markers, detectors, derived RBW, hold
modes, a waterfall, and zero span with a video trigger. A **HackRF One** on
your computer's USB works too, using its firmware sweep mode.

This repository only hosts the **binary releases**. Download one from
[Releases](../../releases).

| archive | contents |
|---|---|
| `sweepsa-<ver>-macos-arm64.tar.gz` | `sweepui`, `sweep_client`, `launch.py`, `sweepd` |
| `sweepsa-<ver>-linux-x86_64.tar.gz` | `sweepui`, `sweep_client`, `launch.py`, `sweepd` |
| `sweepsa-<ver>-windows-x86_64.zip` | `sweepui.exe`, `sweepd` |
| `sweepsa-<ver>-sweepd-armv7.tar.gz` | `sweepd` alone, for the board |
| `sweepsa-<ver>-sweepd-relink-kit.tar.gz` | LGPL relink kit for `sweepd` (see below) |
| `libusb-<ver>-source.tar.bz2` | source of the libusb shipped with the macOS and Windows builds |

## Quick start

```sh
tar xzf sweepsa-*-macos-arm64.tar.gz && cd sweepsa-*-macos-arm64
xattr -dr com.apple.quarantine .     # macOS only: these builds are not notarized
./sweepui                            # synthetic source, no radio needed
pip3 install --user pyserial && ./launch.py   # board on USB: deploy sweepd and connect
```

HackRF One: `./sweepui --hackrf`. libhackrf ships in the macOS and Windows
archives; on Linux install your distribution's `libhackrf0`/`hackrf` package.

`README.txt` in each archive has the details, including how to run by hand
and the macOS USB networking note.

**Not a calibrated instrument.** Levels are dBFS, and an UNCAL badge stays lit,
until you load an amplitude correction.

## Licence

Free to use and to redistribute unmodified. See [LICENSE.txt](LICENSE.txt).
`sweepd` is statically linked against libiio and glibc (LGPL-2.1). The
`sweepd-relink-kit` archive in every release holds the object files, the libiio
source and a script to relink against modified versions of those libraries.
The macOS and Windows builds ship libhackrf (BSD-3-Clause) and libusb
(LGPL-2.1) as separate libraries that `sweepui` loads at run time. Replace them
freely; libusb's source is attached to every release.
