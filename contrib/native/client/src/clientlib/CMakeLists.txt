#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

# Drill Client library

set (CLIENTLIB_SRC_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/decimalUtils.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/drillClient.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/drillClientImpl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/fieldmeta.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/metadata.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/recordBatch.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/rpcMessage.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/errmsgs.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/logger.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/utils.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/saslAuthenticatorImpl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/zookeeperClient.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../include )
include_directories(${PROTOBUF_INCLUDE_DIR})
include_directories(${Zookeeper_INCLUDE_DIRS})
include_directories(${SASL_INCLUDE_DIRS})

link_directories(/usr/local/lib)

set_property(
    DIRECTORY
    PROPERTY COMPILE_DEFINITIONS_DEBUG DEBUG DEBUG=1 THREADED
    )

if(MSVC)
    set(CMAKE_CXX_FLAGS "/EHsc")
    add_definitions(-DDRILL_CLIENT_EXPORTS -D_SCL_SECURE_NO_WARNINGS)
endif()

add_library(drillClient SHARED ${CLIENTLIB_SRC_FILES} )
target_link_libraries(drillClient ${Boost_LIBRARIES} ${PROTOBUF_LIBRARY} ${Zookeeper_LIBRARIES} ${SASL_LIBRARIES} protomsgs y2038)
