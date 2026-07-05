option(SYSTEMD_USER_SERVICE "Install systemd user service file" ON)
option(SYSTEMD_SYSTEM_SERVICE "Install systemd system service file" OFF)
option(OPENRC "Install OpenRC service file" OFF) # To be implemented
set(YDOTOOLD_SERVICE_ARGS "" CACHE STRING "Additional arguments passed to ydotoold in generated service files")

set(YDOTOOLD_SERVICE_COMMAND "${CMAKE_INSTALL_FULL_BINDIR}/ydotoold")
if(YDOTOOLD_SERVICE_ARGS)
    string(APPEND YDOTOOLD_SERVICE_COMMAND " ${YDOTOOLD_SERVICE_ARGS}")
endif()

if(SYSTEMD_USER_SERVICE AND SYSTEMD_SYSTEM_SERVICE)
    message(FATAL_ERROR "Both system and user services are enabled. Choose one.")
endif()

if(SYSTEMD_USER_SERVICE OR SYSTEMD_SYSTEM_SERVICE) 
    add_subdirectory(systemd)
endif()

if(OPENRC)
    add_subdirectory(openrc)
endif()
