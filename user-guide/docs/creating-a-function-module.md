# Creating a Function Module using `ccl`
A Conclave Function needs to be uploaded in a single JavaScript file. However,
you can use a transpiler and a packing tool to take a multi-file project using any
language that can be transpiled into JavaScript, transpile it then pack it into
a single file for upload.

When configuring a module in this way, it can be quite difficult to get the
correct configuration in order to support the version of JavaScript and export
mechanism that Conclave Functions uses. For that reason, the Conclave Cloud
`ccl` tool provides commands to create both TypeScript and JavaScript modules as
well as to add new functions to existing modules.

## Creating a new Function Module
Firstly 
[ensure you have the `npm` tool installed](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) 
to allow the Function Module to be managed and built.

Open a terminal or command prompt in the directory where you want to create your
module and run the following command:

```
ccl module new --language=[language] --project=[project name or UID] --root=[module_name]
```

The `language` value can be either `typescript` or `javascript` depending on the
type of module you want to create.

The `project name or UID` should be set to the project that you will be uploading
the function module into. This can be changed after the module has been created
by editing the configuration files. If you have used the command `ccl save` to
set a default project UID/name then you can omit this parameter.

The `module_name` is the name of the module and will be used as the name for the
directory containing the module.

For example, to create a TypeScript module named `mymodule` in the current
default project, use the following command:

```
ccl module new --language=typescript --root=mymodule
```

The generated module will contain the following files:

| Path | Description |
| ---- | ----------- |
| cclmodule.json | The configuration of the module during creation. This information will be used by `ccl` when running commands to modify the module. |
| package.json | The npm configuration file that contains metadata and dependencies for the module. |
| README.md | Information about the generated module, including information about how to build and upload the module to Conclave Cloud. |
| tsconfig.json | For TypeScript projects, contains the configuration of the TypeScript transpiler, pre-configured to work with Conclave Cloud. |
| webpack.config.js| Webpack configuration file that assembles all source modules and dependencies into a single JavaScript file for upload to Conclave Cloud. |
| src/index.ts | A code module that exports the functions defined in the module. This will be updated by `ccl` each time you add a function to the module. |
| test/test.js | A JavaScript file that can be edited to test the functions within your module. |
| test/template/polyfill.js | A JavaScript file that emulates the JavaScript modules supported in the Conclave Functions runtime environment. |

## Adding a function to the module
When you first create a function module it is created as an empty module that
does not contain any exported functions. In order to create a Conclave Function
you need to create a new function within the module.

From a terminal within the root directory of your module:

```
ccl module add --name=[name of function]
```

For example, to create a function named `function1` in the `mymodule` module:

```
cd mymodule
ccl module add --name=function1
```

The command will generate a new source file named `src/functions/function1.ts`
which contains the following placeholder code:

```typescript
// Auto-generated function code, generated with the Conclave Cloud ccl tool.
// Replace the implementation below with your own code.
export async function function1(arg1: string, arg2: string): Promise<string> {
    return arg1 + arg2;
}
```

Replace the code in the function with your own implementation.

## Preparing the module build
Like with any other `npm` module, you need to install the tools and dependencies
for the module before it can be built or uploaded.

Run this command from the root directory of the module.

```
npm install
```

## Testing
An empty test module has been provided in `test/test.js`. Modify this file to exercise your
Conclave Functions before uploading. You can run the tests with the following command:

```
npm run test
```

## Uploading your module
Once you have added and implemented your functions you can use `npm` to upload
them to Conclave Cloud. They will be uploaded to the project you defined when
creating the module unless you have edited the configuration to use a different
project.

Run this command to upload to the module project:

```
npm run upload
```

## Targeting a different Conclave Cloud Project
If you wish to change the project that the module is targeting then you must edit the 
project UID in `cclmodule.json` and the entries in the upload script in
`package.json`.

## Adding modules using npm
You can add third party dependencies to your module using the `npm` tool, as
long as they do not depend on capabilities that are not present in Conclave
Functions (such as `fs` file support).

For example, to add the `CryptoJS` library to your module:

```
npm install crypto-js
```

You can then use CryptoJS in your function module:

```typescript
import {AES} from "crypto-js";

export async function function1(arg1: string, arg2: string): Promise<string> {
    const encrypted = AES.encrypt(arg1 + arg2, crypto.getProjectKey());
    return encrypted.toString()
}
```