set(RTT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/SEGGER_RTT_V768c)

add_library(jlink_rtt STATIC ${RTT_DIR}/RTT/SEGGER_RTT.c ${RTT_DIR}/RTT/SEGGER_RTT_printf.c)

target_include_directories(jlink_rtt PUBLIC ${RTT_DIR}/RTT)

if (JLINK_RTT_USE_SYSCALLS)

  if (CMAKE_C_COMPILER_ID STREQUAL "GNU" OR CMAKE_C_COMPILER_ID STREQUAL "Clang")
    target_sources(jlink_rtt PRIVATE ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_GCC.c)

  elseif (CMAKE_C_COMPILER_ID STREQUAL "IAR")
    target_sources(jlink_rtt PRIVATE ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_IAR.c)

  else ()
    # Compile all syscall files - their content is protected by ifdefs against using wrong ones I have no experience
    # with those compilers, and CMake don't have predefined compiler ids' so feel free to correct this
    target_sources(
      jlink_rtt PRIVATE ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_KEIL.c ${RTT_DIR}/Syscalls/SEGGER_RTT_Syscalls_SES.c
    )
  endif ()

  target_link_options(jlink_rtt INTERFACE -u_write) # This makes sure that implementation from std would be ignored
                                                    # (i.e. when linking with nosys.spec)
endif ()

# Suppress warnings in RTT code
if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
  target_compile_options(jlink_rtt PRIVATE -Wno-pedantic -Wno-sign-conversion -Wno-cast-align)
endif ()
