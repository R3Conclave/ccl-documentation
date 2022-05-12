# Conclave Functions `crypto` module
In order to allow data to be safely exported from serverless functions, each
function has access to an encryption key that is unique to the function code
within the Conclave Cloud project.

This encryption key can be used to protect data that can subsequently be
accessed by the same function code within the same project, but cannot be
accessed by any other entity including the data originator.

Using this key allows functions to securely export and import state, providing a
simple way to combine datasets or derive information from multiple data sources
without ever providing access to the data to any entity other than the function
itself.

## Key derivation
The key used to encrypt the data is derived in the sequence defined below:

1. The Conclave Cloud master key.
2. The Project key.
3. The hash of the source code that defines a function or a set of functions.

This means that each source code module obtains a unique key even if the same
code is uploaded to another Conclave Cloud project.

Note however though that the key is derived from the hash of the source code but
does not include the hash of the function entry point. Deriving a key in this
way means that a set of functions that are all defined in a single code module
can share a key, making it easy to develop an entire module that works with an
encrypted state. If you wish to make a cryptographic separation between two
different functions in the same project then you need to ensure each function is
uploaded within a different source module.

## Example
This example shows how to encrypt some data that can only be decrypted by
functions defined in the same module within the same project, using the project
key as a passphrase for the crypto-js `AES.encrypt` function.

```javascript
const encrypted = AES.encrypt(data_to_encrypt, crypto.getProjectKey());
```

## 'crypto' Interface
`crypto.getProjectKey()`

Get the project key - the key which is unique to the code module within the
project where the code is hosted.

The function returns a 32 byte key that is Base64 encoded to a string.
