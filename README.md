# Black Duck CoPilot Gradle/Travis CI Example

[![Travis CI](https://travis-ci.org/BlackDuckCoPilot/example-gradle-travis.svg?branch=master)](https://travis-ci.org/BlackDuckCoPilot/example-gradle-travis) [![Black Duck Security Risk](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-gradle-travis/public/results/branches/master/badge-risk.svg)](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-gradle-travis/public/results/branches/master)

Shows a working setup for using the Black Duck CoPilot integration to analyze the risk of project dependencies

## Gradle Setup

The `build.gradle` file has been modified to use the [hub-gradle-plugin](https://github.com/blackducksoftware/hub-gradle-plugin) to generate the data used by CoPilot for analysis:

```groovy
buildscript{
	repositories {
		mavenCentral()
		maven { url 'http://jcenter.bintray.com' }
	}
	dependencies {
		classpath group: 'com.blackducksoftware.integration', name: 'hub-gradle-plugin', version: '3.4.1'
	}
}

apply plugin: 'com.blackducksoftware.hub'
```

## Travis CI Setup

The `.travis.yml` file has been modified to upload the generated data to Black Duck CoPilot:

```yaml
after_success:
- ./gradlew createHubOutput
- bash <(curl -s https://copilot.blackducksoftware.com/bash/travis) ./build/blackduck/*_bdio.jsonld
```
