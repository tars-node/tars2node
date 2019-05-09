cmake_minimum_required(VERSION 2.6)

project(tars2node)

set(CMAKE_VERBOSE_MAKEFILE off)

# version
set(TARS_VERSION "1.1.0")
set(PARSER_VERSION "${TARS_VERSION}")
set(GENERATOR_VERSION "20190509")

# namespace
set(IDL_NAMESPACE Tars)
string(TOLOWER ${IDL_NAMESPACE} TC_NAMESPACE)
set(GRAMMAR_NAME Grammar)

# idl
set(RPC_MODULE_PATH "@tars/rpc")
set(STREAM_MODULE_PATH "@tars/stream")
set(IDL_TYPE "Tars")
set(PROTOCOL_NAME "Tup")

# flag
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -g -O2 -Wall -Wno-sign-compare -Wno-unused-result -static")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -O2 -Wall -static")

# define
add_definitions(-DTARS_VERSION="${TARS_VERSION}")
add_definitions(-DPARSER_VERSION="${PARSER_VERSION}")
add_definitions(-DGENERATOR_VERSION="${GENERATOR_VERSION}")
add_definitions(-DTC_NAMESPACE=${TC_NAMESPACE})
add_definitions(-DIDL_NAMESPACE=${IDL_NAMESPACE})
add_definitions(-DGRAMMAR_NAME=${GRAMMAR_NAME})
add_definitions(-DRPC_MODULE_PATH="${RPC_MODULE_PATH}")
add_definitions(-DSTREAM_MODULE_PATH="${STREAM_MODULE_PATH}")
add_definitions(-DEXECUTE_FILENAME="${PROJECT_NAME}")
add_definitions(-DIDL_TYPE="${IDL_TYPE}")
add_definitions(-DPROTOCOL_NAME="${PROTOCOL_NAME}")

# include
include_directories(${PROJECT_SOURCE_DIR}/third_partly/dirent/include)
include_directories(${PROJECT_SOURCE_DIR}/third_partly/tarsgrammar)
include_directories(${PROJECT_SOURCE_DIR}/third_partly/tarsparse)
include_directories(${PROJECT_SOURCE_DIR}/third_partly/util/include)
include_directories(${PROJECT_SOURCE_DIR}/include)

# source
aux_source_directory(${PROJECT_SOURCE_DIR}/third_partly/tarsgrammar DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/third_partly/tarsparse DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/third_partly/util/src DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/src DIR_SRCS)
add_executable(${PROJECT_NAME} ${DIR_SRCS})