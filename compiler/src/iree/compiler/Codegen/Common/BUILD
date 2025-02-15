# Copyright 2019 The IREE Authors
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
    name = "FoldTensorExtractOpIncGen",
    tbl_outs = [
        (
            ["--gen-rewriters"],
            "FoldTensorExtractOp.cpp.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "FoldTensorExtractOp.td",
    deps = [
        "@llvm-project//mlir:BufferizableOpInterfaceTdFiles",
        "@llvm-project//mlir:BufferizationOpsTdFiles",
        "@llvm-project//mlir:MemRefOpsTdFiles",
        "@llvm-project//mlir:OpBaseTdFiles",
        "@llvm-project//mlir:TensorOpsTdFiles",
    ],
)

iree_compiler_cc_library(
    name = "Common",
    srcs = [
        "BufferizationAnalysis.cpp",
        "BufferizeCopyOnlyDispatchesPass.cpp",
        "CleanupBufferAllocViewPass.cpp",
        "ConvertToDestinationPassingStylePass.cpp",
        "DestructiveUpdateUtils.cpp",
        "FlattenMemRefSubspanPass.cpp",
        "FoldAffineMinInDistributedLoops.cpp",
        "FoldTensorExtractOpPass.cpp",
        "ForOpCanonicalizationPass.cpp",
        "GPUDistributeSharedMemoryCopy.cpp",
        "GPUPipelining.cpp",
        "IREEComprehensiveBufferizePass.cpp",
        "InsertDistributionInfoPass.cpp",
        "LinalgBufferizePass.cpp",
        "MemrefCopyToLinalg.cpp",
        "OptimizeVectorTransferPass.cpp",
        "PolynomialApproximationPass.cpp",
        "RemoveTrivialLoops.cpp",
        "RewriteLinalgDestructiveUpdatesPass.cpp",
        "SetNumWorkgroupsPass.cpp",
        "TileAndDistributeToWorkgroupsPass.cpp",
        "TypePropagationPass.cpp",
        "VectorizeConv.cpp",
        "VectorizeMMT4d.cpp",
        "WorkGroupSwizzle.cpp",
    ],
    hdrs = [
        "BufferizationAnalysis.h",
        "DestructiveUpdateUtils.h",
        "Transforms.h",
    ],
    deps = [
        "//compiler/src/iree/compiler/Codegen:PassHeaders",
        "//compiler/src/iree/compiler/Codegen/Common:FoldTensorExtractOpIncGen",
        "//compiler/src/iree/compiler/Codegen/Dialect:IREECodegenDialect",
        "//compiler/src/iree/compiler/Codegen/Interfaces:BufferizationInterfaces",
        "//compiler/src/iree/compiler/Codegen/Transforms",
        "//compiler/src/iree/compiler/Codegen/Utils",
        "//compiler/src/iree/compiler/Dialect/Flow/IR",
        "//compiler/src/iree/compiler/Dialect/Flow/IR:PartitionableLoopsInterface",
        "//compiler/src/iree/compiler/Dialect/HAL/IR",
        "//compiler/src/iree/compiler/Dialect/Util/IR",
        "//llvm-external-projects/iree-dialects:IREELinalgExtDialect",
        "//llvm-external-projects/iree-dialects:IREELinalgExtPasses",
        "//llvm-external-projects/iree-dialects:IREELinalgExtTransforms",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:Affine",
        "@llvm-project//mlir:AffineUtils",
        "@llvm-project//mlir:Analysis",
        "@llvm-project//mlir:ArithmeticDialect",
        "@llvm-project//mlir:ArithmeticTransforms",
        "@llvm-project//mlir:BufferizationDialect",
        "@llvm-project//mlir:BufferizationTransforms",
        "@llvm-project//mlir:CFGTransforms",
        "@llvm-project//mlir:DialectUtils",
        "@llvm-project//mlir:FuncDialect",
        "@llvm-project//mlir:GPUDialect",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:LLVMCommonConversion",
        "@llvm-project//mlir:LLVMDialect",
        "@llvm-project//mlir:LinalgInterfaces",
        "@llvm-project//mlir:LinalgOps",
        "@llvm-project//mlir:LinalgTransforms",
        "@llvm-project//mlir:MathDialect",
        "@llvm-project//mlir:MathTransforms",
        "@llvm-project//mlir:MemRefDialect",
        "@llvm-project//mlir:MemRefTransforms",
        "@llvm-project//mlir:NVGPU",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:SCFDialect",
        "@llvm-project//mlir:SCFTransforms",
        "@llvm-project//mlir:SideEffectInterfaces",
        "@llvm-project//mlir:Support",
        "@llvm-project//mlir:TensorDialect",
        "@llvm-project//mlir:Transforms",
        "@llvm-project//mlir:VectorOps",
        "@llvm-project//mlir:VectorTransforms",
        "@llvm-project//mlir:ViewLikeInterface",
    ],
)
