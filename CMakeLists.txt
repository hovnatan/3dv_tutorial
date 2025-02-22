cmake_minimum_required(VERSION 2.6)

project(3dv_tutorial)
SET(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 14)
# set(OpenCV_DIR "$ENV{HOME}/opt_arm64/lib/cmake/opencv4")

set(CMAKE_BUILD_TYPE Release)
find_package(OpenCV REQUIRED)
find_package(Ceres REQUIRED)

set(SRC_DIR	"${CMAKE_SOURCE_DIR}/src")
set(BIN_DIR	"${CMAKE_SOURCE_DIR}/bin")

file(GLOB APP_SOURCES "${SRC_DIR}/*.cpp")
foreach(app_source ${APP_SOURCES})
    string(REPLACE ".cpp" "" app_name ${app_source})
    string(REPLACE "${SRC_DIR}/" "" app_name ${app_name})
    add_executable(${app_name} ${app_source})
    target_link_libraries(${app_name} ${OpenCV_LIBS} ${Ceres_LIBRARIES})
    install(TARGETS ${app_name} DESTINATION ${BIN_DIR})
endforeach(app_source ${APP_SOURCES})
