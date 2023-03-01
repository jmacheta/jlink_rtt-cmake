cmake_minimum_required(VERSION 3.21)

set(RTT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/SEGGER_RTT_V768c)

add_library(jlink_rtt STATIC ${RTT_DIR}/RTT/SEGGER_RTT.c ${RTT_DIR}/RTT/SEGGER_RTT_printf.c)

target_include_directories(jlink_rtt PUBLIC ${RTT_DIR}/RTT)

if (JLINK_RTT_USE_SYSCALLS)
  # Compile all syscall files - their content is protected by ifdefs against using wrong ones
  target_sources(
    jlink_rtt PRIVATE ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_GCC.c 
                      ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_IAR.c
                      ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_KEIL.c
                      ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_SES.c
  )
  target_compile_options(jlink_rtt PRIVATE -Wno-pedantic -Wno-sign-conversion -Wno-cast-align)
  target_link_options(jlink_rtt INTERFACE -u_write) # This makes sure that implementation from std would be ignored (i.e. when linking with nosys.spec)

endif ()
