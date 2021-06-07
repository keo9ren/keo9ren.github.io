---
layout: post
title: Ionic Cordova Android App Bundle (AAB)
--- 

How to build the new Android App Bundles (AAB) with Ionic and/or Cordova.

Linux and mac:
```shell 
ionic cordova build android --prod --release -- -- --keystore=bar --storePassword=foo --alias=android --password=2332  --versionCode=123 --versionName=124 --packageType=bundle

cordova build android --release -- --keystore=bar storePassword=foo --alias=android --password=123 --versionCode=162142 --versionName=162142 --packageType=bundle
```

Windows:
```shell
ionic cordova build android --prod --release --alias=cos-android --password=supergeheim  --versionCode=12345 --versionName=12345 -- -- -- --packageType=bundle

cordova build android --prod --release --alias=cos-android --password=supergeheim  --versionCode=12345 --versionName=12345 -- -- --packageType=bundle
```