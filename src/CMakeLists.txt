cmake_minimum_required(VERSION 3.21)

add_library(jlink_rtt OBJECT RTT/SEGGER_RTT.c RTT/SEGGER_RTT_printf.c)

target_include_directories(jlink_rtt PUBLIC RTT)

if (JLINK_RTT_USE_SYSCALLS)
  # Compile all syscall files - their content is protected by ifdefs against using wrong ones
  target_sources(jlink_rtt PRIVATE Syscalls/SEGGER_RTT_Syscalls_GCC.c Syscalls/SEGGER_RTT_Syscalls_IAR.c Syscalls/SEGGER_RTT_Syscalls_KEIL.c Syscalls/SEGGER_RTT_Syscalls_SES.c)
endif ()
