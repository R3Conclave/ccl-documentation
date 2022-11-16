# Invoking a Conclave Function using the Conclave Cloud JavaScript SDK

This tutorial details how to invoke a simple JavaScript function using the React framework and the Conclave Cloud
JavaScript SDK. It uses the `Hello Conclave Cloud project` from the [Conclave Cloud samples repo](https://github.com/R3Conclave/conclave-cloud-samples/).

After completing this tutorial, you will be able to invoke a Conclave Cloud function from the project UI.

## Prerequisites

To follow this tutorial, you should already have done the following:

- Sign-up for a [Conclave Cloud](https://www.conclave.cloud/) account and log in to the portal.
- Download and install the `ccl` tool as per the instructions [here](index.md).
- Upload the simple.js function to [Conclave Cloud](https://www.conclave.cloud/) as per the instructions [here](creating-your-first-function.md).

## 1. Run the Hello Conclave Cloud project

* Get the [Hello Conclave Cloud Tutorial](https://github.com/R3Conclave/conclave-cloud-samples/) repository:
  
  ```
  git clone https://github.com/R3Conclave/conclave-cloud-samples.git
  ```

* Change to the `hello-conclave-cloud-tutorial` directory.

* Install and run the project:  
  
  `npm install`  
  `npm start`

  _This is the base UI set-up for the sayHello function call. The SDK is yet to be configured._

## 2. Install and configure the Conclave Cloud SDK

* Install the conclave-cloud-sdk npm package:  
  
  `npm install /path to file/conclave-cloud-sdk-1.0.0-beta2.tgz --save`

* Create a project.

* In the project's root directory, create a new file and call it `ConclaveCloud.js`.

* Create an API key using the Conclave Cloud CLI command line tool:
  
  `ccl apikeys create`

* Add the following configurations to `ConclaveCloud.js`
  
  ```
  import { Conclave } from 'conclave-cloud-sdk'
  const conclaveConfig = new Conclave.create({
        apiKey: 'apiKey' // replace with the apiKey you've created.
  });
  export default conclaveConfig;
  ```

_Note_
 
  > This project was built using create-react-app, which due to webpack 5, has breaking changes. The project has already been set up to use react-app-rewired to bypass the errors.  
  > To learn more about breaking changes and the options to bypass, you can read [this section](#4. Fixing-Breaking-Changes-with-create-react-app).

## 3. Invoke Call via SDK

* Import conclaveConfig into the app.tsx file
  
  ```
  import conclaveConfig from "./ConclaveCloud";
  ```

* Add the following to the `sendMessage` function:
  
  ```
  response = await conclaveConfig.functions.call(
     "function name",
     "function hash",
     [args]
   );
  ```

  > The [args] value is the input value from the project.

* It should look like this:
  
  ```
  response = await conclaveConfig.functions.call(
     "sayHello",
     "60C5AEFCE46A44163467EC82C204AB5207B780A45527A65A6580886AECAC49D4",
     [input]
    );
  ```

* You can now invoke the function from the UI.

## 4. Fixing Breaking Changes with create-react-app

Due to create-react-app using Webpack 5+, you will experience some breaking changes due to polyfills not being included.
Below are options to use in your project to include polyfills, either by downgrading to Webpack 4.\*or by manually
including polyfills:

### Downgrading react-scripts:

* Run the following commands:

  `npm uninstall react-scripts`  
  `npm install react-scripts@4.0.3`

### Adding a Webpack config file with fallback:

* In the root project directory, create the file `webpack.config.js`.
* Add the following to webpack.config.js:
  
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

* Run the following command.  
  
  `npm install crypto-browserify stream-browserify --save`

### Adding fallback to react-script's webpack configuration file:

* After the initial npm install, navigate to `node_modules/react-scripts/config/webpack.config.js` and find the
  module.exports section.

* In the module.exports section, find the resolve section, and add the following:
  
  ```
  fallback: {
  crypto: require.resolve('crypto-browserify'),
  stream: require.resolve('stream-browserify'),
  }
  ```

* The section should look like this:

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

* Run the following command:  
  `npm install react-app-rewired`

* In the root project directory, create a file `config-overrides.js`

* Add the following code to the `config-overrides.js` file:

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

* Run the following command:  
  `npm install crypto-browserify stream-browserify --save`

* In package.json, substitute the start scripts with the following lines:
  
  ```
  "scripts": {
  "start": "react-app-rewired start",
  ```

* Run the following command:
  
  `npm start`
