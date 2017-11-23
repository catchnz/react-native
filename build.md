# To Build
* I was using java 8
* Checkout project
* Download `http://dl.google.com/android/repository/android-ndk-r10e-darwin-x86_64.zip`
* Extract and point local.properties ndk.dir to ndk folder
* Set `export ANDROID_NDK=_NDK_DIRECTORY_` in terminal or in `~/.bash_profile`
* Change line 171-173 of ReactAndroid/build.gradle, `def ndkDir = "/Users/[user_name]/Library/Android/sdk/ndk-bundle/"` to point at your ndk dir instead.
* Locally host `boost_1_57_0.zip` which can be found at `https://drive.google.com/file/d/1K2uWsNaGjYYaUU5iSpdcKfMoTQna0yAw/view?usp=sharing`, then insert URL to hosted file at ReactAndroid/build.gradle line 31
* Run `scripts/build-android-rn.js` 


----
# What this is missing
## Javadocs
Line 107 - 114 of `scripts/build-android-rn.js` is commented out to stop javadocss from being generated.
Could not get docs compiling using java greater than version 7.
I could not find a version of java7 for mac. 
The react native build scripts says they do not work with anything but version 7.

## Sources JAR
Line 102 of `ReactAndroid/release.gradle.js` was commented out. Not sure if this affects anything. I think this was a fix for building from android studio. When running the script `scripts/build-android-rn.js` dont think this line is encounted.


----
# What was changed

### scripts/build-android-rn.js
 `scripts/build-android-rn.js` is a completely new file that was taken from `scripts/publish-npm.js`

* hardcoded buildbranch line 52
* hardcoded commit message and tag version message line 66 and 71
* commented out lines 99 - 114 to stop compile error for java versions greater than. because javadocs.
* commented out lines 136 - 144 to stop npm trying to publish the package

### ReactAndroid/build.gradle.js

* line 31 needs a url to a locally a hosted `boost_0_57_1.zip` which can be found at https://drive.google.com/file/d/1K2uWsNaGjYYaUU5iSpdcKfMoTQna0yAw/view?usp=sharing
* lines 126 - 136 added tasks to generate jars from ReactAndroid may not be needed
* Change line 171-173 of `ReactAndroid/build.gradle :` `def ndkDir = "/Users/[user_name]/Library/Android/sdk/ndk-bundle/"` to point at your ndk dir


### ReactAndroid/release.gradle.js

* line 30 - 40 is a modified version of lines 14 - 24 `property('repositoryUrl')` was returning null
* commented out line 102