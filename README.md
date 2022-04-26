# Conclave Cloud Documentation
```
   ___                 _                     ___ _                 _
  / __\___  _ __   ___| | __ ___   _____    / __\ | ___  _   _  __| |
 / /  / _ \| '_ \ / __| |/ _` \ \ / / _ \  / /  | |/ _ \| | | |/ _` |
/ /__| (_) | | | | (__| | (_| |\ V /  __/ / /___| | (_) | |_| | (_| |
\____/\___/|_| |_|\___|_|\__,_| \_/ \___| \____/|_|\___/ \__,_|\__,_|
Conclave Cloud - the serverless platform that preserves privacy using Intel SGX.
```

[Conclave Cloud](https://conclave.cloud) provides a set of services within
the platform, all of which can be accessed using this client library.

[Conclave Functions](https://functions.conclave.cloud) is a serverless
  framework that allows your project to run backend code in a privacy preserving
  environment.

## Documentation for the Conclave Cloud platform

This repository contains source files for various different R3 Conclave Cloud platform information sites and sources. Each subfolder contains a different set of documentation as outlined in the table below.

## Documents
| Document | Folder | Notes |
| -------- | ------ | ----- |
| Conclave Cloud user documentation | `user-guide` | A collection of document source files that are used to build the Conclave Cloud user documentation pages. |
| REST API specification | `openapi` | An OpenAPI specification that defines the REST interface for Conclave Cloud. |

## Publishing
The rendered pages from `user-guide` are hosted on GitHub pages at [https://r3conclave.github.io/ccl-documentation/](https://r3conclave.github.io/ccl-documentation/).

The latest version can be generated and pushed to the `gh-pages` branch using the following commands.

```
cd user-guide
mkdocs gh-deploy
```

The pages at the hosted URL will update within a few minutes.

