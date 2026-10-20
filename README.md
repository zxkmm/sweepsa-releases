# sweepsa — free binaries

A swept spectrum analyzer for the **AntSDR E310** (Zynq-7020 + AD936x). It hops
the LO with the chip's **fastlock** profiles from the board's own ARM, and the
desktop shows an instrument-style front panel: traces, markers, detectors,
derived RBW, hold modes, a waterfall, and zero span with a video trigger.

This repository only hosts the **binary releases**. Download one from
[Releases](../../releases).

| archive | contents |
|---|---|
| `sweepsa-<ver>-macos-arm64.tar.gz` | `sweepui`, `sweep_client`, `launch.py`, `sweepd` |
| `sweepsa-<ver>-linux-x86_64.tar.gz` | `sweepui`, `sweep_client`, `launch.py`, `sweepd` |
| `sweepsa-<ver>-windows-x86_64.zip` | `sweepui.exe`, `sweepd` |
| `sweepsa-<ver>-sweepd-armv7.tar.gz` | `sweepd` alone, for the board |
| `sweepsa-<ver>-sweepd-relink-kit.tar.gz` | LGPL relink kit for `sweepd` (see below) |

## Quick start

```sh
tar xzf sweepsa-*-macos-arm64.tar.gz && cd sweepsa-*-macos-arm64
xattr -dr com.apple.quarantine .     # macOS only: these builds are not notarized
./sweepui                            # synthetic source, no radio needed
pip3 install --user pyserial && ./launch.py   # E310 on USB: deploy sweepd and connect
```

`README.txt` in each archive has the details, including how to run by hand
and the macOS USB networking note.

**Not a calibrated instrument.** Levels are dBFS, and an UNCAL badge stays lit,
until you load an amplitude correction.

## Licence

Free to use and to redistribute unmodified. See [LICENSE.txt](LICENSE.txt).
`sweepd` is statically linked against libiio and glibc (LGPL-2.1). The
`sweepd-relink-kit` archive in every release holds the object files, the libiio
source and a script to relink against modified versions of those libraries.
