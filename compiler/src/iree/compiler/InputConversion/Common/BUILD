# Copyright 2021 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

load("//build_tools/bazel:build_defs.oss.bzl", "iree_compiler_cc_library")
load("//build_tools/bazel:iree_tablegen.bzl", "iree_gentbl_cc_library")

package(
    default_visibility = ["//visibility:public"],
    features = ["layering_check"],
    licenses = ["notice"],  # Apache 2.0
)

iree_gentbl_cc_library(
    name = "PassesIncGen",
    tbl_outs = [
        (
            ["--gen-pass-decls"],
            "Passes.h.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "Passes.td",
    deps = [
        "@llvm-project//mlir:PassBaseTdFiles",
    ],
)

iree_compiler_cc_library(
    name = "PassHeaders",
    hdrs = [
        "PassDetail.h",
        "Passes.h",
        "Passes.h.inc",
    ],
    deps = [
        ":PassesIncGen",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:Transforms",
    ],
)

iree_compiler_cc_library(
    name = "Common",
    srcs = [
        "IREEImportPublic.cpp",
        "Passes.cpp",
        "QuantizedMatmulToMatmul.cpp",
        "SanitizeModuleNames.cpp",
        "TopLevelSCFToCFG.cpp",
    ],
    hdrs = [
        "Passes.h",
    ],
    deps = [
        ":PassHeaders",
        ":PassesIncGen",
        "//compiler/src/iree/compiler/Dialect/Flow/IR",
        "//compiler/src/iree/compiler/Dialect/HAL/IR",
        "//compiler/src/iree/compiler/Dialect/Util/IR",
        "//llvm-external-projects/iree-dialects:IREEInputDialect",
        "@llvm-project//mlir:ArithmeticDialect",
        "@llvm-project//mlir:FuncDialect",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:LinalgOps",
        "@llvm-project//mlir:LinalgTransforms",
        "@llvm-project//mlir:MemRefTransforms",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:SCFDialect",
        "@llvm-project//mlir:SCFToControlFlow",
        "@llvm-project//mlir:TensorDialect",
        "@llvm-project//mlir:Transforms",
    ],
)
