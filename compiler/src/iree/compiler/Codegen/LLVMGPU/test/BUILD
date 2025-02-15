# Copyright 2021 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

# Tests for common transforms.

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
            "convert_to_nvvm.mlir",
            "convert_to_rocdl.mlir",
            "distribute_to_thread.mlir",
            "gpu_set_num_workgroups.mlir",
            "nvvm_pipeline_test.mlir",
            "pad_dynamic_alloc.mlir",
            "reduce_bank_conflicts.mlir",
            "rocdl_pipeline_test.mlir",
            "illegal_configuration.mlir",
            "legalize.mlir",
            "tensorcore_vectorization.mlir",
            "vector_to_gpu.mlir",
            "vectorization.mlir",
        ],
        include = ["*.mlir"],
    ),
    cfg = "//compiler:lit.cfg.py",
    tools = [
        "//tools:iree-opt",
        "@llvm-project//llvm:FileCheck",
    ],
)
