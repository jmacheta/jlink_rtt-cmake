cmake_minimum_required(VERSION 3.21)

project(jlink_rtt_tests LANGUAGES C ASM)

add_compile_options(-g3)

# Since I don't provide find_package, this is the simple hack to include the library into the project
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../.. ${CMAKE_CURRENT_BINARY_DIR}/jlink_rtt)
set(RTT_EXAMPLE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../src/Examples)

add_executable(input_echo ${RTT_EXAMPLE_DIR}/Main_RTT_InputEchoApp.c startup_stm32l476xx.s)
target_link_libraries(input_echo PRIVATE jlink_rtt)
target_link_options(input_echo PRIVATE -T ${CMAKE_CURRENT_SOURCE_DIR}/STM32L476RGTx_FLASH.ld)


add_executable(input_echo_stdio ${RTT_EXAMPLE_DIR}/Main_RTT_InputEchoAppStdio.c startup_stm32l476xx.s)
target_link_libraries(input_echo_stdio PRIVATE jlink_rtt)
target_link_options(input_echo_stdio PRIVATE -T ${CMAKE_CURRENT_SOURCE_DIR}/STM32L476RGTx_FLASH.ld)


add_executable(menu_app ${RTT_EXAMPLE_DIR}/Main_RTT_MenuApp.c startup_stm32l476xx.s)
target_link_libraries(menu_app PRIVATE jlink_rtt)
target_link_options(menu_app PRIVATE -T ${CMAKE_CURRENT_SOURCE_DIR}/STM32L476RGTx_FLASH.ld)

add_executable(printf_test ${RTT_EXAMPLE_DIR}/Main_RTT_PrintfTest.c startup_stm32l476xx.s)
target_link_libraries(printf_test PRIVATE jlink_rtt)
target_link_options(printf_test PRIVATE -T ${CMAKE_CURRENT_SOURCE_DIR}/STM32L476RGTx_FLASH.ld)


# The package doesn't containt RTOS.h required to build the test. If you need to do so, get the file from somewhere and uncomment
# add_executable(speedtest ${RTT_EXAMPLE_DIR}/Main_RTT_SpeedTestApp.c startup_stm32l476xx.s)
# target_link_libraries(speedtest PRIVATE jlink_rtt)
# target_link_options(speedtest PRIVATE -T ${CMAKE_CURRENT_SOURCE_DIR}/STM32L476RGTx_FLASH.ld)
