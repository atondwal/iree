# Copyright 2019 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

load("//build_tools/bazel:iree_lit_test.bzl", "iree_lit_test_suite")
load("//build_tools/bazel:enforce_glob.bzl", "enforce_glob")

package(
    default_visibility = ["//visibility:public"],
    features = ["layering_check"],
    licenses = ["notice"],  # Apache 2.0
)

iree_lit_test_suite(
    name = "lit",
    srcs = enforce_glob(
        [
            "allocator_ops.mlir",
            "attributes.mlir",
            "buffer_ops.mlir",
            "buffer_view_folding.mlir",
            "buffer_view_ops.mlir",
            "command_buffer_folding.mlir",
            "command_buffer_ops.mlir",
            "descriptor_set_ops.mlir",
            "device_ops.mlir",
            "executable_ops.mlir",
            "executable_targets.mlir",
            "experimental_ops.mlir",
            "interface_ops.mlir",
            "invalid.mlir",
            "semaphore_ops.mlir",
            "tensor_op_folding.mlir",
            "tensor_ops.mlir",
        ],
        include = ["*.mlir"],
    ),
    cfg = "//compiler:lit.cfg.py",
    tools = [
        "//tools:iree-opt",
        "@llvm-project//llvm:FileCheck",
    ],
)
