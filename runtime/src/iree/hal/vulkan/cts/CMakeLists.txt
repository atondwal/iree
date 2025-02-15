# Copyright 2021 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

iree_hal_cts_test_suite(
  DRIVER_NAME
    vulkan
  DRIVER_REGISTRATION_HDR
    "runtime/src/iree/hal/vulkan/registration/driver_module.h"
  DRIVER_REGISTRATION_FN
    "iree_hal_vulkan_driver_module_register"
  COMPILER_TARGET_BACKEND
    "vulkan-spirv"
  EXECUTABLE_FORMAT
    "\"SPVE\""
  DEPS
    iree::hal::vulkan::registration
  EXCLUDED_TESTS
    # Non-push descriptor sets are not implemented in the Vulkan backend yet.
    "descriptor_set"
)
