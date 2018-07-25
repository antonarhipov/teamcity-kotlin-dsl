---
title: "Build Configuration"
date: 2018-07-11T10:21:28+03:00
weight: 20
---
 
To register a new build configuration one should use the `buildType` function by providing either a block or a type name as a parameter    
 
```kotlin
project {
    buildType {
    }
    
    buildType(Build)
}
```

A build configuration in Kotlin DSL is an instance of BuildType:

```kotlin
project {
    buildType(Build)
}

object Build : BuildType {
    id("Build")
    name = "Build"
    
    steps {
        script {
            scriptContent = "echo 'Hello'"
        }
    }
}
```
