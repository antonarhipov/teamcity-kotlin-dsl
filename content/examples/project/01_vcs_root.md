---
title: "VCS Roots"
date: 2018-07-17T10:21:28+03:00
weight: 10
---

Documentation: [Configuring VCS Roots](https://confluence.jetbrains.com/display/TCDL/Configuring+VCS+Roots)

## Register a VCS Root
```kotlin
project {
    vcsRoot(MyGitRoot)
    //...
}
```

##  Git

```kotlin
object MyGitRoot : GitVcsRoot({
    id("MyVcs")
    name = "MyVcs"
    
    url = "https://github.com/antonarhipov/app.git"
    
    branch = "master"
    
    branchSpec = """
        +:refs/heads/feature-*
        +:refs/heads/hotfix-*
    """.trimIndent()
    
    userNameStyle = GitVcsRoot.UserNameStyle.NAME
    
    checkoutSubmodules = CheckoutSubmodules.IGNORE
    
    serverSideAutoCRLF = true
    
    agentCleanPolicy = AgentCleanPolicy.ALWAYS
    
    agentCleanFilesPolicy = AgentCleanFilesPolicy.ALL_UNTRACKED
    
    useTagsAsBranches = true
    
    authMethod = password {
        userName = "username"
        password = "password"
    }
})
```

## Mercurial

```kotlin
object MyHgRoot : HgVcsRoot({
    id("MyVcs")
    name = "MyVcs"
    
    url = "https://bitbucket.org/antonarhipov/mercurial"
    
    branchSpec = "+:feature-*"
    
    useTagsAsBranches = true
    
    detectSubrepoChanges = true
    
    // Leave userName and password blank to use settings from 
    // the server hgrc (see 'man hgrc' for details)
    userName = ""
    password = ""
    
    purgePolicy = HgVcsRoot.PurgePolicy.PURGE_UNKNOWN
})
```

## Subversion

```kotlin
object MySvnRoot : SvnVcsRoot({

})
```

## Perforce

```kotlin
object MyPerforceRoot : PerforceVcsRoot({

})
```

## TFS

```kotlin
object MyTfsRoot : TfsVcsRoot({

})
```