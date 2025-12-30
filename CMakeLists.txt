# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(ESP32_Zephyr_WebServer_LED_Control)

target_sources(app PRIVATE src/main.c)

zephyr_linker_sources(SECTIONS sections-rom.ld)
zephyr_linker_section(NAME http_resource_desc_http_service
                      KVMA RAM_REGION GROUP RODATA_REGION)

set(gen_dir ${ZEPHYR_BINARY_DIR}/include/generated/)
set(source_file_index src/root.html)
generate_inc_file_for_target(app ${source_file_index} ${gen_dir}/root.html.gz.inc --gzip)

