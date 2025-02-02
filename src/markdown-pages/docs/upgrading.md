---
path: "/docs/upgrading"
title: "Upgrading"
---

## Upgrading using the external update site

You can get the latest version of Galasa in Eclipse by completing the following steps:

1. Launch Eclipse. 
2. Choose *Help > Install New Software* from the main menu.
3. Select `https://p2.galasa.dev/` in the _Work with_ field to check whether a new version of Galasa is available.
4. If a new version is available, tick the *Galasa* box in the main panel, ensuring that *Galasa* and all child elements are ticked.
5. Follow the prompts to download and install the new version of Galasa. Eclipse restarts and the latest version is installed.

## Upgrading using the Galasa zipped distribution

Download and extract the Galasa zip file to a directory of your choice and complete the following steps:

1. Launch Eclipse. 
2. Choose *Help > Install New Software* from the main menu.
3. Click *Add* and then Select *Local*.
4. Navigate to the directory into which the zip was extracted, select the Eclipse directory, and click *OK*.
5. Check that the _Location_ field is populated with the filepath information or URL to the running container, for example, `file:///home/username/galasa-isolated-mvp/eclipse/` or `http://hostname:8080/eclipse` and press *Enter*.
6. Tick the *Galasa* box in the main panel, ensuring that *Galasa* and all child elements are ticked.
7. Follow the prompts to download and install the new version of Galasa. Eclipse restarts and the latest version is installed.



## Upgrading existing tests

If you have a pre-built version of tests that were created against an earlier version of Galasa in your local repository, you need to rebuild those test projects and any associated Managers after ugprading, so that the pom.xml files of those tests and Managers specify the new version of Galasa.


A simple way to do this is to complete the following steps: 

1. Search your Galasa files for the version number against which the tests were created, for example *0.9.0*. A filtered list of files containing *0.9.0* is returned. 
2. Check each pom.xml file and replace that version number with the new version number, for example, *0.10.0*. 

**NOTE:** Do not update version numbers for non-Galasa dependencies or plug-ins. Only replace the version number for Galasa dependencies, where the *groupId* is set to *dev.galasa*, as per the following examples:

```
<parent>
<groupId>dev.galasa</groupId>
<artifactId>galasa-parent</artifactId>
<version>0.10.0</version>
</parent>
```

```
<dependencies>
        <dependency>
            <groupId>dev.galasa</groupId>
            <artifactId>dev.galasa</artifactId>
            <version>0.10.0</version>
            <scope>provided</scope>
        </dependency>
```
3. Check that the OBR version in the Galasa preferences references the new version of Galasa.<br><br>
    If you are using Eclipse, complete the following steps:<br><br>
        a. Go to *Eclipse > Preferences > Galasa* on a Mac or *Window > Preferences > Galasa* on Windows. <br><br>
        b. Check the *OBR Version* field is blank, to automatically select the latest version.<br><br>
    If you are using VS code, complete the following steps: <br><br>
        a. Go to  *File > Preferences > Settings* and expand the *Extensions* section.<br><br> 
        b. Select *Galasa* and check that the *Version* field is using the default value of ```LATEST```, to automatically select the latest version. 

## Troubleshooting

If you have problems after completing the steps for upgrading, try running a clean install. 

To run a clean Maven install in Eclipse, complete the following steps: 

1. Right click your project and select *Run as > Maven clean*
2. Right click your project and select *Run as > Maven install* 

Alternatively, run the ```mvn clean install ``` command from the command line. 

To run a clean Gradle install in Eclipse, complete the following steps: 

1. In Project Explorer, right-click on `dev.galasa.simbank.parent` and select _Gradle > Refresh Gradle Project_. A _BUILD SUCCESSFUL_ message is displayed in the _Console_ tab when the project is refreshed successfully.
1. Navigate to *Run > Run Configurations*. The *Create, manage and run configurations* dialog box appears. 
1. Depending on version of Eclipse that you are using, either right-click *Gradle Project* or *Gradle Task* and choose *New Configuration*. 
1. Provide a meaningful name and set up your Gradle Task to run a clean build. 

Alternatively, run the ```gradle clean build``` command from the command line.

If you are still having issues, you can force a full rebuild by deleting your *.m2* repository and creating a new build against your test projects and Managers by running a clean install.