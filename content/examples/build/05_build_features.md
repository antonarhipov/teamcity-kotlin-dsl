---
title: "Build features"
date: 2018-07-17T10:21:28+03:00
weight: 50
---

### Declaring build features block

```kotlin
features {
}
```

### Docker support  
```kotlin
dockerSupport {
    cleanupPushedImages = true
    loginToRegistry = on {
        dockerRegistryId = "PROJECT_EXT_19"
    }
}
```

### Merge branches
```kotlin
merge {
    branchFilter = "+:feature*"
}
```

### Files cleanup using Swabra plugin 
```kotlin
swabra {
    filesCleanup = Swabra.FilesCleanup.AFTER_BUILD
    forceCleanCheckout = true
    lockingProcesses = Swabra.LockingProcessPolicy.REPORT
    verbose = true
}
```

### Replacing content within files
```kotlin
replaceContent {
    fileRules = "+:version.txt"
    pattern = "placeholder"
    replacement = "%build.number%"
}
```

### Generic build feature declaration
```kotlin
feature {
    type = "perfmon"
}
```

