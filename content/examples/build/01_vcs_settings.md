---
title: "VCS settings"
date: 2018-07-17T10:21:28+03:00
weight: 10
---

## VCS root is the same as settings root

```kotlin
vcs {
    root(DslContext.settingsRoot)
}
```

## An arbitrary VCS root

```kotlin
vcs {
    root(MyVcsRoot)
}

//...

object MyVcsRoot({
    //...
})

```

## Checkout rules
```kotlin
vcs {
    root(MyVcsRoot, "+:directory1 => dir1", "+:directory2 => dir2")
}
```

## Additional VCS settings

```kotlin
vcs {
    root(MyVcsRoot1)
    root(MyVcsRoot2)
    root(MyVcsRoot3)
                   
    checkoutMode = CheckoutMode.ON_AGENT
    cleanCheckout = true
    checkoutDir = "."
    showDependenciesChanges = true
}
```

