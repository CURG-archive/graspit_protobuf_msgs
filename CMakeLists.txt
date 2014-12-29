list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE}/cmake/Modules)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()
message("-- Build type: ${CMAKE_BUILD_TYPE}")

find_package(Protobuf REQUIRED)

set(GRASPIT_PB_OUTPUT_DIR ${CMAKE_CURRENT_SOURCE_DIR}/gen_proto)
file(GLOB GRASPIT_PB_PROTOS ${CMAKE_CURRENT_SOURCE_DIR}/*.proto)

set(CMAKE_CURRENT_BINARY_DIR ${GRASPIT_PB_OUTPUT_DIR})
protobuf_generate_cpp(GRASPIT_PB_SOURCES GRASPIT_PB_HEADERS ${GRASPIT_PB_PROTOS})

list(APPEND GRASPIT_CORE_INCLUDE_DIRS ${GRASPIT_PB_OUTPUT_DIR})


add_library(graspit_proto_msgs ${GRASPIT_PB_SOURCES})
target_link_libraries(graspit_proto_msgs ${PROTOBUF_LIBRARY})
include_directories(graspit_proto_msgs ${PROTOBUF_INCLUDE_DIR} ${GRASPIT_PB_OUTPUT_DIR})




