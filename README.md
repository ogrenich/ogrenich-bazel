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
bazel build //*:* --apple_platform_type=ios --cpu=ios_x86_64
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

###### 1. Clean Xcode Build.
###### Build time: ``


###### 2. Clean Bazel Build, Without Remote Cache.
###### Elapsed time: `81.784s`

```bash
iOS$: bazel clean && bazel build //*:*
INFO: Starting clean.
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 81.784s, Critical Path: 31.51s
INFO: 217 processes: 209 darwin-sandbox, 7 local, 1 worker.
INFO: Build completed successfully, 245 total actions
```

###### 3. Clean Bazel Build + Upload Actions and Outputs to Remote Cache.
###### Elapsed time: `103.885s`

```bash
iOS$: bazel clean && bazel build //*:* --remote_cache=grpcs://* --remote_header="authorization=:key:"
Starting local Bazel server and connecting to it...
INFO: Starting clean.
INFO: Invocation ID: eca27bad-d7ef-4f6f-9e4b-9046d025e409
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: Deleting stale sandbox base /private/var/tmp/_bazel_ogrenich/9f59e9f84bd18008bcc3b7847193ed95/sandbox
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 103.885s, Critical Path: 42.74s
INFO: 217 processes: 209 darwin-sandbox, 7 local, 1 worker.
INFO: Build completed successfully, 245 total actions
```

###### 4. Clean Build + Retrieve Actions and Outputs from Remote Cache.
###### Elapsed time: `24.205s`

```bash
iOS$: bazel clean && bazel build //*:* --remote_cache=grpcs://* --remote_header="authorization=:key:"
INFO: Starting clean.
INFO: Invocation ID: a25d976c-c055-45c6-88c4-b1fb80a2c17e
INFO: Analyzed target //Bazel:Bazel (41 packages loaded, 873 targets configured).
INFO: Found 1 target...
INFO: From Processing and signing Bazel:
bazel-out/ios_x86_64-fastbuild/bin/Bazel/Bazel_archive-root/Payload/Bazel.app/Frameworks/Kingfisher.framework: replacing existing signature
Target //Bazel:Bazel up-to-date:
  bazel-bin/Bazel/Bazel.ipa
INFO: Elapsed time: 24.205s, Critical Path: 12.01s
INFO: 217 processes: 216 remote cache hit, 1 local.
INFO: Build completed successfully, 245 total actions
```

#### Result: Build with Remote Cache `~x4 faster` :rocket:
