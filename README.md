# GreenifyOS 
### Current revision based on Prusa FW (commit BA522e1, 24 July 2022) 

A custom flavor of Prusa's buddy board firmware for Prusa MINI. Built with Prusa's provided utils and [PNG2Prusa](https://github.com/CM2205/PNG2PrusaFW), a Java script to automate the conversion of PNG images into Prusa's .c image files. 

The source code provided here is identical to that of the official Prusa FW with small exceptions related to the cosmet adjustments: 
1. The images located in src/gui/res/png andsrc/gui/res/cc have green UI elements instead of the default orange color. 
2. The GUI's orange color (defined in src/gui/include/guitypes.h) has been overwritten in favor of the customized green color. This is the change responsible for changing the GUI's orange menu to the customized green color. 

Note: This project was created with the most up to date source code at the time. As updates will likely be constant for the official firmware, I cannot guarantee that greenifyOS will remain in sync with these changes. In fact, it may very well be the case that updates only come on a fixed timeline (every couple of months or so, if ever). 

For those interested in applying these cosmetic changes to a future release of Prusa firmware, the assets which were adjusted can be added to their respective locations and compiled alongside the stock firmware. Additionally, the change to the guitypes header can be manually implemented by the user. 


# Buddy
[![GitHub release](https://img.shields.io/github/release/prusa3d/Prusa-Firmware-Buddy.svg)](https://github.com/prusa3d/Prusa-Firmware-Buddy/releases)
[![Build Status](https://holly.prusa3d.com/buildStatus/icon?job=Prusa-Firmware-Buddy%2FMultibranch%2Fmaster)](https://holly.prusa3d.com/job/Prusa-Firmware-Buddy/job/Multibranch/job/master/)

This repository includes source code and firmware releases for the Original Prusa 3D printers based on the 32-bit ARM microcontrollers.

The currently supported model is:
- Original Prusa MINI

## Getting Started

### Requirements

- Python 3.6 or newer (with pip)

### Cloning this repository

Run `git clone https://github.com/prusa3d/Prusa-Firmware-Buddy.git`.

### Building (on all platforms, without an IDE)

Run `python utils/build.py`. The binaries are then going to be stored under `./build/products`.

- Without any arguments, it will build a release version of the firmware for all supported printers and bootloader settings.
- To generate `.bbf` versions of the firmware, use: `./utils/build.py --generate-bbf`.
- Use `--build-type` to select build configurations to be built (`debug`, `release`).
- Use `--preset` to select for which printers the firmware should be built.
- By default, it will build the firmware in "prerelease mode" set to `beta`. You can change the prerelease using `--prerelease alpha`, or use `--final` to build a final version of the firmware.
- Use `--host-tools` to include host tools in the build (`bin2cc`, `png2font`, ...)
- Find more options using the `--help` flag!

#### Examples:

Build the firmware for MINI in `debug` mode:

```bash
python utils/build.py --preset mini --build-type debug
```

Build _final_ version for all printers and create signed `.bbf` versions:

```bash
python utils/build.py --final --generate-bbf --signing-key <path-to-ecdsa-private-key>
```

Build the firmware for MINI using a custom version of gcc-arm-none-eabi (available in `$PATH`) and use `Make` instead of `Ninja` (not recommended):

```bash
python utils/build.py --preset mini --toolchain cmake/AnyGccArmNoneEabi.cmake --generator 'Unix Makefiles'
```

#### Windows 10 troubleshooting

If you have python installed and in your PATH but still getting cmake error `Python3 not found.` Try running python and python3 from cmd. If one of it opens Microsoft Store instead of either opening python interpreter or complaining `'python3' is not recognized as an internal or external command,
operable program or batch file.` Open `manage app execution aliases` and disable `App Installer` association with `python.exe` and `python3.exe`.

#### Python environment

The `build.py` script wants to install some python packages. If you prefer not to have your system modified, it is possible to use `virtualenv` or a similar tool.

```bash
virtualnev venv
. venv/bin/activate
```

### Development

The build process of this project is driven by CMake and `build.py` is just a high-level wrapper around it. As most modern IDEs support some kind of CMake integration, it should be possible to use almost any editor for development. Below are some documents describing how to setup some popular text editors.

- [Visual Studio Code](doc/editor/vscode.md)
- [Vim](doc/editor/vim.md)
- [Eclipse, STM32CubeIDE](doc/editor/stm32cubeide.md)
- [Other LSP-based IDEs (Atom, Sublime Text, ...)](doc/editor/lsp-based-ides.md)

#### Formatting

All the source code in this repository is automatically formatted:

- C/C++ files using [clang-format](https://clang.llvm.org/docs/ClangFormat.html),
- Python files using [yapf](https://github.com/google/yapf),
- and CMake files using [cmake-format](https://github.com/cheshirekow/cmake_format).

If you want to contribute, make sure to install [pre-commit](https://pre-commit.com) and then run `pre-commit install` within the repository. This makes sure that all your future commits will be formatted appropriately. Our build server automatically rejects improperly formatted pull requests.

#### Running tests

```bash
mkdir build-tests
cd build-tests
cmake ..
make tests
ctest .
```

## Flashing Custom Firmware

To install custom firmware, you have to break the appendix on the board. Learn how to in the following article https://help.prusa3d.com/article/zoiw36imrs-flashing-custom-firmware.

## Feedback

- [Feature Requests from Community](https://github.com/prusa3d/Prusa-Firmware-Buddy/labels/feature%20request)

## License

The firmware source code is licensed under the GNU General Public License v3.0 and the graphics and design are licensed under Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0). Fonts are licensed under different license (see [LICENSE](LICENSE.md)).
