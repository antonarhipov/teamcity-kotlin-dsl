+++
title = "FAQ and Common Problems"
description = ""
weight = 30
+++

## How to Add .teamcity as a New Module to a Project?

Question: How to add the .teamcity settings directory as a new module to an existing project in IntelliJ IDEA?

Solution: In your existing project in  IntelliJ IDEA:

Go to File | Project Structure, or press Ctrl+Shift+Alt+S.
Select Modules under the Project Settings section.
Click the plus sign, select Import module and choose the folder containing your project settings. Click Ok and follow the wizard.
Click Apply. The new module is added to your project structure.


## New URL of Settings VCS Root (Non portable format)

Problem: I changed the URL of the VCS root where settings are stored in Kotlin and now TeamCity cannot find any settings in the repository at the new location.

Solution:  

Fix the URL in the Kotlin DSL in the version control and push the fix.
Disable versioned settings to enable the UI.
Fix the URL in the VCS root in the UI.
Enable versioned settings with same VCS root and the Kotlin format again, TeamCity will detect that the repository contains the .teamcity directory and ask you if you want to import settings.
Choose to import settings.

## How to Read Files in Kotlin DSL
Problem: I want to generate a TeamCity build configuration based on the data in some file residing in the VCS inside the .teamcity directory

Solution: TeamCity executes DSL with the .teamcity as the current directory, so files can be read using the paths relative to the .teamcity directory e.g. File("data/setup.xml"). Files outside the .teamcity directory are not accessible to Kotlin DSL.

## Passwords-Related Questions

### Prior to TeamCity 2017.1

Problem: I do not want the passwords to be committed to the VCS, even in a scrambled form.

Solution: You can move the passwords to the parent project whose settings are not committed to a VCS.

 

Problem: I want to change passwords after the settings have been generated.

Solution: The passwords will have to be scrambled manually using the following command in the maven project with settings:
 
```
mvn -Dtext=<text to scramble> org.jetbrains.teamcity:teamcity-configs-maven-plugin:scramble
```

### Since TeamCity 2017.1

Solution: Use tokens instead of passwords. Please refer to the related [section](http://).