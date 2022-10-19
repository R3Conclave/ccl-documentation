# Create, upload, and invoke your first function in Conclave Cloud

This tutorial illustrates the steps to create a simple JavaScript function, upload it to the Conclave Functions 
service, and invoke it.

## Prerequisites

To follow this tutorial, you should already have done the following as per the instructions [here](index.md):

* Sign-up for Conclave Cloud and log in to the portal.
* Download, install, and test the `ccl` tool.

## 1. Create a new project

You can create a new project using the [Conclave Cloud portal](https://www.conclave.cloud/) or the `ccl` tool.

### Using the portal

Click the **New Project** button and enter a name for the project.

![A screenshot of a button named 'New Project'](assets/NewProject.png)

### Using the CLI

Use the following command to create a new project.

```bash
ccl projects create --name "My Project"
```
_Note:_ A project UID will be auto-generated for you. Optionally, you may pick the UID of your project by adding
`--uid my-project` to the command above. Both the UID and the name must be unique.

You may be prompted to log in using your Conclave Cloud username and password.

## 2. Set the project as the default project in `ccl`

This step is for convenience to make subsequent command lines shorter.

Firstly, you need to get the project UID/name. You can see this in the portal's project page, or you can find it using 
`ccl`.

```bash
ccl projects list
```

Set the project UID/name as the default, replacing `UID/name` with the actual ID.

```bash
ccl save --project <UID/name>
```

## 3. Write a JavaScript function using any editor

Here's an example for you. Save it as 'simple.js'.

```javascript
cclexports = {
    sayHello: (name) => {
        return "Hello " + name;
    }
}
```

This creates a global object named `cclexports` that contains all the functions that should be exported from the 
JavaScript module. In this example, one function named `sayHello` returns a string that says "Hello " appended with the 
`name` argument.

_Note:_ The `cclexports` object is important. Conclave Functions will look for this when you upload the code to 
determine what functions can be called within the code module. Always populate this object with the function you 
want to call.

## 4. Upload the function

You can use the `ccl` tool to upload a function:

```bash
ccl functions upload --name "sayHello" --code simple.js --entry "sayHello"
```

Your function is live and hosted. You can call your function from anywhere.

Here, the arguments used are:

| Argument | Description                                         |
|----------|-----------------------------------------------------|
| `name`   | The function's name that appears in the portal.     |
| `code`   | The code module to upload.                          |
| `entry`  | The name of the exported function you want to call. |


The `name` and the `entry` need not be identical.

## 5. Invoke the function

You can use the `ccl` tool to invoke a function:

```bash
ccl invocations invoke --name "sayHello" --args "[\"World\"]"
```

The result should be similar to this:

```
*** The expected code hash has not been specified and has been set to the value calculated when the function was 
uploaded. Please ensure this hash is correct. ***

Result:
{"name":"sayHello","version":"1.0.0","invocationId":"73904ecb224a4971904ecb224a69713d","start":1649432866241,"end":1649432866671,"duration":430,"response":{"status":"success","result":{"result":"ABUBAAAAAAAAAAAABmludm9rZQAAAACyBkdL95AXywZ8ayxSOKGyIAb07XFAFRqIKsHG66ytZHrQC5SUS+SIc/3bc3jN/sPl5TKZQefKvgSEn+MBttCI2n49X0FB0zQ5gQjal5Z7w2JbcL0VYWtuXdN34wbpKpHyAQ90oqAQ1nw7O3iQQAyHjfO2ho3WatdAKvXGCj6fbnfGHL+vTfApXhSsrEDsEdp8iuRuT/jp/0V7NgP/DhWiA8sJS9AE9VCv0HWap/Us0jvmFKQUrrKB/jHAqTmDvRi5EPCSyaN/I3X8+xbIWXYtiXN4UNHmb2OxfMUzYkRdozx1VGNorsw9oZkos5/NvUbdUWfRV1d9+42ywK6qIWtDTADP0ITIkOaX9CpmZWgck9PkeFK/YEHhrTostoLmKzNxniaEUD/nVHexjzNXX31XFWTZ7cqPlT8fZ3gn8IqD7VuwAoxXQ0tNPfF7TqUqTXthqCO+7F+e63hXuD4rmUsV+sMeoiezt7ZQeCTvg4psSyomABK3kpkbWD/lKz9mgNB87DQsGGs="},"success":true,"size":565},"logs":[],"cause":null,"statusCode":null,"waitTime":235.0,"timeout":false,"initTime":334.0}

Decrypted:
{ "return": "Hello World" }
```

This result is the raw data returned by the function. The important bit is in the `Decrypted:` section at the 
bottom, as it contains the decrypted return of the function. The `ccl` tool creates a private key for communicating with
Conclave Cloud. This private key is the only entity that can decrypt the encrypted result in the data returned from 
the invocation.

You've successfully invoked your first function.

## Previous invocations

You can see a list of previous invocations using this command:

```bash
ccl invocations list
```

This command shows information such as how long the function took to run and whether it was a
[cold or warm start](https://azure.microsoft.com/en-in/blog/understanding-serverless-cold-start/). You may have to 
run the command more than once, as it doesn't always update immediately.

## Function list

You can see the list of functions that you have uploaded with the following command:

```bash
ccl functions list
```

## Explore the portal

The [Conclave Cloud portal](https://www.conclave.cloud/) provides you with graphs and metrics about your functions 
and invocations. Browse around and see what you discover.