Crosswalk-for-meteor
=====================

A documentation on how to build android app from meteor using [`crosswalk-11.40.277.1-arm`](https://s3.amazonaws.com/meteor-mobile/crosswalk-11.40.277.1.zip). This steps I found from [here](http://pt.stackoverflow.com/questions/53282/plugin-de-splashcreen-cordova-e-%C3%ADcones-n%C3%A3o-funcionam-no-crosswalk). In which we will be replacing the `src/org/apache/cordova/CordovaWebView.java` file. 

`crosswalk-11.40.277.1.zip` provided in the repo is `CordovaWebView.java` replaced version of [`crosswalk-11.40.277.1-arm`](https://s3.amazonaws.com/meteor-mobile/crosswalk-11.40.277.1.zip), By using `crosswalk-11.40.277.1.zip` provided in the repo You can skip Step 4 to 6.

Steps for building apk
----------------------

1. ` cd  meteor_app`
2. ` meteor build .build --server host:port` replace host and port
3. ` mkdir .build-tools && cd .build-tools`
4. ` wget https://s3.amazonaws.com/meteor-mobile/crosswalk-11.40.277.1.zip`
5. ` unzip crosswalk-11.40.277.1.zip`
6.  replace `crosswalk-11.40.277.1/crosswalk-arm/framework/src/org/apache/cordova/CordovaWebView.java` with `CordovaWebView.java` file provided in this repo
7. ` cd ..`  move to meteor_app/ directory
8. ` rm -Rf .meteor/local/cordova-build/platforms/android/CordovaLib/*`
9. ` cp -a .build-tools/crosswalk-11.40.277.1/crosswalk-arm/framework/* .meteor/local/cordova-build/platforms/android/CordovaLib/`
10. ` cp -a .build-tools/crosswalk-11.40.277.1/crosswalk-arm/VERSION .meteor/local/cordova-build/platforms/android/`
11. ` cd .meteor/local/cordova-build/platforms/android/CordovaLib/`
12. ` android update project --subprojects --path . --target "android-21"`
13. ` ant debug`
14. ` cd ..` move to .meteor/local/cordova-build/platforms/android/
15. ` rm -Rf ant-gen;`
16. ` rm -Rf ant-build;`
17. add wifi permission `<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />` to `.meteor/local/cordova-build/platforms/android/AndroidManifest.xml`  
18. ` cd ../../` move to .meteor/local/cordova-build/
19. `cordova build android` or `cordova build android --release`
20. for signing & zipalign, follow [this](http://developer.android.com/tools/publishing/app-signing.html#signing-manually) after release build.

