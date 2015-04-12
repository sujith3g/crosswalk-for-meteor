Crosswalk-for-meteor
=====================

A documentation on how to build android app from meteor using `crosswalk-11.40.277.1-arm`. This steps I found from [here](http://pt.stackoverflow.com/questions/53282/plugin-de-splashcreen-cordova-e-%C3%ADcones-n%C3%A3o-funcionam-no-crosswalk). In which we will be replacing the `src/org/apache/cordova/CordovaWebView.java` file. 
Steps for building apk
----------------------

1. ` cd  meteor_app`
2. ` meteor build .build --server host:port` replace host and port
3. ` mkdir .build-tools && cd .build-tools`
4. ` wget https://s3.amazonaws.com/meteor-mobile/crosswalk-11.40.277.1.zip`
5. ` unzip crosswalk-11.40.277.1.zip`
6. ` cd ..`  move to meteor_app/ directory
7. ` rm -Rf .meteor/local/cordova-build/platforms/android/CordovaLib/*`
8. ` cp -a crosswalk-11.40.277.1/crosswalk-arm/framework/* .meteor/local/cordova-build/platforms/android/CordovaLib/`
9. ` cp -a crosswalk-11.40.277.1/crosswalk-arm/VERSION .meteor/local/cordova-build/platforms/android/`
10. ` cd .meteor/local/cordova-build/platforms/android/CordovaLib/`
11.  replace `CordovaLib/src/org/apache/cordova/CordovaWebView.java` with `CordovaWebView.java` file provided in this repo
12. ` android update project --subprojects --path . --target "android-21"`
13. ` cd ..` move to .meteor/local/cordova-build/platforms/android/
14. ` rm -Rf ant-gen;`
15. ` rm -Rf ant-build;`
16. add wifi permission `<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />` to `.meteor/local/cordova-build/platforms/android/AndroidManifest.xml`  
17. ` cd ../../` move to .meteor/local/cordova-build/
18. `cordova build android` or `cordova build android --release`
19. for signing & zipalign, follow [this](https://github.com/meteor/meteor/wiki/How-to-submit-your-Android-app-to-Play-Store) after release build.

