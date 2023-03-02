# Jlink RTT CMake library

This package wrapps official SEGGER RTT library, bundled with [J-link Software](https://www.segger.com/downloads/jlink/), into CMake library.

## Installation

The easiest way is to use built-in CMake FetchContent:

```cmake
include(FetchContent)
FetchContent_Declare(
    jlink_rtt
    GIT_REPOSITORY https://github.com/jmacheta/jlink_rtt-cmake
    GIT_TAG main
)

FetchContent_MakeAvailable(jlink_rtt)
```

Alternatively, you can add this repo as a submodule, and simply use ```add_subdirectory(<path_to_cubemx_cmake_in_your_tree>)```

## Usage

As with every CMake library, the only thing you need to do is link with the library by

```cmake
target_link_libraries(<your_component> PUBLIC jlink_rtt)
```

The provided package comes with example configuration file in src/Config. If your preprocessor supports __has_include command (like GCC and Clang), and the example config suits your needs, you don't need to do anyting.
Otherwise you need to inject include directory containing config file to this library:

```cmake
target_include_directories(jlink_rtt PUBLIC <PATH_TO_DIRECTORY_WITH_CONFIG_HEADER>) # the visibility MUST be public - the file is also included by public API header
```

That's basically it. You may also with to include SEGGER's _write syscall implementation. To do so, define

```cmake
set(JLINK_RTT_USE_SYSCALLS ON)
```

before fetching library.

## Toolchain-dependent behaviour

- When preprocessor supports __has_include command, it will look for "custom" SEGGER_RTT_Conf.h file in provided include directories. If it fails, it will fall back to sample configuration from src/Config/SEGGER_RTT_Conf.h. If preprocessor has no__has_include support, it will simply include SEGGER_RTT_Conf.h, which may fail if none is find.

## Non-Affiliation Disclaimer

This package is not endorsed by, directly affiliated with, maintained, authorized, or sponsored by SEGGER. All product and company names are the registered trademarks of their original owners. The use of any trade name or trademark is for identification and reference purposes only and does not imply any association with the trademark holder of their product brand.
