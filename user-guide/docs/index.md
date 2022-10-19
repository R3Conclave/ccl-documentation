# Getting Started with Conclave Cloud

Welcome to Conclave Cloud - the serverless platform that preserves privacy.

This site provides you with all the information you need to understand what Conclave Cloud is and what it can do. You
can also find information on how to create your first *Conclave function* and develop a simple password manager as 
an example.

## Sign-up for access to Conclave Cloud

If you haven't already, the first thing to do is sign up and create an account on Conclave Cloud. You can sign up at 
the [Conclave Cloud portal landing page](https://www.conclave.cloud/).

Click on `CREATE ACCOUNT` and enter your details to register.

![a screenshot of a banner with a CREATE ACCOUNT button](assets/start_for_free.png)

Once you have signed up, you can log in to the Conclave Cloud portal.

## What next?

You need to create a project and upload one or more functions to your project.

Use the resources below to use the platform.

## Resources

The following pages describe Conclave Cloud and give examples to write and invoke Conclave functions.

| Page                                                                    | Description                                                                                                                       |
| ----------------------------------------------------------------------- |-----------------------------------------------------------------------------------------------------------------------------------|
| [What is Conclave Cloud?](what-is-conclave-cloud.md)                    | An overview of the Conclave Cloud platform and what it can do.                                                                    |
| [Conclave Cloud Concepts](conclave-cloud-concepts.md)                   | Understand projects and functions in Conclave CLoud.                                                                              |
| [Creating your first function](creating-your-first-function.md)         | Write your first JavaScript function, upload it to the platform, and invoke it.                                                   |
| [JavaScript in Conclave Functions](javascript-in-conclave-functions.md) | Writing JavaScript for Conclave Functions is not quite the same as for other platforms such as node. Find more out about it here. |
| [The ConclavePass Sample](conclavepass-sample.md)                       | View an in-depth example which shows how to use TypeScript in Conclave Functions, Java clients, and JavaScript clients.           |

You can interact with Conclave Cloud using the *Conclave Cloud Command Line Interface (`ccl`)* as well as client SDKs 
for Java, Kotlin, and JavaScript. You can obtain the latest versions of these tools and SDKs from the table below.

| Tool/SDK                                                                                                                                                       | Description                                                                                              | Copyright Notice                                                                                                            | License                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- |----------------------------------------------------------------------------------------------------------| --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [Command Line tool for Linux or macOS](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/ccl)                                      | Manage your Conclave Cloud projects and services from the terminal.                                      | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/CLI.NOTICE.txt)                   | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/License.txt) |
| [Command Line tool for Windows](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/ccl.zip)                                         | Manage your Conclave Cloud projects and services from the terminal.                                      | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/CLI.NOTICE.txt)                   | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/License.txt) |
| [Conclave Cloud JavaScript Client SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/conclave-cloud-sdk-1.0.0-beta2.tgz)       | Interact with Conclave Cloud and invoke Conclave Functions from your TypeScript/JavaScript applications. | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/JavaScript.Client.SDK.Notice.txt) | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/License.txt) |
| [Conclave Cloud Java/Kotlin Client SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/conclave-cloud-sdk-java-1.0.0-beta2.zip) | Interact with Conclave Cloud and invoke Conclave Functions from your Java or Kotlin applications.        | [Copyright](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/Java.Client.SDK.Notice.txt)       | [License](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/License.txt) |

For information about the current release and about previous releases, please visit the [releases page](releases.md).

## Installing the `ccl` tool

You need Java 11 or higher runtime environment to run the `ccl` tool.

=== "Linux/macOS"

    1. Download the `ccl` tool using [this link](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/ccl).
    2. Add the directory containing the `ccl` tool to your `PATH` environment variable.
    3. Test it by executing `ccl`.

=== "Windows"

    1. Download the zip file using [this link](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/ccl.zip).
    2. Unzip the contents to the folder of your choice.
    3. Open the start menu, type **env**, and choose **Edit the system environment variables**.
    4. Click the **Environment Variables** button.
    5. Find the **Path** entry, edit it, and add the folder containing the tool to the path value.
    6. Restart your command prompt to ensure the path has been updated.

Note that for Windows, whenever you are asked to type `ccl`, you need to replace it with `ccl.bat`.

## Installing the Conclave Cloud JavaScript client SDK

1. Download and unzip [the SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/conclave-cloud-sdk-1.0.0-beta2.tgz))
   to the directory of your choice.
   
   The zip file contains an npm-compatible component. You can import it into your JavaScript/TypeScript 
   application by setting it as a dependency in your project.

2. To add it as a dependency, add the following to your `package.json`, making sure to provide the correct path to 
   where you unzipped the SDK.

```json
"dependencies": {
    ...
    "conclave-cloud-sdk": "file:path/to/conclave-cloud-sdk-1.0.0-beta2.tgz",
    ...
}
```


## Installing the Conclave Cloud Java/Kotlin Client SDK


1. Download and unzip [the SDK](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-beta2/conclave-cloud-sdk-java-1.0.0-beta2.zip)
   to the directory of your choice.

   The zip file contains a file-based Maven repository.

2. Add the repository to your `build.gradle.kts`, making sure to provide the correct path to where you unzipped the SDK.

```kotlin
repositories {
	maven(url = "path/to/conclave-cloud-sdk/repo")
	mavenCentral()
}
```

3. Add the SDK as a dependency:

```kotlin
	// Conclave Cloud
	implementation("com.r3.conclave.cloud:conclave-cloud-sdk:1.0-RC1")
```
