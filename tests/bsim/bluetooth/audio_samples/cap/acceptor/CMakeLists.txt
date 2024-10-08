# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(cap_acceptor_self_tets)

set(cap_acceptor_path ${ZEPHYR_BASE}/samples/bluetooth/cap_acceptor)

target_sources(app PRIVATE
  ${cap_acceptor_path}/src/main.c
)

zephyr_sources_ifdef(CONFIG_SAMPLE_UNICAST ${cap_acceptor_path}/src/cap_acceptor_unicast.c)
zephyr_sources_ifdef(CONFIG_SAMPLE_BROADCAST ${cap_acceptor_path}/src/cap_acceptor_broadcast.c)

target_sources(app PRIVATE
	src/cap_acceptor_sample_test.c
	src/test_main.c
)

zephyr_library_include_directories(${ZEPHYR_BASE}/samples/bluetooth)

zephyr_include_directories(
  ${BSIM_COMPONENTS_PATH}/libUtilv1/src/
  ${BSIM_COMPONENTS_PATH}/libPhyComv1/src/
  )
