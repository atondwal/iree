# Copyright 2022 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

# Tests for common transforms.

load("//build_tools/bazel:build_defs.oss.bzl", "iree_cmake_extra_content")
load("//build_tools/bazel:enforce_glob.bzl", "enforce_glob")
load("//build_tools/bazel:iree_lit_test.bzl", "iree_lit_test_suite")

package(
    default_visibility = ["//visibility:public"],
    features = ["layering_check"],
    licenses = ["notice"],  # Apache 2.0
)

iree_cmake_extra_content(
    content = """
if(NOT IREE_BUILD_TORCH_MLIR_SUPPORT)
  return()
endif()
""",
)

iree_lit_test_suite(
    name = "lit",
    srcs = enforce_glob(
        [
            "convert_tm_tensor_to_linalg_ext.mlir",
        ],
        include = ["*.mlir"],
    ),
    cfg = "//compiler:lit.cfg.py",
    tools = [
        "//tools:iree-opt",
        "@llvm-project//llvm:FileCheck",
    ],
)
