cmake_minimum_required(VERSION 3.10)


if(NOT DEFINED PRINT_VERSION)
    set(PRINT_VERSION "1.0.0")
endif()

project(solver
    VERSION ${PRINT_VERSION}
    DESCRIPTION "C++ app for solving equations"
)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib)


add_library(solver_lib ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp)
add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)


target_include_directories(solver_lib PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib
)


target_link_libraries(solver PRIVATE formatter_ex_lib solver_lib)


install(TARGETS solver
    RUNTIME DESTINATION bin
)


include(InstallRequiredSystemLibraries)


set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "C++ app for solving equations")
set(CPACK_RESOURCE_FILE_LICENSE ${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README ${CMAKE_CURRENT_SOURCE_DIR}/README.md)


set(CPACK_SOURCE_IGNORE_FILES 
    "\\\\.cmake;/\\\\.build/;/\\\\.git/;/\\\\.github/"
)
set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")
set(CPACK_SOURCE_PACKAGE_FILE_NAME "solver-${PROJECT_VERSION}")


set(CPACK_DEBIAN_PACKAGE_NAME "solver")
set(CPACK_DEBIAN_FILE_NAME "solver-${PROJECT_VERSION}.deb")
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "jerex2218")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION "Solve quadratic equations")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)


set(CPACK_GENERATOR "DEB")


include(CPack)
