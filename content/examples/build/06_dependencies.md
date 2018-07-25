---
title: "Dependencies"
date: 2018-07-17T10:21:28+03:00
weight: 60
---

### Dependencies block

```kotlin
dependencies {
}
```

### Snapshot dependencies

```kotlin
dependency(Build){
    snapshot {}
}
```

```kotlin
snapshot(Build){
}
```

### Artifact dependencies

```kotlin
dependency(Build){
    artifact {
        artifactRules = "*.jar"
    }
}
```

```kotlin
artifact(Build) {
    artifactRules = "*.jar"
}
```

### Declaring snapshot and artifact dependencies 

```kotlin
dependency(Build){
    snapshot {
    }
    artifact {
        artifactRules = "*.jar"
    }
}
```