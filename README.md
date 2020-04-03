# Ogrenich Bazel

## Prepare Environment

Install [Bazelisk](https://github.com/bazelbuild/bazeliskhttps://github.com/bazelbuild/bazelisk) `1.3.0` as Bazel through [Homebrew](https://brew.sh):

```bash
brew install bazelisk@1.3.0
ln -s /user/local/Cellar/bazelisk/1.3.0/bin/bazelisk /user/local/bin/bazel
```

## iOS

1. Create a new Xcode project. iOS Single View App (Swift, Storyboards, Include Unit and UI Tests).

2. Remove `*.xcodeproj`.

3. Create a new `WORKSPACE` file with base dependencies.

4. Create a new `BUILD` file for the main target.

5. Update some env values in your main target's `Info.plist` file:
```
CFBundlePackageType: $(PRODUCT_BUNDLE_PACKAGE_TYPE) -> APPL
UISceneDelegateClassName: $(PRODUCT_MODULE_NAME).SceneDelegate -> *_Sources.SceneDelegate
```

6. Add a new `.bazelversion` and specify exact version of Bazel in it.

7. Build project with Bazel:

```bash
bazel build //Bazel:*
```

8. Build with Bazel completed successfully! :tada:

9. Install Tulsi – Xcode Project Generator For Bazel: <https://github.com/bazelbuild/tulsi#building-and-installing>.

10. Create a new `*` project with Tulsi.

11. Add a `BUILD` file as a package in Tulsi project.

12. Create a new `*.tulsiproj` and save it on the same level with `WORKSPACE` file. You have to include `*` - `ios_application` and `Sources` – `swift_library`.

13. Add `*` and `external` Source Targets with a Recursive strategy and Save a new Config with `Default` name.

14. Generate Xcode Project with Tulsi and save it on the same level with `WORKSPACE` and `*.tulsiproj` files.

Finally, build and run your `*` App with Bazel in Xcode. :champagne:
