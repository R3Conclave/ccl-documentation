# Invoking your first Function using the Conclave Cloud JS SDK

This is a set-up tutorial on how to invoke a simple JavaScript function using the React framework and the Conclave Cloud JS SDK.

> This is a step-by-step walkthrough and uses the [Hello Conclave Cloud project](https://github.com/R3Conclave/ccl-sample-conclavepass).  
> Once completed the User can invoke a conclave cloud function from the project ui.

## Prerequisites

In order to follow this tutorial you should already have done the following:

- Sign-up for a [Conclave Cloud Beta](https://www.dev.conclave.cloud/) account and log in to the portal.
- Download and install the `ccl` tool for your operating system and verify it
  works.
- Upload the simple.js function to [Conclave Cloud Beta](https://www.dev.conclave.cloud/) by following the steps documented in ["Creating your first function"](/creating-your-first-function/).

## 1. Run the Hello Conclave Cloud project

Get the [Hello Conclave Cloud Tutorial](https://github.com/R3Conclave/ccl-sample-conclavepass) repository:

```
git clone https://github.com/R3Conclave/conclave-cloud-samples.git
```

In the project directory install and run the project:  
`npm install`  
`npm start`

_This is the base ui set-up for the sayHello function call, the sdk has yet to be configured._

## 2. Install and Configure the Conclave Cloud SDK

Install the conclave-cloud-sdk npm package:  
`npm install conclave-cloud-sdk --save`

In the projects root directory create a new file and call it `ConclaveCloud.js`  
Add the following configurations:

```
import { Conclave } from 'conclave-cloud-sdk'

const conclaveConfig = new Conclave.create({
    tenantID: 'tenantId',
    projectID: 'projectId',
});

export default conclaveConfig;
```

~ Id's can be found in a selected projects dashboard screen in ([Conclave Cloud Beta](https://www.dev.conclave.cloud/)) or running the following CLI commands:

`ccl platform tenant`

`ccl projects list`

> This project was built using create-react-app which due to webpack 5 have breaking changes. The project has already been set-up to use react-app-rewired to bypass the errors. To learn more about breaking changes and the options to bypass read Section 4.Fixing Breaking Changes with create-react-app below.

## 3. Invoke Call via SDK

import conclaveConfig into the app.tsx

```
import conclaveConfig from "./ConclaveCloud";
```

Add the following to the sendMessage() function:

```
      response = await conclaveConfig.functions.call(
        "function name",
        "function hash",
        [args]
      );
```

> [args] value will be the input value from the project
> It should look like so:

```
      response = await conclaveConfig.functions.call(
        "sayHello",
        "60C5AEFCE46A44163467EC82C204AB5207B780A45527A65A6580886AECAC49D4",
        [input]
      );
```

You can Now invoke the function from the ui.

## 4. Fixing Breaking Changes with create-react-app

Due to create-react-app using Webpack 5+, you will experience some breaking changes due to polyfills not being included. Below are options to use in your project to include polyfills, either by downgrading to Webpack 4.\*or by manually including polyfills:

### Downgrading react-scripts:

`npm uninstall react-scripts`  
`npm install react-scripts@4.0.3`

### Adding a Webpack config file with fallback:

In the root project directory create the file webpack.config.js, add the following:

```
module.exports = {
  resolve: {
    fallback: {
      crypto: require.resolve('crypto-browserify'),
      stream: require.resolve('stream-browserify'),
    },
  },
};
```

then  
`npm install crypto-browserify stream-browserify --save`

### Adding fallback to react-script's webpack configuration file:

After initial npm install navigate to `node_modules/react-scripts/config/webpack.config.js, find module.exports in this file.  
In module.exports section find resolve section and add the following

```
fallback: {
crypto: require.resolve('crypto-browserify'),
stream: require.resolve('stream-browserify'),
}
```

The section should look like this:

```
module.exports = function (webpackEnv) {
...
return {
...
resolve: {
...
fallback: {
crypto: require.resolve('crypto-browserify'),
stream: require.resolve('stream-browserify'),
}
}
}
}
```

### Using react-app-rewired:

Run the following:  
`npm install react-app-rewired`

In the root project directory create the file `config-overrides.js`  
Add the following:

```
module.exports = function override(config) {
const fallback = config.resolve.fallback || {};
Object.assign(fallback, {
"stream": require.resolve("stream-browserify"),
"crypto": require.resolve("crypto-browserify")
});
config.resolve.fallback = fallback;
return config;
};
```

then:  
`npm install crypto-browserify stream-browserify --save`  
in package.json change the start scripts:

```
"scripts": {
"start": "react-scripts start",
```

change to

```
"scripts": {
"start": "react-app-rewired start",
```

then

`npm start`
