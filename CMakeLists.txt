cmake_minimum_required(VERSION 3.2)
project(battmon_cmake)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin/)

find_package(LibNotify REQUIRED)
find_package(GLIB REQUIRED)
find_package(GDK-PixBuf REQUIRED)
find_package(GTK2 REQUIRED)
find_package(Boost COMPONENTS program_options filesystem REQUIRED)
include_directories(${LibNotify_INCLUDE_DIRS} ${GLIB_INCLUDE_DIRS} ${GDK-PIXBUF_INCLUDE_DIRS} ${GTK2_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
set(LIBS ${LIBS} ${LibNotify_LIBRARIES} ${GLIB_LIBRARIES} ${GDK-PIXBUF_LIBRARIES} ${GTK2_LIBRARIES} ${Boost_LIBRARIES})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(SOURCE_FILES battmon.cpp)
add_executable(battmon ${SOURCE_FILES})
target_link_libraries(battmon ${LIBS} -lnotify -lboost_system)

install(TARGETS battmon DESTINATION /usr/bin)
install(DIRECTORY icons DESTINATION /usr/share/battmon)