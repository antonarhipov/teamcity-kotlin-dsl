+++
title = "Advanced Topics"
description = ""
weight = 20
+++

## Non-Portable DSL

Versions before 2018.1 used a different format for Kotlin DSL settings. This format can still be enabled by turning off the **Generate portable DSL scripts** checkbox on versioned settings page.

When TeamCity generates non-portable DSL, the project structure in the .teamcity directory looks as follows:

* *pom.xml*
* *&lt;project id&gt;/settings.kts*
* *&lt;project id&gt;/Project.kt*
* *&lt;project id&gt;/buildTypes/<build conf id>.kt*
* *&lt;project id&gt;/vcsRoots/<vcs root id>.kt*

where *&lt;project id&gt;* is the ID of the project where versioned settings are enabled. The Kotlin DSL files producing build configurations and VCS roots are placed under the corresponding subdirectories.

### settings.kts

In the non-portable format each project has the following *settings.kts* file:

```kotlin
package MyProject
import jetbrains.buildServer.configs.kotlin.v2018_1.*
/* ... */
version = "2018.1"
 
project(MyProjectId.Project)
```
This is the entry point for project settings generation. Basically, it represents a `Project` instance which generates project settings.

### Project.kt

The `Project.kt` file looks as follows:

```kotlin
package MyPackage
import jetbrains.buildServer.configs.kotlin.v2018_1.*
import jetbrains.buildServer.configs.kotlin.v2018_1.Project
 
object Project : Project({
   uuid = "05acd964-b90f-4493-aa09-c2229f8c76c0"
   id("MyProjectId")
   parentId("MyParent")
   name = "My project"
   ...
})
``` 

where:

* *id* is the absolute id of the project, the same id we'll see in browser address bar if we navigate to this project
* *parentId* is the absolute id of a parent project where this project is attached
* *uuid* is some unique sequence of characters.
* The *uuid* is a unique identifier which associates a project, build configuration or VCS root with its data. If the *uuid* is changed, then the data is lost. The only way to restore the data is to revert the *uuid* to the original value. On the other hand, the id of an entity can be changed freely, if the *uuid* remains the same. This is the main difference of the non-portable DSL format from portable. The portable format does not require specifying the *uuid*, but if it happened so that a build configuration lost its history, one has to reattach it again via the web interface. 

**Note:** If the build history is important, it should be restored as soon as possible: after the deletion, there is a [configurable](http://) timeout (5 days by default) before the builds of the deleted configuration are removed during the build history clean-up.

In case of non-portable DSL, patches are stored under the project patches directory of *.teamcity*:

* *pom.xml*
* *&lt;project id&gt;/settings.kts*
* *&lt;project id&gt;/Project.kt*
* *&lt;project id&gt;/patches/<uuid>.kt*

Working with patches is the same as in portable DSL: you need to move the actual settings from the patch to your script and remove the patch.

## Debugging Maven ‘generate’ Task

The pom.xml file provided for a Kotlin project has the generate task, which can be used to generate TeamCity XML files locally from the Kotlin DSL files. This task supports debugging. If you’re using IntelliJ IDEA, you can easily start debugging of a Maven task:

1. Navigate to **View | Tool Windows | Maven Projects**. The **Maven Projects** tool window is displayed.
2. Locate the task node: Plugins | teamcity-configs | teamcity-configs:generate, the **Debug** option is available in the context menu for the task:

TODO: image

## Ability to Use External Libraries 

You can use external libraries in your Kotlin DSL code, which allows sharing code between different Kotlin DSL-based projects.

To use an external library in your Kotlin DSL code, add a dependency on this library to the _.teamcity/pom.xml_ file in the settings repository and commit this change so that TeamCity detects it. Then, before starting the generation process, the TeamCity server will fetch the necessary dependencies from the Maven repository, compile code with them, and then start the settings generator.