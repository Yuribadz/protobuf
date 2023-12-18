# Minimum CMake required
cmake_minimum_required(VERSION 3.10)

# Project
project(other)

# Find required protobuf package
find_package(Protobuf REQUIRED)

if(protobuf_VERBOSE)
  message(STATUS "Using Protocol Buffers ${protobuf_VERSION}")
endif()

set(CMAKE_INCLUDE_CURRENT_DIR TRUE)
message(STATUS "${Protobuf_LIBRARIES} ${Protobuf_INCLUDE_DIR}")

# http://www.cmake.org/Wiki/CMake_FAQ#How_can_I_build_my_MSVC_application_with_a_static_runtime.3F
if(MSVC AND protobuf_MSVC_STATIC_RUNTIME)
  foreach(flag_var
      CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE
      CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
    if(${flag_var} MATCHES "/MD")
      string(REGEX REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
    endif(${flag_var} MATCHES "/MD")
  endforeach()
endif()


set(executable_name addperson_cpp)
add_executable(addperson_cpp addperson.cpp)
target_sources(addperson_cpp
  PRIVATE
  addperson.cpp
  addressbook.proto)

target_link_libraries(addperson_cpp protobuf::libprotobuf)
protobuf_generate(TARGET addperson_cpp)