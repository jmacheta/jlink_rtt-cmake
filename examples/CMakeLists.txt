add_compile_options(-g3)

add_executable(input_echo critical_section_stub.c Main_RTT_InputEchoApp.c)
target_link_libraries(input_echo PRIVATE jlink_rtt)

add_executable(input_echo_stdio critical_section_stub.c Main_RTT_InputEchoAppStdio.c)
target_link_libraries(input_echo_stdio PRIVATE jlink_rtt)

add_executable(menu_app critical_section_stub.c Main_RTT_MenuApp.c)
target_link_libraries(menu_app PRIVATE jlink_rtt)

add_custom_target(jlink-rtt_examples DEPENDS input_echo input_echo_stdio menu_app critical_section_stub.c)
