cmake_minimum_required(VERSION 3.21)

project(jlink_rtt-cmake LANGUAGES C VERSION 7.68.3)

option(JLINK_RTT_EXAMPLES "Forces building test cases" ${PROJECT_IS_TOP_LEVEL})

option(JLINK_RTT_USE_SYSCALLS "Provides _write syscall bound to RTT" ${PROJECT_IS_TOP_LEVEL})

add_subdirectory(src)

if (JLINK_RTT_EXAMPLES)
  include(CTest)
  add_subdirectory(examples EXCLUDE_FROM_ALL)
endif ()
