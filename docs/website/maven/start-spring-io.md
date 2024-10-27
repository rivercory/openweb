---
title: start.spring.io
---

> GitHub: https://github.com/spring-io/start.spring.io <br/>
> Website: https://start.spring.io <br/>
> Language (Framework): Maven

# start.spring.io
<a href="https://gitter.im/spring-io/initializr?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge" target="_blank">
<img src="https://badges.gitter.im/spring-io/initializr.svg"/>
</a>

This repository configures a [Spring Initializr](https://github.com/spring-io/initializr) instance with a custom UI
running at https://start.spring.io. The following modules are available:

* `start-client`: client-side assets
* `start-site`: server infrastructure and metadata configuration
* `start-site-verification`: tests to verify the validity of the metadata

## Using
There is a [dedicated page](USING.adoc) that describes how you can interact with the
service.

## Building from Source

You need Java 17 and a bash-like shell.

### Building

Invoke the build at the root of the project

```
$ ./mvnw clean install
```

The project also includes a number of longer-running verification tests. They
can be built and run using the `verification` profile:

```
$ ./mvnw -Pverification clean install
```

The project’s other tests are not included in the `verification` profile. All of
the project’s tests can be run using the `full` profile:

```
$ ./mvnw -Pfull clean install
```

If building `start-client` fails, you may have an outdated cache that can be deleted as
follows:

```
$ cd start-client
$ rm -rf .cache node_modules
```

### Running the app locally
As long as you’ve built the project beforehand (in particular `start-client`), you can
easily start the app as any other Spring Boot app:

```
$ cd start-site
$ ../mvnw spring-boot:run
```

### Running the app in an IDE
You should be able to import the project into your IDE with no problems. Once there you
can run the `StartApplication` from its main method and debug it. If you also need to
work on the library, adding the `initializr` project in your workspace would make sure
to reload the app whenever you make any change.

This is the recommended way to operate while you are developing the application,
especially the UI.

## Reusing the Web UI
This instance has a thin layer with our opinions about getting started with Spring Boot.
You can reuse them but please keep in mind that this is not supported with the same
level as the Spring Initializr library. The Web UI, in particular, is for our own
purpose and is not particularly engineered to be easily extended.

## Deploying to Cloud Foundry

If you are on a Mac and using [homebrew](https://brew.sh/), install the Cloud Foundry
CLI:

```
$ brew install cloudfoundry-cli
```

Alternatively, download a suitable binary for your platform from
[Pivotal Web Services](https://console.run.pivotal.io/tools).

You should ensure that the application name and URL (name and host values) are
suitable for your environment before running `cf push`.

First, make sure that you have [built the application](#building), then make sure first
that the jar has been created:

```
$ cd start-site
$ ../mvnw package
```

The project creates a regular library jar and a repackaged archive that can be used to
start the application with the `exec` classifier. Once the build as completed, you can
push the application:

```
$ cf push your-start -p target/start-site-exec.jar
```

## License
The start.spring.io website is Open Source software released under the
[Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0.html).
