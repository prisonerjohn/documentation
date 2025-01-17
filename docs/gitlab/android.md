# Android

To make build working with Android, you will need a specific Unity license (because that is not the same docker image). Add the content of your specific Unity license in your CI's environment variable : `UNITY_LICENSE_CONTENT_ANDROID`

By default the apk is not signed and the build will use the Unity's default debug key.
For _security reasons_, **you should not add your keystore to git**.

## Encode your keystore

Encode your keystore file as base64 using openssl:

```bash
openssl base64 -A -in yourKeystore.keystore
```

Copy the result to your CI's environment variable `ANDROID_KEYSTORE_BASE64`

Add following environment variables:

- `KEYSTORE_PASS`: Keystore pass
- `KEY_ALIAS_NAME`: Keystore alias name to use (if not set, the program will use the alias name set in Project's PlayerSettings)
- `KEY_ALIAS_PASS`: Keystore alias pass to use

Note about _keystore security_, if you would like to use another solution for storage, see [Where to Store Android KeyStore File in CI/CD Cycle?](https://android.jlelse.eu/where-to-store-android-keystore-file-in-ci-cd-cycle-2365f4e02e57).

### Android app bundle

`BUILD_APP_BUNDLE` env var is defined in `gitlab-ci.yml`. Set it to `true` to build an `.aab` file. Note: to build an android app bundle, you need an image with **Android NDK**.

See [related issue gableroux/unity3d#61](https://gitlab.com/gableroux/unity3d/issues/61)

### Bundle version code

The bundle version code must be increment for each deployed build.

To simplify the process, the `BUNDLE_VERSION_CODE` env var is used and set as bundle version code.

Currently, for gitlab, `BUNDLE_VERSION_CODE = $CI_PIPELINE_IID`. [Documentation](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)  
If you use another CI solution, set a CI env var incrementing for each pipeline.

### Fastlane supply (deployement)

Follow [setup instructions](https://docs.fastlane.tools/actions/supply/) to get a google play console token, then, add the content to env var `GPC_TOKEN`.

Uncomment the `#deploy-android` job in gitlab-ci.yml and replace `com.youcompany.yourgame` by your package name.

You can change the track `internal` to `alpha`, `beta` or `production`.

That is the simplest way with command line but you can also make `fastlane/Fastfile` and `fastlane/Appfile`, with the following command after building a temporary gradle project (export gradle project option in Unity build settings):

```bash
fastlane init
```

Then run the following command:

```bash
fastlane supply init
```

and update all metadata, images, changelogs, etc... These will be uploaded to the store everytime. Refer to [fastlane supply documentation](https://docs.fastlane.tools/actions/supply/) for more details.
