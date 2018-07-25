---
title: "Build steps"
date: 2018-07-17T10:21:28+03:00
weight: 20
---

### Build steps block

```kotlin
steps {
}
```

### Invoke Ant build using file

```kotlin
ant {
    mode = antFile {
        path = "resources/ant/build.xml"
    }
    targets = "build"
    jvmArgs = "-Xmx512m"
}
```

### Invoke Ant build using inline script
```kotlin
ant {
    mode = antScript {
        content = """
            <?xml version="1.0" encoding="UTF-8"?>
            <project name="echoMessage">
            <target name="sayHello">
              <echo message="Hello, world!"/>
            </target>
            </project>
        """.trimIndent()
    }
    targets = "sayHello"
}
```

### Invoke Ant build using file in Docker container

```kotlin
ant {
    mode = antFile {
        // takes build.xml in the root of the checkout directory by default        
    }
    targets = "sayHello"
    dockerImage = "someImageName:someVersion"
}
```

### Invoke Gradle build

```kotlin
gradle {
    name = "Gradle Step"
    tasks = "clean build"
}
```

### Maven build
```kotlin
maven {
    goals = "clean package install"
    mavenVersion = defaultProvidedVersion()
    jvmArgs = "-Xmx512m"
}
```

### CLI
```kotlin
script {
    scriptContent = "echo %build.number%"
}
```

### Docker Command
```kotlin
dockerCommand {
    commandType = build {
        source = path {
            path = "Dockerfile"
        }
        namesAndTags = "antonarhipov/blah:%build.number%"
        commandArgs = "--pull"
    }
}
```

### Generic step
```kotlin
step {
    name = "FtpUpload"
    type = "ftp-deploy-runner"
    param("jetbrains.buildServer.deployer.ftp.authMethod", "ANONYMOUS")
    param("jetbrains.buildServer.deployer.ftp.transferMethod", "AUTO")
    param("jetbrains.buildServer.deployer.sourcePath", "dir/**/*.zip")
    param("jetbrains.buildServer.deployer.targetUrl", "ftp.target.net")
    param("jetbrains.buildServer.deployer.ftp.securityMode", "0")
}
```

### Helm install
```kotlin
helmInstall {
    chart = "."
    param("teamcity.helm.command", "helm-install")
}
```