# Ogrenich Bazel

## Prepare Environment

###### Install [Bazelisk](https://github.com/bazelbuild/bazeliskhttps://github.com/bazelbuild/bazelisk) `1.3.0` as Bazel through [Homebrew](https://brew.sh):

```bash
brew install bazelisk@1.3.0
ln -s /user/local/Cellar/bazelisk/1.3.0/bin/bazelisk /user/local/bin/bazel
```

## iOS

###### 1. Create a new Xcode project. iOS Single View App (Swift, Storyboards, Include Unit and UI Tests).

###### 2. Remove `*.xcodeproj`.

###### 3. Create a new `WORKSPACE` file with base dependencies.

###### 4. Create a new `BUILD` file for the main target.

###### 5. Update some env values in your main target's `Info.plist` file:
```
CFBundlePackageType: $(PRODUCT_BUNDLE_PACKAGE_TYPE) -> APPL
UISceneDelegateClassName: $(PRODUCT_MODULE_NAME).SceneDelegate -> *_Sources.SceneDelegate
```

###### 6. Add a new `.bazelversion` and specify exact version of Bazel in it.

###### 7. Build project with Bazel:

```bash
bazel build //Bazel:*
```

###### 8. Build with Bazel completed successfully! :tada:

###### 9. Install Tulsi – Xcode Project Generator For Bazel: <https://github.com/bazelbuild/tulsi#building-and-installing>.

###### 10. Create a new `*` project with Tulsi.

###### 11. Add a `BUILD` file as a package in Tulsi project.

###### 12. Create a new `*.tulsiproj` and save it on the same level with `WORKSPACE` file. You have to include `*` - `ios_application` and `Sources` – `swift_library`.

###### 13. Add `*` and `external` Source Targets with a Recursive strategy and Save a new Config with `Default` name.

###### 14. Generate Xcode Project with Tulsi and save it on the same level with `WORKSPACE` and `*.tulsiproj` files.

#### Finally, build and run your `*` App with Bazel in Xcode. :champagne:

### iOS Build with Remote Cache :construction_worker:

###### 1. Clean Build + Upload Actions and Outputs to Remote Cache.
###### Elapsed time: `121.182s`

```bash
iOS$: bazel clean && bazel build //Bazel:Bazel --remote_cache=grpcs://* --remote_header="authorization=:key:"
2020/04/03 18:37:33 Downloading https://releases.bazel.build/3.0.0/rc2/bazel-3.0.0rc2-darwin-x86_64...
Extracting Bazel installation...
Starting local Bazel server and connecting to it...
INFO: Starting clean.
INFO: Invocation ID: *
DEBUG: Rule 'build_bazel_rules_apple' indicated that a canonical reproducible form can be obtained by modifying arguments commit = "19f031f09185e0fcd722c22e596d09bd6fff7944", shallow_since = "1570721035 -0700" and dropping ["tag"]
DEBUG: Call stack for the definition of repository 'build_bazel_rules_apple' which is a git_repository (rule definition at /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/bazel_tools/tools/build_defs/repo/git.bzl:195:18):
 - <builtin>
 - /Users/ogrenich/Developer/ogrenich/ogrenich-bazel/Examples/iOS/WORKSPACE:32:1
DEBUG: Rule 'build_bazel_apple_support' indicated that a canonical reproducible form can be obtained by modifying arguments commit = "8c585c66c29b9d528e5fcf78da8057a6f3a4f001", shallow_since = "1570646613 -0700" and dropping ["tag"]
DEBUG: Call stack for the definition of repository 'build_bazel_apple_support' which is a git_repository (rule definition at /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/bazel_tools/tools/build_defs/repo/git.bzl:195:18):
 - <builtin>
 - /Users/ogrenich/Developer/ogrenich/ogrenich-bazel/Examples/iOS/WORKSPACE:38:1
DEBUG: Rule 'build_bazel_rules_swift' indicated that a canonical reproducible form can be obtained by modifying arguments commit = "ebef63d4fd639785e995b9a2b20622ece100286a", shallow_since = "1570649187 -0700" and dropping ["tag"]
DEBUG: Call stack for the definition of repository 'build_bazel_rules_swift' which is a git_repository (rule definition at /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/bazel_tools/tools/build_defs/repo/git.bzl:195:18):
 - <builtin>
 - /Users/ogrenich/Developer/ogrenich/ogrenich-bazel/Examples/iOS/WORKSPACE:44:1
DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `bazel_skylib` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/bazel-skylib.git (tag 0.9.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_apple_support` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/apple_support.git (tag 0.7.2). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_rules_swift` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/rules_swift.git (tag 0.13.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: Rule 'bazel_skylib' indicated that a canonical reproducible form can be obtained by modifying arguments commit = "2b38b2f8bd4b8603d610cfc651fcbb299498147f", shallow_since = "1562957722 -0400" and dropping ["tag"]
DEBUG: Call stack for the definition of repository 'bazel_skylib' which is a git_repository (rule definition at /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/bazel_tools/tools/build_defs/repo/git.bzl:195:18):
 - <builtin>
 - /Users/ogrenich/Developer/ogrenich/ogrenich-bazel/Examples/iOS/WORKSPACE:22:1
INFO: Analyzed target //Bazel:Bazel (40 packages loaded, 883 targets configured).
INFO: Found 1 target...
INFO: Deleting stale sandbox base /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/sandbox
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 121.182s, Critical Path: 39.62s
INFO: 217 processes: 209 darwin-sandbox, 7 local, 1 worker.
INFO: Build completed successfully, 245 total actions
```

###### 2. Clean Build + Retrieve Actions and Outputs from Remote Cache.
###### Elapsed time: `44.139s`

```bash
iOS$: bazel clean && bazel build //Bazel:Bazel --remote_cache=grpcs://* --remote_header="authorization=:key:"
INFO: Starting clean.
INFO: Invocation ID: *
DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `bazel_skylib` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/bazel-skylib.git (tag 0.9.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_apple_support` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/apple_support.git (tag 0.7.2). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_rules_swift` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/rules_swift.git (tag 0.13.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

INFO: Analyzed target //Bazel:Bazel (40 packages loaded, 883 targets configured).
INFO: Found 1 target...
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 44.139s, Critical Path: 19.13s
INFO: 217 processes: 216 remote cache hit, 1 local.
INFO: Build completed successfully, 245 total actions
```

###### 3. Clean Build, Without Remote Cache.
###### Elapsed time: `77.803s`

```bash
iOS$: bazel clean && bazel build //Bazel:Bazel
INFO: Starting clean.
DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `bazel_skylib` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/bazel-skylib.git (tag 0.9.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_apple_support` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/apple_support.git (tag 0.7.2). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

DEBUG: /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/external/build_bazel_rules_apple/apple/repositories.bzl:35:5:
WARNING: `build_bazel_rules_apple` depends on `build_bazel_rules_swift` loaded from None (tag None), but we have detected it already loaded into your workspace from https://github.com/bazelbuild/rules_swift.git (tag 0.13.0). You may run into compatibility issues. To silence this warning, pass `ignore_version_differences = True` to `apple_rules_dependencies()`.

INFO: Analyzed target //Bazel:Bazel (40 packages loaded, 883 targets configured).
INFO: Found 1 target...
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 77.803s, Critical Path: 22.82s
INFO: 217 processes: 209 darwin-sandbox, 7 local, 1 worker.
INFO: Build completed successfully, 245 total actions
```

#### Result: Build with Remote Cache `~x2 faster` :rocket:
