# Invoking a Conclave Function using the Conclave Cloud Java SDK

This tutorial details how to invoke a simple function using the Conclave Cloud Java/Kotlin SDK. After completing 
this tutorial, you will be able to invoke a Conclave Cloud function from the project UI.

## Prerequisites

To follow this tutorial, you should already have done the following:

- Sign-up for a [Conclave Cloud](https://www.conclave.cloud/) account and log in to the portal.
- Download and install the `ccl` tool following the instructions [here](index.md).
- Upload the `simple.js` function to [Conclave Cloud](https://www.conclave.cloud/) following the instructions [here](creating-your-first-function.md).

## 1. Install and configure the Conclave Cloud Java SDK

* Download the Java SDK zip file from this [link](https://github.com/R3Conclave/ccl-documentation/releases/download/1.0.0-GA/conclave-cloud-sdk-java-1.0.0-GA.zip).

* Unzip the SDK to the directory of your choice. Add the repository to your build.gradle.kts, making sure to provide 
  the correct path to where you unzipped the SDK.
  ```
  repositories {
    maven(url = "path/to/conclave-cloud-sdk/repo")
    mavenCentral()
  }
  ```
* Add the SDK as a dependency:
  ```
  // Conclave Cloud
  implementation("com.r3.conclave.cloud:conclave-cloud-sdk:1.0-RC1")

* Create a project.

* In the project's root directory, create a new file and call it `ConclaveCloud.js`.

* Create an API key using the Conclave Cloud CLI command line tool:
  `ccl apikeys create`

* Add the following configurations to `ConclaveCloud.js`
   ```
   clientConfig = new ConclaveClientConfig(
    "apiKey",                                    // Replace with the API key you've created.
   Conclave.PRODUCTION_API_URL                   // The URL of the Conclave Cloud API service.
   );
   conclave = Conclave.create(clientConfig);
   ```

## 2. Invoke Call via SDK

The `conclave` instance that you created in the earlier step contains a helper named `functions`, which you can use to 
invoke a function.

You can call a function as follows:

```
retval = conclave.functions.call(
         <name>,
         <hash>,
         [args]
         );
```
The parameters in the above syntax are described below:

| Parameter  | Description                                                                                                                                                                                      |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name       | The name of the function to invoke. This must match the function name that was specified when the function was uploaded.                                                                         |
| hash       | The SHA256 hash of the uploaded JavaScript function code concatenated with the function entry point.                                                                                             |
| args       | A [Jackson ArrayNode](https://fasterxml.github.io/jackson-databind/javadoc/2.6/com/fasterxml/jackson/databind/node/ArrayNode.html) containing the arguments to pass to the function entry point. |
        

* It should look like this:
  ```
  retval = conclave.functions.call(
           "sayHello",
           "60C5AEFCE46A44163467EC82C204AB5207B780A45527A65A6580886AECAC49D4",
           [input]
           );
  ```

* You can now invoke the function from the UI.