# Using JavaScript in Conclave Functions
Conclave Functions provides a fully capable ES6 JavaScript engine in which to
execute your function code. However, due to the nature of enclaves, not
everything works inside an enclave.

## JavaScript Engine
Conclave functions provides a pure JavaScript engine. It does not provide full
support for environments like Node.js (yet). This means that without importing
libraries, you do not have access to Node.js built-ins such as file support or
`Buffer`.

However, you can create a project using npm and import standard packages to fill
in the gaps.

The [ConclavePass sample](https://github.com/R3Conclave/ccl-sample-conclavepass)
uses this technique, implementing an npm component that compiles to a single
JavaScript file for upload, importing a cryptographic library, buffer and other
useful tools.

In addition, the Conclave Cloud `ccl` tool provides a command to bootstrap a new
JavaScript or TypeScript project that supports multiple code modules and
packages and packs them into a single JavaScript file for uploading to Conclave
Functions. You can read how you can use this to 
[create your function module here](creating-a-function-module.md).

