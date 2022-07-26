# Gradle | Dev | OFBiz | Quickstarts

## OWASP (security)
[org.owasp.dependencycheck](https://jeremylong.github.io/DependencyCheck/dependency-check-gradle/index.html): 
- *The OWASP dependency-check-gradle plugin provides monitoring of the projects dependent libraries; creating a report of known vulnerable components that are included in the build.*
- *It is important to understand that the first time this task is executed it may take 5-20 minutes as it downloads and processes the data from the National Vulnerability Database (NVD) hosted by NIST: https://nvd.nist.gov*
- *After the first batch download, as long as the plugin is executed at least once every seven days the update will only take a few seconds.*

Syntax: 
```bash
gradlew -PenableOwasp dependencyCheckAnalyze
```

## DependencyUpdates plugin
- *gradle will download required dependencies and activate Gradle's DependencyUpdates plugin and its related tasks.*

Syntax: 
```bash
gradlew -PenableDependencyUpdates dependencyUpdates -Drevision=releas
```

Check only:
```bash
gradlew -PenableDependencyUpdates useLatestVersions && gradlew -PenableDependencyUpdates useLatestVersionsCheck
```

Automated update:
```bash
gradlew -PenableDependencyUpdates useLatestVersions
```

## Javadoc
There is a section on [javadoc](https://en.wikipedia.org/wiki/Javadoc).

*TODO: You might need to pass a flag to generate the Javadoc (need to add more doc here)*

## Node
Node (node.js) is included.

It seems to be used for the themes JS.

## Compatibility
- `sourceCompatibility = '1.8'`
- `targetCompatibility = '1.8'`

## Repositories
In the section `allprojects` you have the settings for the repositories.

## Subprojects
In the subprojects section Gradle loads all the plugins.

## `excludedJavaSources`
`excludedJavaSources` is an array with list of Java file paths.

I think they need to be removed from the list if you want them loaded. (unsure)

## `compileGroovyScriptsGroovy`
By default it is set as `false`.

Because groovy elements are to be considered as standalone elements executed in isolation by OFBiz.

## `checkstyle`
[`checkstyle`](https://en.wikipedia.org/wiki/Checkstyle) section is the setting for Checkstyle tool.

This tool is used for static code analysis to make sure the code is compliant with specified coding rules.

It checks for: 
- quality
- readability
- re-usability

By default it is set as: 
- `tasks.checkstyleMain.maxErrors = 0`
- `showViolations = true`

## `gitHooks`
`gitHooks` is a section for git hooks.

By default: 
```groovy
hooks = ['pre-push': 'checkstyleMain']
```

## Eclipse plugin settings
It seems to clean up stuff added by Eclipse.

## Tasks
- loadAll
- testIntegration
- terminateOfbiz
- loadAdminUserLogin - *Create admin user with temporary password equal to ofbiz. You must provide userLoginId*
- loadTenant - *Load data using tenantId*
- createTenant - *Create a new tenant in your environment*
- generateDatabaseTemplateFile
- generateAdminUserTemplateFile
- 
