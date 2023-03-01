cmake_minimum_required(VERSION 3.21)

project(jlink_rtt_tests)

include(ExternalProject)

ExternalProject_Add(
  segger_examples
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/segger_examples
  CMAKE_ARGS --toolchain=${CMAKE_CURRENT_SOURCE_DIR}/stm32l476_toolchain.cmake
)