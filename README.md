Gradle Circle Style
===================

A plugin for Gradle that summarizes failed Gradle builds in [CircleCI], with special handling for [Checkstyle] and [FindBugs] failures.

[Checkstyle]: https://docs.gradle.org/current/userguide/checkstyle_plugin.html
[CircleCI]: https://circleci.com/
[FindBugs]: https://docs.gradle.org/current/userguide/findbugs_plugin.html

[![Gradle plugins page](https://img.shields.io/github/release/palantir/gradle-circle-style.svg?maxAge=60)](https://plugins.gradle.org/plugin/com.palantir.circle.style)
[![CircleCI](https://img.shields.io/circleci/project/github/palantir/gradle-circle-style/master.svg?maxAge=60)](https://circleci.com/gh/palantir/gradle-circle-style/tree/master)
[![Apache 2.0 License](https://img.shields.io/github/license/palantir/gradle-circle-style.svg?maxAge=2592000)](http://www.apache.org/licenses/LICENSE-2.0)

Quickstart
----------

Add the following to your project's top-level build.gradle file:

```gradle

plugins {
  id 'com.palantir.circle.style' version '1.1.2'
}
```

And now your CircleCI builds will fail with nice summaries:

![CHECKSTYLE — 1 FAILURE](images/checkstyle-circle-failure.png?raw=true "CircleCI failure image")

Details
-------

This plugin is enabled by the `CIRCLE_TEST_REPORTS` environment variable, set automatically on CircleCI builds. It then automatically enables XML output for Checkstyle and FindBugs plugins, and adds a finalizer task that collates their results (and any other Gradle build step failures) using the JUnit XML output that CircleCI expects.

Additionally, all JUnit output is placed in the `CIRCLE_TEST_REPORTS` directory.

Note that FindBugs does not support generating both HTML and XML output, so HTML output will be disabled on CircleCI builds. (Checkstyle does not have this limitation.)
