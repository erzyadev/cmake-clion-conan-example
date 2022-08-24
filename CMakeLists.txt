cmake_minimum_required(VERSION 3.11)

project(cmake-clion-conan-example CXX)

set(CMAKE_CXX_STANDARD 20)


include(cmake/conan.cmake)
conan_check(REQUIRED)

conan_cmake_run(CONANFILE conanfile.txt
        BASIC_SETUP CMAKE_TARGETS
        BUILD_TYPE Release
        REMOTE conancenter
        BUILD missing)


find_package(Boost 1.78.0 REQUIRED)
if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
endif()


set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

add_executable(cmake-clion-conan-example src/main.cpp)

target_link_libraries(cmake-clion-conan-example PRIVATE Threads::Threads)
