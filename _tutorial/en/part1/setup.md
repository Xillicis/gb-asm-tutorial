---
title: Setup
---

First, we should set up our dev environment.
We will need:

1. A POSIX environment
2. [RGBDS](https://rgbds.gbdev.io) v0.5.1 (though v0.5.0 should be compatible)
3. GNU Make (preferably a recent version)
4. A code editor

## Linux & macOS

Good news: you're already fulfilling step 1!
You just need to [install RGBDS](https://rgbds.gbdev.io/install), and maybe update GNU Make.

### macOS

At the time of writing this, macOS (up to 11.0, the current latest release) ships a very outdated GNU Make.
You can check it by opening a terminal, and running `make --version`, which should indicate "GNU Make" and a date, among other things.

If your Make is too old, you can update it using [Homebrew](https://brew.sh)'s formula [`make`](https://formulae.brew.sh/formula/make#default).
At the time of writing, this should print a warning that the updated Make has been installed as `gmake`; you can either follow the suggestion in order to use it as your "default" `make`, or substitute `gmake` for `make` in this tutorial.

### Linux

Once RGBDS is installed, open a terminal and run `make --version` to check your Make version (which is likely GNU Make).

If `make` cannot be found, you may need to install your distribution's `build-essentials`.

## Windows

The sad truth is that Windows is a terrible OS for development; however, you can install environments that solve most issues.

On Windows 10, your best bet is [WSL](https://docs.microsoft.com/en-us/windows/wsl).
Install WSL 1 or WSL 2, install a Linux distribution, and then follow these steps again, but for the Linux distribution you installed.

If WSL is not an option, you can use [MSYS2](https://www.msys2.org) or [Cygwin](https://www.cygwin.com) instead; you will likely have to [install RGBDS from source](https://rgbds.gbdev.io/install/source).
