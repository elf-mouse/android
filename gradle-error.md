Q:

```
Error:Execution failed for task ':app:transformClassesWithDexForDebug'.
com.android.build.transform.api.TransformException: com.android.ide.common.process.ProcessException: org.gradle.process.internal.ExecException: Process 'command '/Library/Java/JavaVirtualMachines/jdk1.8.0_XX.jdk/Contents/Home/bin/java'' finished with non-zero exit value 2
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
