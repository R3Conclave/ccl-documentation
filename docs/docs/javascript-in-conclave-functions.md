# Using JavaScript in Conclave Functions
Conclave Functions provides a fully capable ES6 JavaScript engine in which to
execute your function code. However, due to the nature of enclaves, not
everything works inside an enclave.

## Conclave Functions != Node.js
Conclave functions provides a pure JavaScript engine. It does not provide
Node.js support (yet). This means that you do not have access to Node.js
built-ins such as file support or Buffer.

However, you can create a project using npm and import standard packages to fill
in the gaps, particular with support for objects like `Buffer`.

The [ConclavePass sample](https://github.com/R3Conclave/ccl-sample-conclavepass)
uses this technique, implementing an npm component that compiles to a single
JavaScript file for upload, importing a cryptographic library, buffer and other
useful tools.

## Accessing external web services
Conclave Functions are stateless and do not have access to any persistent
storage. Therefore, external storage within the cloud is necessary in order to
persist the user databases. 

The JavaScript engine in Conclave Functions supports a subset of the JavaScript
`fetch()` built-in capability to query and update an external data store with
each user's encrypted database entries. 

It is vitally important to ensure that any data exchanged via `fetch()` is
encrypted as the request is made outside the Conclave Functions Intel SGX
enclave. 

Here is an example of using `fetch()` to `GET` a URL:

```javascript
cclexports = {
    lookup: async (url) => {
        var retval = await fetch(url);
        return await retval.text();
    }
}
```

And another example showing a `POST`:

```javascript
cclexports = {
    lookup: (url) => {
        var retval;
        fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: "{ \"test\": \"Hello\" }"
        }).then(result => {
            result.text().then(text => {
                retval = text;
                }, error => {})
        });
        return retval;
    }
}
```

## Accessing a per-function cryptographic key
In order to allow data to be safely exported from a function, an encryption key
is provided that can be used to encrypt data that can subsequently only be
encrypted by exactly the same function code within the same project.

The key is derived directly from the project key - a key that is unique to the
tenant/project that can only be accessed within the Conclave Functions enclave.
This key is not used directly, instead it is derived using the hash of the code
module that is currently executing. 

Note that it does not include the entry point in the derivation process meaning
that a single code module that exports multiple functions will have the same
hash, allowing a set of Conclave Functions to all access the same encryption
key.

The key can be obtained from within JavaScript code using:

```javascript
const key = crypto.getProjectKey();
```

Note that this API is likely to change in future versions of Conclave Functions,
to add more key derivation possibilities.

