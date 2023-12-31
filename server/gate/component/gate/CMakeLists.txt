PROJECT(gate)
CMAKE_MINIMUM_REQUIRED(VERSION 3.0) 

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

set(gc_header_path ..//..//3rdparty//bdwgc//include CACHE PATH "gc include path")
INCLUDE_DIRECTORIES(${gc_header_path})

set(protocol_header_path ..//..//framework_proto CACHE PATH "protocol include path")
INCLUDE_DIRECTORIES(${protocol_header_path})
file(GLOB protcol_header_files ../../framework_proto/ ../../framework_proto/cpp/*.h)
AUX_SOURCE_DIRECTORY(../../framework_proto/ protocol_DIR_SRC)

set(juggle_header_path ..//..//juggle CACHE PATH "juggle include path")
INCLUDE_DIRECTORIES(${juggle_header_path})
file(GLOB juggle_header_files ../../juggle/ ../../juggle/*.h)
AUX_SOURCE_DIRECTORY(../../juggle/ juggle_DIR_SRC)

set(time_header_path ..//..//time CACHE PATH "time include path")
INCLUDE_DIRECTORIES(${time_header_path})
file(GLOB time_header_files ../../time/ ../../time/*.h)
AUX_SOURCE_DIRECTORY(../../time/ time_DIR_SRC)

set(config_header_path ..//..//config CACHE PATH "config include path")
INCLUDE_DIRECTORIES(${config_header_path})
file(GLOB config_header_files ../../config/ ../../config/*.h)

set(service_header_path ..//..//service CACHE PATH "service include path")
INCLUDE_DIRECTORIES(${service_header_path})
file(GLOB service_header_files ../../service/ ../../service/*.h)
AUX_SOURCE_DIRECTORY(../../service service_DIR_SRC)

set(log_header_path ..//..//log CACHE PATH "log include path")
INCLUDE_DIRECTORIES(${log_header_path})
file(GLOB log_header_files ../../log/ ../../log/*.h)

AUX_SOURCE_DIRECTORY(. DIR_SRC)
file(GLOB header_gate_files ./ ./*.h)

set(LIBS_DEBUG_PATH ${PROJECT_SOURCE_DIR}//..//..//lib_debug CACHE PATH "lib debug path")
set(LIBS_RELEASE_PATH ${PROJECT_SOURCE_DIR}//..//..//lib CACHE PATH "lib release path")

SET(header_files
    ${header_gate_files}
    ${service_header_files}
    ${juggle_header_files}
    ${protocol_header_files}
    ${config_header_files}
    ${time_header_files}
    ${log_header_files}
)

SET(SRC_LIST 
    ${DIR_SRC}
    ${juggle_DIR_SRC}
    ${service_DIR_SRC}
    ${protocol_DIR_SRC}
    ${time_DIR_SRC}
)

ADD_LIBRARY(gate ${SRC_LIST} ${header_files})