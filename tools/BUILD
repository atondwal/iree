# Copyright 2019 The IREE Authors
#
# Licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

# Misc tools used to optimize, translate, and evaluate IREE.
# Compiler tooling, like the compiler, is not designed to run on device and is tagged as "hostonly".

package(
    default_visibility = ["//visibility:public"],
    features = ["layering_check"],
    licenses = ["notice"],  # Apache 2.0
)

exports_files(["lit.cfg.py"])

cc_binary(
    name = "iree-benchmark-module",
    srcs = ["iree-benchmark-module-main.cc"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:cc",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:file_io",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/modules/hal",
        "//runtime/src/iree/tools/utils:vm_util",
        "//runtime/src/iree/vm",
        "//runtime/src/iree/vm:bytecode_module",
        "//runtime/src/iree/vm:cc",
        "@com_google_benchmark//:benchmark",
    ],
)

cc_binary(
    name = "iree-benchmark-trace",
    srcs = ["iree-benchmark-trace-main.c"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:atomic_slist",
        "//runtime/src/iree/base/internal:file_path",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/testing:benchmark",
        "//runtime/src/iree/tools/utils:trace_replay",
        "//runtime/src/iree/tools/utils:yaml_util",
        "//runtime/src/iree/vm",
        "@com_github_yaml_libyaml//:yaml",
    ],
)

cc_binary(
    name = "iree-check-module",
    testonly = True,
    srcs = ["iree-check-module-main.cc"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:cc",
        "//runtime/src/iree/base:core_headers",
        "//runtime/src/iree/base:logging",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:file_io",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/modules/check",
        "//runtime/src/iree/modules/hal",
        "//runtime/src/iree/testing:gtest",
        "//runtime/src/iree/tools/utils:vm_util",
        "//runtime/src/iree/vm",
        "//runtime/src/iree/vm:bytecode_module",
    ],
)

cc_binary(
    name = "iree-dump-module",
    srcs = ["iree-dump-module-main.c"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base/internal:file_io",
        "//runtime/src/iree/base/internal/flatcc:debugging",
        "//runtime/src/iree/schemas:bytecode_module_def_c_fbs",
    ],
)

cc_library(
    name = "iree_opt_main",
    srcs = ["iree-opt-main.cc"],
    deps = [
        "//compiler/src/iree/compiler/Tools:init_passes_and_dialects",
        "//compiler/src/iree/compiler/Tools:init_targets",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:MlirOptLib",
        "@llvm-project//mlir:Support",
    ],
)

cc_binary(
    name = "iree-opt",
    tags = ["hostonly"],
    deps = [
        ":iree_opt_main",
    ],
)

cc_binary(
    name = "iree-mlir-lsp-server",
    srcs = ["iree-mlir-lsp-server.cc"],
    deps = [
        "//compiler/src/iree/compiler/Tools:init_passes_and_dialects",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:MlirLspServerLib",
        "@llvm-project//mlir:Support",
    ],
)

cc_binary(
    name = "iree-run-mlir",
    srcs = ["iree-run-mlir-main.cc"],
    tags = ["hostonly"],
    deps = [
        "//compiler/src/iree/compiler/Dialect/HAL/Target",
        "//compiler/src/iree/compiler/Dialect/VM/Target:init_targets",
        "//compiler/src/iree/compiler/Dialect/VM/Target/Bytecode",
        "//compiler/src/iree/compiler/Tools:init_passes_and_dialects",
        "//compiler/src/iree/compiler/Tools:init_targets",
        "//compiler/src/iree/compiler/Translation:IREEVM",
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:cc",
        "//runtime/src/iree/base:logging",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/modules/hal",
        "//runtime/src/iree/tools/utils:vm_util",
        "//runtime/src/iree/vm",
        "//runtime/src/iree/vm:bytecode_module",
        "//runtime/src/iree/vm:cc",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:LLVMToLLVMIRTranslation",
        "@llvm-project//mlir:Parser",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:Support",
        "@llvm-project//mlir:ToLLVMIRTranslation",
    ],
)

cc_binary(
    name = "iree-run-module",
    srcs = ["iree-run-module-main.cc"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:cc",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:file_io",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/modules/hal",
        "//runtime/src/iree/tools/utils:vm_util",
        "//runtime/src/iree/vm",
        "//runtime/src/iree/vm:bytecode_module",
        "//runtime/src/iree/vm:cc",
    ],
)

cc_binary(
    name = "iree-run-trace",
    srcs = ["iree-run-trace-main.c"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:file_path",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/tools/utils:trace_replay",
        "//runtime/src/iree/tools/utils:yaml_util",
        "//runtime/src/iree/vm",
        "@com_github_yaml_libyaml//:yaml",
    ],
)

cc_binary(
    name = "iree-e2e-matmul-test",
    srcs = ["iree-e2e-matmul-test.c"],
    deps = [
        "//runtime/src/iree/base",
        "//runtime/src/iree/base:core_headers",
        "//runtime/src/iree/base:tracing",
        "//runtime/src/iree/base/internal:file_path",
        "//runtime/src/iree/base/internal:flags",
        "//runtime/src/iree/hal",
        "//runtime/src/iree/hal/drivers",
        "//runtime/src/iree/modules/hal",
        "//runtime/src/iree/tools/utils:cpu_features",
        "//runtime/src/iree/tools/utils:trace_replay",
        "//runtime/src/iree/tools/utils:yaml_util",
        "//runtime/src/iree/vm",
        "@com_github_yaml_libyaml//:yaml",
    ],
)

cc_binary(
    name = "iree-tblgen",
    srcs = [
        "//compiler/src/iree/compiler/Dialect/Util/Tools:GenSrcs",
        "//compiler/src/iree/compiler/Dialect/VM/Tools:GenSrcs",
    ],
    tags = ["hostonly"],
    deps = [
        "//build_tools:default_linkopts",
        "//compiler/src/iree/compiler/Utils",
        "@llvm-project//llvm:Support",
        "@llvm-project//llvm:TableGen",
        "@llvm-project//mlir:MlirTableGenMain",
        "@llvm-project//mlir:Support",
        "@llvm-project//mlir:TableGen",
    ],
)

cc_binary(
    name = "iree-translate",
    srcs = ["iree-translate-main.cc"],
    tags = ["hostonly"],
    deps = [
        "//compiler/src/iree/compiler/Tools:iree_translate_lib",
    ],
)

cc_binary(
    name = "iree-compile",
    srcs = ["iree-compile-main.cc"],
    tags = ["hostonly"],
    deps = [
        "//compiler/src/iree/compiler/Tools:iree_translate_lib",
    ],
)
