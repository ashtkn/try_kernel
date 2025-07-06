# Interface TryKernel

[Interface 2023年7月号 特集「ゼロから作るOS」](https://github.com/ytoyoyama/interface_trykernel)勉強用

## 開発環境

### 共通

[Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)をダウンロードし，`bin`ディレクトリへの絶対パスを`GCC_PATH`環境変数として設定してください。
また，[Raspberry Pi Pico SDK](https://github.com/raspberrypi/pico-sdk)をダウンロードし，`pico-sdk`ディレクトリへの絶対パスを`PICO_SDK_PATH`環境変数として設定してください。

### Windows

以下のソフトウェアをダウンロードしてパスを通してください。

- [Make for Windows](https://gnuwin32.sourceforge.net/packages/make.htm)
- [LibIntl for Windows](https://gnuwin32.sourceforge.net/packages/libintl.htm)
- [LibIconv for Windows](https://gnuwin32.sourceforge.net/packages/libiconv.htm)
- [OpenOCD](https://github.com/ciniml/debug-tools-builder/tree/v1.3)
- [LLVM](https://github.com/llvm/llvm-project/releases)

### Mac / Linux

`Make`，`OpenOCD`，`LLVM`をインストールしてください。

## デバッガ

VSCode上でF5キーを押してください。
