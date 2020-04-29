package(default_visibility = ["//visibility:public"])

load(
    "@build_bazel_rules_apple//apple/internal:apple_framework_import.bzl",
    "apple_dynamic_framework_import",
)

apple_dynamic_framework_import(
    name = "Kingfisher",
    framework_imports = glob(["Carthage/Build/iOS/Kingfisher.framework/**"]),
)
