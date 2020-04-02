# Ogrenich Bazel

## Environment Prepare

Install Bazel `2.2.0` with [Homebrew](https://brew.sh):

```bash
brew tap bazelbuild/tap
brew install bazelbuild/tap/bazel
```

## iOS 13

1. Create a new Xcode project. iOS Single View App (Swift, Storyboards, Include Unit and UI Tests).

2. Remove `*.xcodeproj`.

3. Create a new `WORKSPACE` file with base dependencies.

4. Create a new `BUILD` file for the main target.

5. Update some env values in your main target's `Info.plist` file:
```
CFBundlePackageType: $(PRODUCT_BUNDLE_PACKAGE_TYPE) -> APPL
UISceneDelegateClassName: $(PRODUCT_MODULE_NAME).SceneDelegate -> *_Sources.SceneDelegate
```

6. Build project with Bazel:

```bash
bazel build //Bazel:*
```

7. Build with Bazel completed successfully! :tada:

8. Install Tulsi – Xcode Project Generator For Bazel: <https://github.com/bazelbuild/tulsi#building-and-installing>.

9. Create a new `*` project with Tulsi.

10. Add a `BUILD` file as a package in Tulsi project.

11. Create a new `*.tulsiproj` and save it on the same level with `WORKSPACE` file. You have to include `*` - `ios_application` and `Sources` – `swift_library`.

12. Add `*` and `external` Source Targets with a Recursive strategy and Save a new Config with `Default` name.

13. Generate Xcode Project with Tulsi and save it on the same level with `WORKSPACE` and `*.tulsiproj` files.

Finally, build and run your `*` App with Bazel in Xcode. :champagne:
