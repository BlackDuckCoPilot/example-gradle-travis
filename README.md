# Black Duck CoPilot Gradle/Travis CI Example

[![Travis CI](https://travis-ci.org/BlackDuckCoPilot/example-gradle-travis.svg?branch=master)](https://travis-ci.org/BlackDuckCoPilot/example-gradle-travis) [![Black Duck Security Risk](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-gradle-travis/public/results/branches/master/badge-risk.svg)](https://copilot.blackducksoftware.com/github/groups/BlackDuckCoPilot/locations/example-gradle-travis/public/results/branches/master)

Shows a working setup for using the Black Duck CoPilot integration to analyze the risk of project dependencies

## Travis CI Setup

The `.travis.yml` file has been modified to upload generated dependency data to Black Duck CoPilot:

```yaml
after_success:
- curl https://copilot.blackducksoftware.com/scripts/init/gradle -o bds_init.gradle
- ./gradlew --init-script bds_init.gradle buildBom -DbdsPluginVersion=5.0.0
- bash <(curl -s https://copilot.blackducksoftware.com/bash/travis) ./build/blackduck/*_bdio.jsonld
```
