---
title: "Failure conditions"
date: 2018-07-17T10:21:28+03:00
weight: 40
---

### Declaring failure conditions

```kotlin
failureConditions {
}
```

### Fail if execution takes too long

```kotlin
failureConditions {
    executionTimeoutMin = 240
}
```

### Fail if the build log contains a string

```kotlin
failOnText {
    conditionType = BuildFailureOnText.ConditionType.CONTAINS
    pattern = "error in build"
    failureMessage = "Build failed"
    reverse = false
    stopBuildOnFailure = true
}
```

### Fail on artifact size change
```kotlin
failOnMetricChange {
    metric = BuildFailureOnMetric.MetricType.ARTIFACT_SIZE
    threshold = 100
    units = BuildFailureOnMetric.MetricUnit.DEFAULT_UNIT
    comparison = BuildFailureOnMetric.MetricComparison.LESS
    compareTo = value()
    param("anchorBuild", "lastSuccessful")
}
```

### Fail on build duration change
```kotlin
failOnMetricChange {
    metric = BuildFailureOnMetric.MetricType.BUILD_DURATION
    threshold = 200
    units = BuildFailureOnMetric.MetricUnit.PERCENTS
    comparison = BuildFailureOnMetric.MetricComparison.MORE
    compareTo = build {
        buildRule = lastSuccessful()
    }
}
```

### Fail on test duration change
```kotlin
failOnMetricChange {
    metric = BuildFailureOnMetric.MetricType.TEST_DURATION
    threshold = 200
    units = BuildFailureOnMetric.MetricUnit.PERCENTS
    comparison = BuildFailureOnMetric.MetricComparison.MORE
    compareTo = build {
        buildRule = lastSuccessful()
    }
    stopBuildOnFailure = true
}
```

