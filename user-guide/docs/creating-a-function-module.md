# Creating a function module using `ccl`

You need to upload a Conclave Function in a single JavaScript file. However, if you have a multi-file project, you can 
use a packing tool to pack it into a single file for upload. You can also use a transpiler to transpile your projects 
in other languages to Javascript.

When configuring a module using a transpiler, getting the correct configuration to support the version of JavaScript 
and export mechanism that Conclave Functions uses can be challenging. For that reason, the Conclave Cloud `ccl` tool 
provides commands to create TypeScript and JavaScript modules and add new functions to existing modules.

## Creating a new function module

1. Firstly,
[ensure you have the `npm` tool installed](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) 
to build and manage function modules.

2. Open a terminal or command prompt and change to the directory where you want to create your function module.

3. Run the following command:

```
ccl module new --language=<language_name> --project=<project_name or UID> --root=<module_name>
```

The `language` value can be either `typescript` or `javascript` depending on the type of module you want to create.

The `project name or UID` should be set to the project to which you upload the function module. You can change this 
after creating the module by editing the configuration files. You can omit this parameter if you have used the 
command `ccl save` to set a default project UID/name.

The `module_name` is the name of the module and is used as the name for the directory containing the module.

For example, to create a TypeScript module named `mymodule` in the current default project, use the following command:

```
ccl module new --language=typescript --root=mymodule
```

The generated module will contain the following files:

| Path                      | Description                                                                                                                                |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| cclmodule.json            | The module configuration during creation. `ccl` uses this information when running commands to modify the module.                          |
| package.json              | The npm configuration file that contains metadata and dependencies for the module.                                                         |
| README.md                 | Information about the generated module, including how to build and upload the module to Conclave Cloud.                                    |
| tsconfig.json             | For TypeScript projects, contains the configuration of the TypeScript transpiler, pre-configured to work with Conclave Cloud.              |
| webpack.config.js         | Webpack configuration file that assembles all source modules and dependencies into a single JavaScript file for upload to Conclave Cloud.  |
| src/index.ts              | A code module that exports the functions defined in the module. `ccl` updates this information each time you add a function to the module. |
| test/test.js              | A JavaScript file that you can edit to test the functions within your module.                                                              |
| test/template/polyfill.js | A JavaScript file that emulates the JavaScript modules supported in the Conclave Functions runtime environment.                            |

## Adding a function to the module

When you first create a function module, it is an empty module that does not contain any exported functions.

To create a Conclave Function, you must create a new function within the module.

1. Open a terminal or command prompt and use the following command within the root directory of your module:

   ```
   ccl module add --name=<name_of_function>
   ```

   For example, to create a function named `function1` in the `mymodule` module:

   ```
   cd mymodule
   ccl module add --name=function1
   ```

   The command generates a new source file named `src/functions/function1.ts` which contains the following placeholder 
   code:

   ```typescript
   // Auto-generated function code, generated with the Conclave Cloud ccl tool.
   // Replace the implementation below with your code.
      export async function function1(arg1: string, arg2: string): Promise<string> {
      return arg1 + arg2;
      }
   ```

2. Replace the code in the function with your implementation.

## Preparing the module build

Like with any other `npm` module, you need to install the tools and dependencies for the module before you can build 
or upload the module.

Run this command from the root directory of the module.

```
npm install
```

## Testing

You can find an empty test module in `test/test.js`. Modify this file to call your Conclave Functions before 
uploading. You can run the tests with the following command:

```
npm run test
```

## Uploading your module

Once you have added and implemented your functions, you can use `npm` to upload them. Conclave Cloud uploads your 
functions to the project you defined when creating the module unless you have edited the configuration to use a 
different project.

Run this command to upload to the module project:

```
npm run upload
```

## Targeting a different Conclave Cloud Project

If you wish to change the project that the module is targeting, then you must edit the project UID in `cclmodule.json`
and the entries in the upload script in `package.json`.

## Adding modules using npm

You can add third-party dependencies to your module using the `npm` tool, as long as they do not depend on 
capabilities not present in Conclave Functions (such as `fs` file support).

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