# Oigetit Android

## Continues integration process 

### Release to GP test group
0. Merge to master branch. This will trigger the build process in CircleCI that will:
1. Increment application version code and application version name (required changes for new release).
2. Commit this change to git.
3. Create tag with appropriate release version name.
4. Push changes to git.
5. Start [Fastlane](https://fastlane.tools/) release process to internal test group for GP.

### Release to GP production
0. Release application to GP test group and test the result release
1. Go to [Google Play Publish Console](https://play.google.com/apps/publish/?account=6342769836511779022#ManageReleasesPlace:p=io.scal.oigetit&appid=4972818834053907185)
2. Create new production release, add artefact from the library, set up release note and roll out new release.

## Local application delivery

### Do NOT use master branch for develop process!

0. Any direct commit to master branch will fail.
1. The only way to commit to master branch is to marge changes throught Pull Request.

### Pre build actions
0. Check out develop branch from this repository.
1. Create `key.properties` file in the root directory with this data `storeFile=oigetit_scal.jks`
3. Download android build toolchain. It is better to have Android Studio with build-in Android SDK that can be found [here](https://developer.android.com/studio). Otherwise if you want to use command line tools - setup is up to you.

### Building with AS (recommended)
Open project in Android Studio by specifying the root path of this repo. All other things should be done automatically. Perhaps you will have to download buildtools or other things during this process but usually it is done automatically or with single action promts.
You can find tutorials [here](https://www.pdftron.com/documentation/android/faq/run-in-android-studio/) and base [here](https://developer.android.com/training/basics/firstapp) 

### Building with command line
To build the app with command line use the guide [here](https://developer.android.com/studio/build/building-cmdline)

### Debug vs Release configurations
During the development process you should use `debug` build configuration.
You may see this error during the build process: 
```
Some problems were found with the configuration of task ':app:signingConfigWriterScalRelease'.
> No value has been specified for property 'signingConfig.keyAlias'.
> No value has been specified for property 'signingConfig.keyPassword'.
> No value has been specified for property 'signingConfig.storePassword'.
```
This happends because we do NOT push release build configuration to git for security reasons. To solve this issue change build configuration to `scalDebug` - this way you will build debug version that is fine for development process and should be enouth. See [this](https://developer.android.com/studio/run#changing-variant) link for additional information.

If you still need to build the app in release mode - ask for credentials (Mikhail Gurevich has them).
