Q:

```
Execution failed for task ':app:transformClassesWithDexForDebug'.
> com.android.build.api.transform.TransformException: com.android.ide.common.process.ProcessException: org.gradle.process.internal.ExecException: Process 'command '/Library/Java/JavaVirtualMachines/jdkX.Y.Z.jdk/Contents/Home/bin/java'' finished with non-zero exit value 2
```

A:

```
android {
   ...
   defaultConfig {
      ...
      // Enabling multidex support.
      multiDexEnabled true
   }
}
```

---

Q:

```
Execution failed for task ':app:transformClassesWithJarMergingForDebug'.
> com.android.build.api.transform.TransformException: java.util.zip.ZipException: duplicate entry: com/tencent/mm/a/a.class
```

A: `Project Structure` - `Modules` - `Dependencies`
