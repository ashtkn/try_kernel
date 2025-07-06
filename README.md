# Interface TryKernel

[Interface 2023年7月号 特集「ゼロから作るOS」](https://github.com/ytoyoyama/interface_trykernel)勉強用

## 開発環境

## Windows

以下のソフトウェアをダウンロードしてパスを通してください。

- [Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
- [Make for Windows](https://gnuwin32.sourceforge.net/packages/make.htm)
- [LibIntl for Windows](https://gnuwin32.sourceforge.net/packages/libintl.htm)
- [LibIconv for Windows](https://gnuwin32.sourceforge.net/packages/libiconv.htm)
- [OpenOCD](https://github.com/ciniml/debug-tools-builder/tree/v1.3)
- [LLVM](https://github.com/llvm/llvm-project/releases)

以下の環境変数を設定してください。

- `GCC_PATH`: `arm-none-eabi-gcc`がある`bin`ディレクトリへのフルパス
- `PICO_SDK_PATH`: [pico-sdk](https://github.com/raspberrypi/pico-sdk)のプロジェクトルートディレクトリへのフルパス

## Mac

以下のソフトウェアをダウンロードしてパスを通してください。

- [Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)

また，`Make`，`OpenOCD`，`LLVM`をHomebrew等でインストールしてください。
Windowsと同じく`GCC_PATH`，`PICO_SDK_PATH`環境変数を設定してください。

## デバッガ

VSCode上でF5キーを押してください。
