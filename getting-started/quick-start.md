---
description: Getting started with the SSI Kit.
---

# Quick Start

There are different ways to get started in using the SSI Kit.

* Docker: Quick way to launch and try out the latest builds. No build environment required.
* Local Build: Build and run the SSI Kit locally. Requires a JDK 16 build environment including, Gradle.
* Dependency (JVM): The SSI Kit can be used directly as JVM-dependency **** via Maven or Gradle.&#x20;

**CLI Tool**: The SSI Kit comes with a **** command-line interface (CLI) tool, which offers a rich set of commands to run the entire functionality the SSI Kit provides. The CLI tool can be used by running the Docker container or the executable by the local build.

**REST API**: In case you want to run the SSI Kit as a service, your application can access all functionalities via the REST API.

## Run

The simplest way of using the _SSI Kit_ library is by pulling the Docker Container and running it via **Docker**:

```
docker run -itv $(pwd)/data:/app/data waltid/ssikit -h
```

Use the wrapper script **ssikit.sh** on Linux (requires Gradle 7 and Java 16) for building the source and running the CLI tool:

```
git clone https://github.com/walt-id/waltid-ssikit.git
cd waltid-ssikit/
./ssikit.sh -h
```

For a quick intro using the command line interface, refer to the [CLI - Command Line Interface](cli-command-line-interface.md).

## Build

You need:

* JDK 16 (or above),
* Git.

The easiest way to build the SSI Kit on Linux is by using the wrapper script **`ssikit.sh`**

First, clone the Git repo and switch into the project folder:

```
git clone https://github.com/walt-id/waltid-ssikit.git
cd waltid-ssikit/
```

Then, run the build command using the wrapper script:

```
./ssikit.sh build
```

For more detailed information about the build process and build options, refer to [Build](build.md).
