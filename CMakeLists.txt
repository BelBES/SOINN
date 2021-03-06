project(SOINN)
cmake_minimum_required(VERSION 2.8)
aux_source_directory(. SRC_LIST)

#################################
set(Boost_INCLUDE_DIR "C:/Program Files (x86)/PCL 1.6.0/3rdParty/Boost/include")
set(Boost_LIBRARIES_DIR "C:/Program Files (x86)/PCL 1.6.0/3rdParty/Boost/lib")
find_package(Boost COMPONENTS ${BOOST_COMPONENTS} system filesystem serialization program_options graph REQUIRED)
if(NOT Boost_FOUND)
    message(SEND_ERROR "Failed to find Boost")
    return()
else()
    include_directories(${Boost_INCLUDE_DIRS})
    link_directories(${Boost_LIBRARY_DIRS})
    add_definitions(-DBOOST_ALL_NO_LIB)
    add_definitions(-DBOOST_ALL_DYN_LINK)
endif()
#################################

#################################
set(Opencv_INCLUDE_DIR "C:/DevTools/opencv/opencv_bin/include")
set(Opencv_LIBRARIES_DIR "C:/DevTools/opencv/opencv_bin/lib/Debug")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${Opencv_LIBRARIES_DIR})
find_package(OpenCV REQUIRED)
if(NOT OpenCV_FOUND)
    message(SEND_ERROR "Faild to find Opencv")
    return()
else()
    include_directories(${Opencv_INCLUDE_DIR})
endif()
#################################

add_executable(${PROJECT_NAME} ${SRC_LIST})

target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${Boost_LIBRARIES})
