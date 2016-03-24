## build

```
android {
    ...
    signingConfigs {
        myConfig {
            keyAlias 'projectName'
            keyPassword 'myPassword'
            storeFile file('/path/to/myStore.keystore')
            storePassword 'storePassword'
        }
    }
    ...
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.myConfig
        }
    }
}
```

`gradle build` 生成APK到 `build/outputs/apk/` 中
