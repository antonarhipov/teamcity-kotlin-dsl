---
title: "Triggers"
date: 2018-07-17T10:21:28+03:00
weight: 30
---

### Declaring the triggers block
```kotlin
triggers {
}
```

### VCS trigger
```kotlin
vcs {
}
```

### Scheduled build trigger
```kotlin
schedule {
    branchFilter = ""
    triggerBuild = onWatchedBuildChange {
        buildType = "${Build.id}"
        watchedBuildRule = ScheduleTrigger.WatchedBuildRule.LAST_FINISHED
    }
    withPendingChangesOnly = false
    param("dayOfWeek", "Sunday")
}
```

### Finished build trigger
```kotlin
finishBuildTrigger {
    buildTypeExtId = "App10_BuildApp"
    successfulOnly = true
}
```

### Remote run on branch
```kotlin
trigger {
    type = "remoteRunOnBranch"
    param("branchy:jetbrains.git", "pattern:jetbrains.git")
}
```

### Retry build trigger
```kotlin
retryBuild {
    delaySeconds = 10
}
```