# Embedded iOS Frameworks in Titanium
Support embedded frameworks in native Titanium modules and Hyperloop. 
To add Swift framework-support to your module, check out the [hook-swift-frameworks](https://github.com/appcelerator-modules/hook-swift-frameworks) repository 🙌.

### ⚠️ DEPRECATION-WARNING
If you are using Titanium SDK 6.2.0 or later, this hook is not required anymore, as full dynamic-lbrary support is already
integrated into the SDK. If you are having an open-source module that targets SDK < 6.2.0, you can still support both techniques, since the hook will detect the SDK version and skip further adjustments if already existing.

### Usage
1. Download the `ti.dynamiclib.js` file and open it
2. Search for the `frameworkPaths` and specify your framework path(s). The paths are relative to the `build/iphone` directory
3. Adjust your module project code
    - For classic modules:
        * Add `LD_RUNPATH_SEARCH_PATHS=$(inherited) "@executable_path/Frameworks" $(FRAMEWORK_SEARCH_PATHS)` to your module.xcconfig
        * Place the `ti.dynamiclib.js` file in `<your-module-ios-root>/hooks`
    - For Hyperloop modules (will be automated in future Hyperloop versions - Follow TIMOB-23853):
        * Add the above to the `hyperloop.ios.xcodebuild.flags` object of your appc.js
        * Place the `ti.dynamiclib.js` file in `<your-project-root>/plugins/ti.dynamiclib/hooks`
        * Add the plugin to your tiapp: `<plugin>ti.dynamiclib</plugin>`
4. Some frameworks include Simulator architectures ("fat libraries"). Those frameworks usually provide a script to strip the unused architectures for distribution, e.g. `strip-framework.sh`. If you use such a framework, adjust the path of the variable `scriptPath`, otherwise `null` it to skip the build script phase. An example of this file is included in this repo (© Realm).
5. That's it! You can check an example integration in the Ti.Flic module (https://github.com/hansemannn/ti.flic)

### License
Apache 2.0

### Legal
This module is Copyright (c) 2016-present by Axway Appcelerator. All Rights Reserved. Usage of this module is subject 
to the Terms of Service agreement with Axway, Inc. 

### Contributing
Code contributions are greatly appreciated, please submit a new [Pull Request](https://github.com/appcelerator-modules/hook-embedded-frameworks/pull/new/master)!
