# Ogrenich Bazel


## Prepare Environment

###### Install [Bazelisk](https://github.com/bazelbuild/bazeliskhttps://github.com/bazelbuild/bazelisk) `1.4.0` as Bazel through [Homebrew](https://brew.sh):

```bash
brew install bazelisk@1.4.0
ln -s /user/local/Cellar/bazelisk/1.4.0/bin/bazelisk /user/local/bin/bazel
```


## iOS

###### 1. Create a new Xcode project. iOS Single View App (Swift, Storyboards, Include Unit and UI Tests).

###### [Optional] (Carthage) Create a new `Cartfile` file with dependencies and run:

```bash
carthage bootstrap --platform iOS
```

###### 2. Create a new `WORKSPACE` file with base dependencies.

###### 3. Create a new `BUILD` file for the main target.

###### [Optional] (Carthage) Create an additional `BUILD` file in the root directory of the iOS project with imports of dynamic frameworks.

###### 4. Update some env values in your main target's `Info.plist` file:
```
CFBundlePackageType: $(PRODUCT_BUNDLE_PACKAGE_TYPE) -> APPL
UISceneDelegateClassName: $(PRODUCT_MODULE_NAME).SceneDelegate -> *_Sources.SceneDelegate
```

###### 5. Add a new `.bazelversion` and specify exact version of Bazel in it. Additionally add a new `.bazelrc` with predefined build flags for iOS.

###### 6. Build project with Bazel:

```bash
bazel build //*:* --spawn_strategy=local --apple_platform_type=ios --cpu=ios_x86_64
```

###### 7. Build iOS App with Bazel completed successfully! :tada:

###### 8. Install Tulsi `0.20200219.88` – Xcode Project Generator For Bazel: <https://github.com/bazelbuild/tulsi#building-and-installing>.

###### 9. Remove `*.xcodeproj`.

###### 10. Create a new `*.tulsiproj` and save it on the same level with `WORKSPACE` file.

###### 11. Add `*/BUILD` file associated with the project as a Package to the created Tulsi's project. Repeat this step if you have more than one `BUILD` file containing targets you wish to build directly.

###### 12. Next, you have to select one or more targets that you want to build in Xcode, for example `*` - `ios_application` and `Sources` – `swift_library`.

###### 13. Select one or more `Source Targets` with a Recursive strategy (Optional). This allows you to select a working set from your full source tree that best matches the portion of the project that you're likely to edit. Save a new Config with the `Default` name.

###### 14. Generate a new Xcode Project with Tulsi and save it on the same level with `WORKSPACE` and `*.tulsiproj` files.

#### Finally, build and run your `*` App with Bazel in Xcode. :champagne:



### iOS Build Benchmarks :construction_worker:

###### 1. Cold Build iOS App (Carthage) with Xcode.
###### Build time: `11.592s`


###### 2. Cold Build with Bazel without Remote Cache.
###### Elapsed time: `71.736s`

```bash
iOS$: bazel clean && bazel build //*:*
INFO: Starting clean.
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 71.736s, Critical Path: 25.28s
INFO: 217 processes: 217 local.
INFO: Build completed successfully, 245 total actions
```

###### 3. Cold Build with Bazel + Upload Actions and Outputs to Remote Cache.
###### Elapsed time: `86.610s`

```bash
iOS$: bazel clean && bazel build //*:* --remote_cache=grpcs://* --remote_header="authorization=:key:"
INFO: Starting clean.
INFO: Invocation ID: *
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: Deleting stale sandbox base /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/sandbox
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 86.610s, Critical Path: 34.90s
INFO: 217 processes: 4 remote cache hit, 213 local.
INFO: Build completed successfully, 245 total actions
```

###### 4. Cold Build with Bazel + Retrieve Actions and Outputs from Remote Cache.
###### Elapsed time: `10.451s`

```bash
iOS$: bazel clean && bazel build //*:* --remote_cache=grpcs://* --remote_header="authorization=:key:"
INFO: Starting clean.
INFO: Invocation ID: *
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 10.451s, Critical Path: 3.92s
INFO: 217 processes: 216 remote cache hit, 1 local.
INFO: Build completed successfully, 245 total actions
```

#### Result: Overall speedup Bazel with Remote Cache is `~x7 faster` :rocket:
