cmake_minimum_required(VERSION 2.6)

project(tars2node)

set(CMAKE_VERBOSE_MAKEFILE off)

# version
set(TARS_VERSION "2.4.5")
set(PARSER_VERSION "${TARS_VERSION}")
set(GENERATOR_VERSION "20200707")

# namespace
set(IDL_NAMESPACE Tars)
string(TOLOWER ${IDL_NAMESPACE} TC_NAMESPACE)
set(GRAMMAR_NAME Grammar)

# idl
set(RPC_MODULE_PATH "@tars/rpc")
set(STREAM_MODULE_PATH "@tars/stream")
set(IDL_TYPE "Tars")
set(PROTOCOL_NAME "Tup")

IF (APPLE)
link_libraries(iconv)
ENDIF(APPLE)

set(PLATFORM)
IF (UNIX)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -std=c++11  -Wno-deprecated -fno-strict-aliasing -Wno-overloaded-virtual")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-builtin-macro-redefined -D__FILE__='\"$(notdir $(abspath $<))\"'")
    
    set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -Wall -g")
    set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O2 -Wall -fno-strict-aliasing")

    set(PLATFORM "linux")
    IF(APPLE)
        set(PLATFORM "mac")
        SET(CMAKE_C_ARCHIVE_CREATE   "<CMAKE_AR> Scr <TARGET> <LINK_FLAGS> <OBJECTS>")
        SET(CMAKE_CXX_ARCHIVE_CREATE "<CMAKE_AR> Scr <TARGET> <LINK_FLAGS> <OBJECTS>")
        SET(CMAKE_C_ARCHIVE_FINISH   "<CMAKE_RANLIB> -no_warning_for_no_symbols -c <TARGET>")
        SET(CMAKE_CXX_ARCHIVE_FINISH "<CMAKE_RANLIB> -no_warning_for_no_symbols -c <TARGET>")
    ENDIF(APPLE)

ELSEIF (WIN32)
    set(PLATFORM "window")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /wd4101 /wd4244 /wd4996 /wd4091 /wd4503 /wd4819 /wd4200 /wd4800 /wd4267 /wd4834 /wd4267")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /bigobj " )

ELSE ()
    MESSAGE(STATUS "================ ERROR: This platform is unsupported!!! ================")
ENDIF (UNIX)

#编译的可执行程序输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin/${PLATFORM}/)

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
