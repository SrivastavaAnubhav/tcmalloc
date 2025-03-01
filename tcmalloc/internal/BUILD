# Copyright 2019 The TCMalloc Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Internal libraries used for the implementation and testing of TCMalloc.

load("@rules_fuzzing//fuzzing:cc_defs.bzl", "cc_fuzz_test")
load("@rules_cc//cc:defs.bzl", "cc_proto_library")
load("@rules_proto//proto:defs.bzl", "proto_library")
load("//tcmalloc:copts.bzl", "TCMALLOC_DEFAULT_COPTS")
load("//tcmalloc:variants.bzl", "create_tcmalloc_benchmark")

package(default_visibility = ["//visibility:private"])

licenses(["notice"])

cc_library(
    name = "affinity",
    testonly = 1,
    srcs = ["affinity.cc"],
    hdrs = ["affinity.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "affinity_test",
    srcs = ["affinity_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":affinity",
        ":percpu",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "atomic_danger",
    hdrs = ["atomic_danger.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = ["//visibility:private"],
    deps = [":config"],
)

cc_library(
    name = "atomic_stats_counter",
    hdrs = ["atomic_stats_counter.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "clock",
    hdrs = ["clock.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "config",
    hdrs = ["config.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "config_test",
    srcs = ["config_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":config",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "declarations",
    hdrs = ["declarations.h"],
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
)

cc_library(
    name = "environment",
    srcs = ["environment.cc"],
    hdrs = ["environment.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [":config"],
)

cc_test(
    name = "environment_test",
    srcs = ["environment_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":environment",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "fake_profile",
    hdrs = ["fake_profile.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        "//tcmalloc:malloc_extension",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "lifetime_predictions",
    hdrs = ["lifetime_predictions.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":linked_list",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "lifetime_predictions_test",
    srcs = ["lifetime_predictions_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":lifetime_predictions",
        "//tcmalloc/testing:testutil",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "lifetime_tracker",
    hdrs = ["lifetime_tracker.h"],
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":clock",
        ":lifetime_predictions",
        ":linked_list",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "lifetime_tracker_test",
    srcs = ["lifetime_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":clock",
        ":lifetime_predictions",
        ":lifetime_tracker",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "linked_list",
    hdrs = ["linked_list.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)

create_tcmalloc_benchmark(
    name = "linked_list_benchmark",
    srcs = ["linked_list_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
    deps = [
        ":linked_list",
        ":logging",
        ":mock_span",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "linked_list_test",
    size = "small",
    srcs = ["linked_list_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":linked_list",
        ":mock_span",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "linux_syscall_support",
    hdrs = ["linux_syscall_support.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
)

cc_library(
    name = "logging",
    srcs = ["logging.cc"],
    hdrs = ["logging.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__pkg__",
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":parameter_accessors",
        "//tcmalloc:malloc_extension",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "logging_test",
    srcs = ["logging_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    data = [
    ],
    deps = [
        ":logging",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_binary(
    name = "logging_test_helper",
    testonly = 1,
    srcs = ["logging_test_helper.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
)

cc_library(
    name = "memory_stats",
    srcs = ["memory_stats.cc"],
    hdrs = ["memory_stats.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":page_size",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "memory_stats_test",
    srcs = ["memory_stats_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":memory_stats",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "mincore",
    srcs = ["mincore.cc"],
    hdrs = ["mincore.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        ":config",
        ":page_size",
    ],
)

cc_library(
    name = "residency",
    srcs = ["residency.cc"],
    hdrs = ["residency.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        ":config",
        ":page_size",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

create_tcmalloc_benchmark(
    name = "mincore_benchmark",
    srcs = ["mincore_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":logging",
        ":mincore",
        ":page_size",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "mincore_test",
    srcs = ["mincore_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":mincore",
        ":page_size",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_test(
    name = "residency_test",
    srcs = ["residency_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":page_size",
        ":residency",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "mock_span",
    testonly = 1,
    hdrs = ["mock_span.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":linked_list",
    ],
)

cc_library(
    name = "cache_topology",
    srcs = ["cache_topology.cc"],
    hdrs = ["cache_topology.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "cache_topology_test",
    srcs = ["cache_topology_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":cache_topology",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "numa",
    srcs = ["numa.cc"],
    hdrs = ["numa.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":environment",
        ":logging",
        ":percpu",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_fuzz_test(
    name = "numa_fuzz",
    testonly = 1,
    srcs = ["numa_fuzz.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":numa",
    ],
)

cc_test(
    name = "numa_test",
    srcs = ["numa_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":logging",
        ":numa",
        ":percpu",
        "//tcmalloc:want_numa_aware",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "optimization",
    hdrs = ["optimization.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "overflow",
    hdrs = ["overflow.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "page_size",
    srcs = ["page_size.cc"],
    hdrs = ["page_size.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "parameter_accessors",
    hdrs = ["parameter_accessors.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//base:__pkg__",
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "percpu",
    srcs = [
        "percpu.cc",
        "percpu_rseq_asm.S",
        "percpu_rseq_unsupported.cc",
    ],
    hdrs = ["percpu.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    textual_hdrs = [
        "percpu_rseq_aarch64.S",
        "percpu_rseq_x86_64.S",
    ],
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        ":atomic_danger",
        ":config",
        ":linux_syscall_support",
        ":logging",
        ":optimization",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "percpu_tcmalloc",
    hdrs = ["percpu_tcmalloc.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":mincore",
        ":percpu",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "percpu_tcmalloc_test",
    timeout = "long",
    srcs = ["percpu_tcmalloc_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    malloc = "//tcmalloc:tcmalloc_deprecated_perthread",
    deps = [
        ":affinity",
        ":config",
        ":logging",
        ":page_size",
        ":percpu_tcmalloc",
        ":util",
        "//tcmalloc:malloc_extension",
        "//tcmalloc/testing:testutil",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "prefetch",
    hdrs = ["prefetch.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "prefetch_test",
    srcs = ["prefetch_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":prefetch",
        "@com_google_googletest//:gtest_main",
    ],
)

proto_library(
    name = "profile_proto",
    srcs = ["profile.proto"],
)

cc_proto_library(
    name = "profile_cc_proto",
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [":profile_proto"],
)

cc_library(
    name = "profile_builder",
    srcs = ["profile_builder.cc"],
    hdrs = ["profile_builder.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = ["//tcmalloc:__subpackages__"],
    deps = [
        ":logging",
        ":residency",
        "//tcmalloc:malloc_extension",
        "//tcmalloc/internal:profile_cc_proto",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_fuzz_test(
    name = "profile_builder_fuzz",
    testonly = 1,
    srcs = ["profile_builder_fuzz.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":profile_builder",
    ],
)

cc_test(
    name = "profile_builder_test",
    srcs = ["profile_builder_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    data = [
        "testdata/b180635896.so",
    ],
    deps = [
        ":environment",
        ":fake_profile",
        ":page_size",
        ":profile_builder",
        "//tcmalloc:malloc_extension",
        "//tcmalloc/internal:profile_cc_proto",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "proc_maps",
    srcs = ["proc_maps.cc"],
    hdrs = ["proc_maps.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        ":util",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_library(
    name = "range_tracker",
    hdrs = ["range_tracker.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        ":optimization",
        "@com_google_absl//absl:absl_shared",
    ],
)

create_tcmalloc_benchmark(
    name = "range_tracker_benchmark",
    srcs = ["range_tracker_benchmark.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    malloc = "//tcmalloc",
    deps = [
        ":range_tracker",
        "@com_github_google_benchmark//:benchmark",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "range_tracker_test",
    srcs = ["range_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    deps = [
        ":range_tracker",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "stacktrace_filter",
    hdrs = ["stacktrace_filter.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "stacktrace_filter_test",
    srcs = ["stacktrace_filter_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":stacktrace_filter",
        "//tcmalloc/testing:thread_manager",
        "@com_google_absl//absl:absl_shared",
        "@com_google_googletest//:gtest_main",
    ],
)

# An empty rule to force libc malloc instead of TCMalloc.
cc_library(
    name = "system_malloc",
    copts = TCMALLOC_DEFAULT_COPTS,
    linkstatic = 1,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
)

cc_library(
    name = "timeseries_tracker",
    hdrs = ["timeseries_tracker.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":clock",
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)

cc_test(
    name = "timeseries_tracker_test",
    srcs = ["timeseries_tracker_test.cc"],
    copts = TCMALLOC_DEFAULT_COPTS,
    deps = [
        ":timeseries_tracker",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "util",
    srcs = ["util.cc"],
    hdrs = ["util.h"],
    copts = TCMALLOC_DEFAULT_COPTS,
    visibility = [
        "//tcmalloc:__subpackages__",
    ],
    deps = [
        ":config",
        ":logging",
        "@com_google_absl//absl:absl_shared",
    ],
)
