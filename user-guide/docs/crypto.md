# Conclave Functions `crypto` module

To safely export data from serverless functions, each function has access to an encryption key that is unique to the 
function code within the Conclave Cloud project.

You can use this encryption key to protect data that can subsequently be accessed only by the same function code 
within the same project. No other entity can access it, including the data originator.

Using this key allows functions to securely export and import state, providing a simple way to combine datasets or 
derive information from multiple data sources without ever giving access to the data to any entity other than the 
function itself.

## Key derivation

The key used to encrypt the data is derived in the sequence defined below:

1. The Conclave Cloud master key.
2. The Project key.
3. The hash of the source code that defines a function or a set of functions.

Each source code module obtains a unique key even if you upload the same code to another Conclave Cloud project.

Please note that the key does not include the hash of the function entry point. So, a set of functions defined in a 
single code module can share a key, making it easy to develop an entire module that works with an encrypted state.

You must upload each function within a different source module if you wish to create a cryptographic separation between 
two separate functions in the same project.

## Example

This example shows how to encrypt data that can only be decrypted by functions defined in the same module within the 
same project. To do this, use the project key as a passphrase for the crypto-js `AES.encrypt` function.

```javascript
const encrypted = AES.encrypt(data_to_encrypt, crypto.getProjectKey());
```

## 'crypto' Interface

`crypto.getProjectKey()`

Gets the project key - the key unique to the code module within the project where you have hosted the code.

The function returns a 32-byte, [Base64](https://www.base64decode.org/) encoded key.
