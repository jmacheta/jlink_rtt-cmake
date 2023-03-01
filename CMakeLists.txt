cmake_minimum_required(VERSION 3.21)

project(jlink_rtt-cmake LANGUAGES C VERSION 7.68.3)

option(JLINK_RTT_CMAKE_BUILD_TESTS "Forces building test cases" OFF)
option(JLINK_RTT_USE_SYSCALLS "Provides _write syscall bound to RTT" OFF)

add_subdirectory(src)

if (PROJECT_IS_TOP_LEVEL OR JLINK_RTT_CMAKE_BUILD_TESTS)
  enable_testing()
  add_subdirectory(tests)
endif ()
