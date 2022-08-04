# Getting Started with Conclave Cloud

Welcome to Conclave Cloud - the serverless platform that preserves privacy.

This site will provide you with all the information you need to get started in
understanding what Conclave Cloud is and what it can do. It will also give you
information on how to create your first Conclave Function, through to developing
a simple password manager as an example.

## Sign-up for access to Conclave Cloud

The first thing to do if you haven't already is to sign-up and create yourself
an account on Conclave Cloud. You can sign up at the [Conclave Cloud portal landing page](https://www.conclave.cloud/).

Click on `CREATE BETA ACCOUNT` then enter your details to register.

![](assets/start_for_free.png)

Once you have signed up, you can login to the Conclave Cloud portal.

## What next?

From here you need to create yourself a project and then upload one or more
functions to play with.

Use the resources below to guide you through using the platform.

## Resources

The following pages will tell you more about Conclave Cloud as well as giving
examples on how to write and invoke functions.

| Page                                                                    | Description                                                                                                                         |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| [What is Conclave Cloud?](what-is-conclave-cloud.md)                    | An overview of the Conclave Cloud platform, what it is and what it can do.                                                          |
| [Conclave Cloud Concepts](conclave-cloud-concepts.md)                   | What is a project? What is a function? Your questions answered here.                                                                |
| [Creating your first function](creating-your-first-function.md)         | Dive into writing your first JavaScript function, uploading it to the platform and invoking it.                                     |
| [JavaScript in Conclave Functions](javascript-in-conclave-functions.md) | Writing JavaScript for Conclave Functions is not quite the same as for other platforms such as node. Find more out about it here.   |
| [The ConclavePass Sample](conclavepass-sample.md)                       | See a more in-depth example which shows how to use TypeScript in Conclave Functions as well as use the Java and JavaScript clients. |

You can interact with Conclave Cloud using the Conclave Cloud Command Line
Interface (`ccl`) as well as client SDKs for Java/Kotlin and JavaScript. The
latest version of these tools and SDKs can be obtained using the information in
the table below:

| Tool/SDK                                                                                                                                                       | Description                                                                                                                                           | Copyright Notice                                                                                                            | License                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Command Line tool for Linux or macOS](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/ccl)                                      | The `ccl` tool can be used from the terminal to manage your Conclave Cloud projects and services.                                                     | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/CLI.NOTICE.txt)                   | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/License.txt) |
| [Command Line tool for Windows](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/ccl.zip)                                         | The `ccl` tool can be used from the terminal to manage your Conclave Cloud projects and services.                                                     | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/CLI.NOTICE.txt)                   | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/License.txt) |
| [Conclave Cloud JavaScript Client SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/conclave-cloud-sdk-1.0.0-beta1.tgz)       | The JavaScript Client SDK that allows you to interact with Conclave Cloud and invoke Conclave Functions from your TypeScript/JavaScript applications. | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/JavaScript.Client.SDK.Notice.txt) | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/License.txt) |
| [Conclave Cloud Java/Kotlin Client SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/conclave-cloud-sdk-java-1.0.0-beta1.zip) | The Java/Kotlin Client SDK that allows you to interact with Conclave Cloud and invoke Conclave Functions from your Java or Kotlin applications.       | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/Java.Client.SDK.Notice.txt)       | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta1/License.txt) |

For information about the current release and about previous releases, please
visit the [releases page](releases.md).

## Installing the `ccl` tool

Whichever operating system you are using you will need to ensure you have a Java
11 or greater runtime environment installed in order to be able to run the `ccl` tool.

_Linux:_

1. Download the tool using the link above.
2. Copy the tool into a directory that is on your path (such as `~/bin`) _or_
   add the directory containing the tool to your `PATH` environment variable.
3. Test it by executing `ccl`.

_macOS:_

1. Download the tool using the link above.
2. Copy the tool into a directory that is on your path _or_
   add the directory containing the tool to your `PATH` environment variable.
3. Test it by executing `ccl`.

_Windows:_

1. Download the tool zipfile using the link above.
2. Unzip the contents to the folder of your choice.
3. Open the start menu and type "env" then choose "Edit the system environment
   variables".
4. Click the "Environment Variables" button.
5. Find the "Path" entry, edit it and add the folder containing the tool to the
   path value.
6. Restart your command prompt to ensure the path has been updated.

Note that for Windows, whenever you are asked to type `ccl` you need to replace
it with `ccl.bat`.

## Installing the Conclave Cloud JavaScript Client SDK

For the beta version of Conclave Cloud, the JavaScript Client SDK is delivered
in a zip file that contains an npm compatible component that can be imported
into your JavaScript/TypeScript application by setting it as a dependency in
your project.

Download and unzip the SDK to the directory of your choice. To add it as a
dependency, add the following to your `package.json`, making sure to provide the
correct path to where you unzipped the SDK.

```json
"dependencies": {
    ...
    "conclave-cloud-sdk": "file:path/to/conclave-cloud-sdk-1.0.0-beta1.tgz",
    ...
}
```

## Installing the Conclave Cloud Java/Kotlin Client SDK

For the beta version of Conclave Cloud, the Java/Kotlin Client SDK is delivered
in a zip file that contains a file-based maven repository. This can be added as
a dependency in your Java/Kotlin project by adding the repository then
describing the dependency.

Download and unzip the SDK to the directory of your choice. Add the repository
to your `build.gradle.kts`, making sure to provide the correct path to where you
unzipped the SDK.

```kotlin
repositories {
	maven(url = "path/to/conclave-cloud-sdk/repo")
	mavenCentral()
}
```

Then add the SDK as a dependency:

```kotlin
	// Conclave Cloud
	implementation("com.r3.conclave.cloud:conclave-cloud-sdk:1.0-RC1")
```
