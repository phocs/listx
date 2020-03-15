cmake_minimum_required(VERSION 3.12)

# set the project name and version
project(
    listx
	VERSION 0.0.1
	DESCRIPTION "Subset of the Linux's list implementation."
	HOMEPAGE_URL "https://github.com/phocs/listx.git"
	LANGUAGES C
)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(
    ${PROJECT_NAME}
    INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)

# install rules
install(FILES listx.h DESTINATION include)

# uninstall target
if(NOT TARGET uninstall)
  configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)

  add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)
endif()
