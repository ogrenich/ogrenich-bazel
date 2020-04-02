load(
    "@build_bazel_rules_swift//swift:swift.bzl",
    "swift_library",
)

load(
    "@build_bazel_rules_apple//apple:ios.bzl",
    "ios_application",
)

load(
    "@bazel_skylib//rules:build_test.bzl",
    "build_test",
)

swift_library(
    name = "Sources",
    srcs = [
        "SceneDelegate.swift",
        "AppDelegate.swift",
        "ViewController.swift",
    ],
    data = [
        "Base.lproj/Main.storyboard",
    ],
    visibility = ["//visibility:public"],
)

ios_application(
    name = "Bazel",
    app_icons = glob(["Assets.xcassets/**"]),
    bundle_id = "com.ogrenich.bazel",
    families = [
        "iphone",
        "ipad",
    ],
    infoplists = ["Info.plist"],
    launch_storyboard = "Base.lproj/LaunchScreen.storyboard",
    minimum_os_version = "13.0",
    visibility = ["//visibility:public"],
    deps = [":Sources"],
)
