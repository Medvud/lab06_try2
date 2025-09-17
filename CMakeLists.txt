cmake_minimum_required(VERSION 3.16)
project(Project)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib)

add_library(formatter_ex STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib/formatter_ex.cpp)
add_library(formatter STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib/formatter.cpp)
add_library(solver STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp)

add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world_application/hello_world.cpp)
add_executable(equation ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)

target_link_libraries(formatter_ex PUBLIC formatter)
target_link_libraries(equation formatter_ex solver)
target_link_libraries(hello_world formatter_ex)

set(CPACK_PACKAGE_NAME "MyLaba06")
set(CPACK_PACKAGE_VERSION "1.0.0")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Medvud")
set(CPACK_PACKAGE_CONTACT "pishite@gmail.com")
set(CPACK_GENERATOR "DEB RPM WIX DragNDrop TGZ ZIP")
include(CPack)