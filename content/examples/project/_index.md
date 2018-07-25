---
title: "Project Settings"
date: 2018-07-11T10:21:28+03:00
weight: 10
---

The top-level `project` element in `settings.kts` file represents a top level context for all the build configurations and subprojects that are declared within the scope. 
 ____
```kotlin
project {
    
}
```
The top level does not need to have an id and a name.

A project in TeamCity may include sub-projects and build configurations. A sub-project should be registered in the main context by using `subProject` function:

```kotlin
project {

   //as a block
   subProject {
   }
   
   //as an object
   subProject(MyProject)
}

```


