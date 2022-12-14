# Copyright (c) 2021 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

include(GoogleTest)

set(TEST_NAME netsocket-udp-socket-unittest)

add_executable(${TEST_NAME})

target_compile_definitions(${TEST_NAME}
    PRIVATE
        MBED_CONF_NSAPI_DNS_ADDRESSES_LIMIT=10
)

target_sources(${TEST_NAME}
    PRIVATE
        ${mbed-os_SOURCE_DIR}/connectivity/netsocket/source/SocketAddress.cpp
        ${mbed-os_SOURCE_DIR}/connectivity/netsocket/source/InternetSocket.cpp
        ${mbed-os_SOURCE_DIR}/connectivity/netsocket/source/InternetDatagramSocket.cpp
        ${mbed-os_SOURCE_DIR}/connectivity/netsocket/source/UDPSocket.cpp
        ${mbed-os_SOURCE_DIR}/connectivity/libraries/nanostack-libservice/source/libip6string/ip6tos.c
        ${mbed-os_SOURCE_DIR}/connectivity/libraries/nanostack-libservice/source/libip6string/stoip6.c
        ${mbed-os_SOURCE_DIR}/connectivity/libraries/nanostack-libservice/source/libBits/common_functions.c
        test_UDPSocket.cpp
)

target_link_libraries(${TEST_NAME}
    PRIVATE
        mbed-headers-drivers
        mbed-headers-rtos
        mbed-headers-nanostack-libservice
        mbed-headers-netsocket
        mbed-stubs
        mbed-stubs-headers
        mbed-stubs-netsocket
        mbed-stubs-nanostack-libservice
        gmock_main
)

gtest_discover_tests(${TEST_NAME} PROPERTIES LABELS "netsocket")
