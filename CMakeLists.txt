cmake_minimum_required(VERSION 3.0)
project(matplotlibcpp CXX)

include(GNUInstallDirs)

find_package(PythonLibs 2.7 REQUIRED)

add_library(matplotlibcpp INTERFACE)

target_include_directories(matplotlibcpp
	INTERFACE
		${PYTHON_INCLUDE_DIRS}
		$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
		$<INSTALL_INTERFACE:./>)

target_link_libraries(matplotlibcpp INTERFACE ${PYTHON_LIBRARIES})

# 'make install' to the correct locations (provided by GNUInstallDirs).
install(TARGETS matplotlibcpp EXPORT matplotlibcpp-config
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR})
install(FILES matplotlibcpp.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT matplotlibcpp-config DESTINATION cmake)

# Makes the project importable from the build directory
export(TARGETS matplotlibcpp FILE matplotlibcpp-config.cmake)
