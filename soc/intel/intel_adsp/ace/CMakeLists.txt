# Intel ACE SoC family CMake file
#
# Copyright (c) 2022-2024 Intel Corporation
# SPDX-License-Identifier: Apache-2.0


zephyr_library_sources(
  sram.c
  multiprocessing.c
  irq.c
  power_down.S
  power.c
  boot.c
  timestamp.c
  )

zephyr_library_sources_ifdef(CONFIG_GDBSTUB
    gdbstub.c
    )

zephyr_include_directories(include)
zephyr_include_directories(include/${CONFIG_SOC})
zephyr_library_sources_ifdef(CONFIG_SOC_INTEL_COMM_WIDGET comm_widget.c)
zephyr_library_sources_ifdef(CONFIG_SOC_INTEL_COMM_WIDGET comm_widget_messages.c)
zephyr_library_sources_ifdef(
  CONFIG_SOC_SERIES_INTEL_ADSP_ACE_CUSTOM_MORE_SPIN_RELAX_NOPS
  spin_relax.c
)

if (CONFIG_XTENSA_MMU)
  zephyr_library_sources_ifdef(CONFIG_SOC_INTEL_ACE30 mmu_ace30.c)
endif()

set(SOC_LINKER_SCRIPT ${CMAKE_CURRENT_SOURCE_DIR}/linker.ld CACHE INTERNAL "")
