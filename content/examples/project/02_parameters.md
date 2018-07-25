---
title: "Parameters"
date: 2018-07-17T10:21:28+03:00
weight: 20
---

Documentation: [Project and Agent Level Build Parameters](https://confluence.jetbrains.com/display/TCDL/Project+and+Agent+Level+Build+Parameters)

```kotlin
project {

    //...

    params {
        checkbox(name = "Release",
                value = "",
                label = "Release?",
                description = "Enable if you want to release",
                display = ParameterDisplay.PROMPT,
                readOnly = false,
                checked = "release")
    }
    
    
    text("requirement.jdk18", "%env.JDK_18%", display = ParameterDisplay.HIDDEN)

    param("gradleParameters", "--info --full-stacktrace")

    param("env.REPOSITORY_URL", "http://some.url")

    select(name = "system.deploy-repo",
            value = "bintray",
            display = ParameterDisplay.PROMPT,
            options = listOf("sonatype-nexus-snapshots-repo" to "sonatype-nexus-snapshots",
                    "bintray-repo" to "bintray"))
    
}
```