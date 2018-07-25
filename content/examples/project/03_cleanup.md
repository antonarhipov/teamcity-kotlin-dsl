---
title: "Clean-up Rules"
date: 2018-07-17T10:21:28+03:00
weight: 30
---

Documentation: [Project Clean-up Rules](https://confluence.jetbrains.com/display/TCD18/Clean-Up#Clean-Up-ProjectClean-upRules)

```kotlin
project {

    //...
  
    cleanup {
        artifacts(builds = 10, 
                    days = 7, 
                    artifactPatterns = "+:**/*")
                    
        history(builds = 10)             
    }
}




```