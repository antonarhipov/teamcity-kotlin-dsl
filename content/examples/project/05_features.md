---
title: "Features"
date: 2018-07-17T10:21:28+03:00
weight: 50
---
```kotlin
project {
    features {
       //...
    }
}
```

## Connection to Docker registry

Documentation: [Docker connection for a Project](https://confluence.jetbrains.com/display/TCDL/Integrating+TeamCity+with+Docker#IntegratingTeamCitywithDocker-DockerConnectionforaProject)

```kotlin
dockerRegistry {
    id = "dockerRegistry"
    name = "Docker Registry"
    url = "https://docker.io"
    userName = "userName"
    password = "password"
}
```

## Connection to GitHub issues

```kotlin
feature {
    id = "GitHubIssues"
    type = "IssueTracker"
    param("secure:password", "")
    param("name", "antonarhipov/app")
    param("pattern", """#(\d+)""")
    param("authType", "accesstoken")
    param("repository", "https://github.com/antonarhipov/app")
    param("type", "GithubIssues")
    param("secure:accessToken", "zxx....")
    param("username", "")
}
```

## Shared Resources

Documentation: [Shared Resources](https://confluence.jetbrains.com/display/TCDL/Shared+Resources)

```kotlin
feature {
    id = "sharedResource1"
    type = "JetBrains.SharedResources"
    param("quota", "100")
    param("name", "file")
    param("type", "quoted")
}
```
