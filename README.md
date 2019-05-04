# Fury

Copyright (c) 2018 Fury Project, Derived from 2014-2018, The Monero Project 
Portions Copyright (c) 2012-2013 The Cryptonote developers.

## Development resources

- Web: [Fury Website](https://fury.piratepools.nl/)
- Explorer: [Fury Explorer](http://69.55.49.102:8081/)
- Official Mining Pool: [Fury Pool](https://fury.xmining.pro/)
- Bitcointalk: [Fury ANN](https://bitcointalk.org/index.php?topic=5043980.0) 
- Reddit: TBA
- Twitter: [Fury Twitter](https://twitter.com/FuryCoin) 
- Telegram: TBA
- Discord: [Fury Discord](https://discord.gg/bA6YHZC) 
- GitHub: [https://github.com/FuryCoin/Fury](https://github.com/FuryCoin/Fury)

## Introduction

Fury is a cryptocurrency built on Monero v7 with the aim to become one of a few standard currencies for digital payments.  The main characteristics of Fury are detailed below:

-    Total Supply: 1,000,000,000

-    Block Time: 1 minute

-    Algorithm: Cryptonight Superfast

-    Reward: ~1,500 FURY at inception

-    Emission structure: logarithmic until max supply is reached in 2020. For more information: TBA

## License

See [LICENSE](LICENSE).

## Scheduled software upgrades

| Software upgrade block height | Date       | Fork version | Details                                                                            |  
| ------------------------------ | -----------| ----------------- | ---------------------------------------------------------------------------------- |
| 0                       | 28-09-2018 | v1                 |  Genesis block       |
| 1                       | 28-09-2018 | v7                 |  Start of the blockchain       |
| 9                       | 10-01-2019 | v9                 |  Algo change, Bulletproofs     |
| 12                      | 05-04-2019 | v12                |  Service Nodes                 |

Note future releases block heights and dates may change, so make sure to frequently check github, our website, the forums, etc. for the most up to date information.

## Compiling Fury from source

### Dependencies

The following table summarizes the tools and libraries required to build. A
few of the libraries are also included in this repository (marked as
"Vendored"). By default, the build uses the library installed on the system,
and ignores the vendored sources. However, if no library is found installed on
the system, then the vendored source will be built and used. The vendored
sources are also used for statically-linked builds because distribution
packages often include only shared library binaries (`.so`) but not static
library archives (`.a`).

| Dep          | Min. version  | Vendored | Debian/Ubuntu pkg  | Arch pkg     | Fedora            | Optional | Purpose        |
| ------------ | ------------- | -------- | ------------------ | ------------ | ----------------- | -------- | -------------- |
| GCC          | 4.7.3         | NO       | `build-essential`  | `base-devel` | `gcc`             | NO       |                |
| CMake        | 3.5           | NO       | `cmake`            | `cmake`      | `cmake`           | NO       |                |
| pkg-config   | any           | NO       | `pkg-config`       | `base-devel` | `pkgconf`         | NO       |                |
| Boost        | 1.58          | NO       | `libboost-all-dev` | `boost`      | `boost-devel`     | NO       | C++ libraries  |
| OpenSSL      | basically any | NO       | `libssl-dev`       | `openssl`    | `openssl-devel`   | NO       | sha256 sum     |
| libzmq       | 3.0.0         | NO       | `libzmq3-dev`      | `zeromq`     | `cppzmq-devel`    | NO       | ZeroMQ library |
| OpenPGM      | ?             | NO       | `libpgm-dev`       | `libpgm`     | `openpgm-devel`   | NO       | For ZeroMQ     |
| libnorm[2]   | ?             | NO       | `libnorm-dev`      |              |               `   | YES      | For ZeroMQ     |
| libunbound   | 1.4.16        | YES      | `libunbound-dev`   | `unbound`    | `unbound-devel`   | NO       | DNS resolver   |
| libsodium    | ?             | NO       | `libsodium-dev`    | `libsodium`  | `libsodium-devel` | NO       | cryptography   |
| libunwind    | any           | NO       | `libunwind8-dev`   | `libunwind`  | `libunwind-devel` | YES      | Stack traces   |
| liblzma      | any           | NO       | `liblzma-dev`      | `xz`         | `xz-devel`        | YES      | For libunwind  |
| libreadline  | 6.3.0         | NO       | `libreadline6-dev` | `readline`   | `readline-devel`  | YES      | Input editing  |
| ldns         | 1.6.17        | NO       | `libldns-dev`      | `ldns`       | `ldns-devel`      | YES      | SSL toolkit    |
| expat        | 1.1           | NO       | `libexpat1-dev`    | `expat`      | `expat-devel`     | YES      | XML parsing    |
| GTest        | 1.5           | YES      | `libgtest-dev`[1]  | `gtest`      | `gtest-devel`     | YES      | Test suite     |
| Doxygen      | any           | NO       | `doxygen`          | `doxygen`    | `doxygen`         | YES      | Documentation  |
| Graphviz     | any           | NO       | `graphviz`         | `graphviz`   | `graphviz`        | YES      | Documentation  |         


[1] On Debian/Ubuntu `libgtest-dev` only includes sources and headers. You must
build the library binary manually. This can be done with the following command ```sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make && sudo mv libg* /usr/lib/ ```
[2] libnorm-dev is needed if your zmq library was built with libnorm, and not needed otherwise

Debian / Ubuntu one liner for all dependencies  
``` sudo apt update && sudo apt install build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev doxygen graphviz libpgm-dev```

### Cloning the repository

     $ git clone https://github.com/FuryCoin/Fury 

### Build instructions

Fury uses the CMake build system and a top-level [Makefile](Makefile) that
invokes cmake commands as needed.

#### On Linux and OS X

* Install the dependencies
* Change to the root of the source code directory and build:

        cd Fury
        make release

    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.

    *Note*: If cmake can not find zmq.hpp file on OS X, installing `zmq.hpp` from
    https://github.com/zeromq/cppzmq to `/usr/local/include` should fix that error.

* The resulting executables can be found in `build/release/bin`

* Add `PATH="$PATH:$HOME/Fury/build/release/bin"` to `.profile`

* Run Fury with `fury --detach`

* **Optional**: build and run the test suite to verify the binaries:

        make release-test

    *NOTE*: `core_tests` test may take a few hours to complete.

* **Optional**: to build binaries suitable for debugging:

         make debug

* **Optional**: to build statically-linked binaries:

         make release-static

Dependencies need to be built with -fPIC. Static libraries usually aren't, so you may have to build them yourself with -fPIC. Refer to their documentation for how to build them.

* **Optional**: build documentation in `doc/html` (omit `HAVE_DOT=YES` if `graphviz` is not installed):

        HAVE_DOT=YES doxygen Doxyfile

#### On Windows:

Binaries for Windows are built on Windows using the MinGW toolchain within
[MSYS2 environment](https://www.msys2.org). The MSYS2 environment emulates a
POSIX system. The toolchain runs within the environment and *cross-compiles*
binaries that can run outside of the environment as a regular Windows
application.

**Preparing the build environment**

* Download and install the [MSYS2 installer](https://www.msys2.org), either the 64-bit (x86_64) or the 32-bit (i686) package, depending on your system.
* Note: Installation must be on the C drive and root directory as result of [Monero issue 3167](https://github.com/monero-project/monero/issues/3167).
* Open the MSYS shell via the `MSYS2 MSYS` shortcut in the Start Menu or "C:\msys64\msys2_shell.cmd -msys"
* Update packages using pacman:  

        pacman -Syu  

* Exit the MSYS shell using Alt+F4 when you get a warning stating: "terminate MSYS2 without returning to shell and check for updates again/for example close your terminal window instead of calling exit"

* Open the MSYS MinGW shell via the `MSYS2 MinGW 64-bit` shortcut or "C:\msys64\msys2_shell.cmd -mingw64" for 64-bit builds or via the `MSYS2 MinGW 32-bit` shortcut or "C:\msys64\msys2_shell.cmd -mingw32" for 32-bit builds 

* Update packages again using pacman: 

        pacman -Syu  

* Install dependencies:

    To build for 64-bit Windows:

        pacman -S mingw-w64-x86_64-toolchain make mingw-w64-x86_64-cmake mingw-w64-x86_64-boost mingw-w64-x86_64-openssl mingw-w64-x86_64-zeromq mingw-w64-x86_64-libsodium mingw-w64-x86_64-hidapi git

    To build for 32-bit Windows:

        pacman -S mingw-w64-i686-toolchain make mingw-w64-i686-cmake mingw-w64-i686-boost mingw-w64-i686-openssl mingw-w64-i686-zeromq mingw-w64-i686-libsodium mingw-w64-i686-hidapi git

* Close and reopen the MSYS MinGW shell via `MSYS2 MinGW 64-bit` shortcut on
  64-bit Windows or `MSYS2 MinGW 32-bit` shortcut on 32-bit Windows. Note 
  that if you are running 64-bit Windows, you will have both 64-bit and
  32-bit MinGW shells.

**Cloning**

* To git clone, run:

      git clone https://github.com/FuryCoin/Fury 

**Building**

* If you are on a 64-bit system, run:

        cd Fury
        make release-static-win64

* If you are on a 32-bit system, run:

        cd Fury
        make release-static-win32

* The resulting executables can be found in `build/release/bin`

### Building portable statically linked binaries

By default, in either dynamically or statically linked builds, binaries target the specific host processor on which the build happens and are not portable to other processors. Portable binaries can be built using the following targets:

* ```make release-static-linux-x86_64``` builds binaries on Linux on x86_64 portable across POSIX systems on x86_64 processors
* ```make release-static-linux-i686``` builds binaries on Linux on x86_64 or i686 portable across POSIX systems on i686 processors
* ```make release-static-linux-armv8``` builds binaries on Linux portable across POSIX systems on armv8 processors
* ```make release-static-linux-armv7``` builds binaries on Linux portable across POSIX systems on armv7 processors
* ```make release-static-linux-armv6``` builds binaries on Linux portable across POSIX systems on armv6 processors
* ```make release-static-win64``` builds binaries on 64-bit Windows portable across 64-bit Windows systems
* ```make release-static-win32``` builds binaries on 64-bit or 32-bit Windows portable across 32-bit Windows systems

## Running furyd

The build places the binary in `bin/` sub-directory within the build directory
from which cmake was invoked (repository root by default). To run in
foreground:

    ./bin/furyd

To list all available options, run `./bin/furyd --help`.  Options can be
specified either on the command line or in a configuration file passed by the
`--config-file` argument.  To specify an option in the configuration file, add
a line with the syntax `argumentname=value`, where `argumentname` is the name
of the argument without the leading dashes, for example `log-level=1`.

To run in background:

    ./bin/furyd --log-file furyd.log --detach

To run as a systemd service, copy
[furyd.service](utils/systemd/furyd.service) to `/etc/systemd/system/` and
[furyd.conf](utils/conf/furyd.conf) to `/etc/`. The [example
service](utils/systemd/furyd.service) assumes that the user `fury` exists
and its home is the data directory specified in the [example
config](utils/conf/furyd.conf).

If you're on Mac, you may need to add the `--max-concurrency 1` option to
monero-wallet-cli, and possibly monerod, if you get crashes refreshing.
