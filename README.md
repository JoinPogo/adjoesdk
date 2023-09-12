# Unity Wrapper SDK

[TOC]


## Overview

This project serves as a wrapper to allow Android apps built in React Native to utilize the functionality provided by the [adjoe SDK](https://gitlab.adjoe.zone/adjoe/android-mobile/android-sdk).

## Documentation

The public documentation for this wrapper can be found [here](https://docs.adjoe.io/adjoe-sdk/react-native/setting-up-the-sdk).

## Build Manually 
- First install node
- Call `npm install` in the root page of the directory
- Run the `build.sh` script
- In your main repository you should know have two updated *.tgz files

### Upload Manually (Unnecessary)
Since you can do this with the pipeline this is unnecessary. But needs to be mentioned.
- The artifacts should be uploaded and made publicly visible in the appropriate folder in S3. For pre-releases (mostly for justDice), this should be in the bucket [prod-prod-adjoe-sdk-release-private/files/playtime/react-native/](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release-private/files/playtime/react-native) and for standard releases this should be in [prod-prod-adjoe-sdk-release/files/playtime/react-native/](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release/files/playtime/react-native)

## Run the App
You can get an apk from the build in each pipeline. Simply open the Artifacts.</br>
Or do it Manually:
- After Build
- You will need to add the created files to the example.
- Switch to examples directory and
- Run the install-adjoe.sh <version> <build-variant = (standard | drm ) >
- Now in android-studio open the `examples/android` directory as a project
- And run the app

Build and run examples: 
- Normal install ~$ `(npm install && ./build.sh &&  cp *.tgz example/ && cd example/ && ./install-adjoe.sh 2.1.0 standard)`
- Hard reset and build ~ $ `( npm cache clean --force && npm install && ./build.sh &&  cp *.tgz example/ && cd example/ && ./install-adjoe.sh 2.1.0 standard )`

## Deployment with Pipeline

To deploy the project follow these steps 

- Update the wrapper version in Gitlab by running a new pipeline and setting variable `SET_SDK_VERSION`. The version number could look like 4.1.3.2. The semantic version would be major.minor.patch.pre-release In such a situation 4 is the major version, 1 is the minor version, 3 is the patch and 2 would be the pre-release number.
- Upload to the environment you desire, e.g. `upload:justdice` for pre-release versions, or `upload:public` and `upload:justdice` for prod releases.
- Next do the `publish` stage for the uploaded environment to set the uploaded zip to be publicly available on S3. 
- The artifacts should be publicly visible in the appropriate folder in S3. For pre-releases (mostly for justDice), this should be in the bucket [prod-prod-adjoe-sdk-release-private/files/playtime/react-native/](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release-private/files/playtime/react-native) and for standard releases this should be in [prod-prod-adjoe-sdk-release/files/playtime/react-native/](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release/files/playtime/react-native)

## External Links to Share
S3 path of the file is from now on always: `files/playtime/react-native/${VERSION_CODE}`
File name is:
- `react-native-adjoe-sdk-${VERSION_CODE}-standard.tgz`
- `react-native-adjoe-sdk-${VERSION_CODE}-drm.tgz`

pre-release Link is a combination of the followings:
- `https://d2rv4xu1hi9oif.cloudfront.net` + [s3 path of the file](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release-private/files/playtime/react-native) + file name
- Example: https://d2rv4xu1hi9oif.cloudfront.net/files/playtime/react-native/2.1.0.9/react-native-adjoe-sdk-2.1.0.9-standard.tgz

Normal release Link is a combination of the followings:
- `https://releases.adjoe.io` + [s3 path of the file](https://s3.console.aws.amazon.com/s3/buckets/prod-prod-adjoe-sdk-release/files/playtime/react-native) + file name
- Example: https://releases.adjoe.io/files/playtime/react-native/2.1.0/react-native-adjoe-sdk-2.1.0-standard.tgz
