# Conclave Functions `fetch` module
Conclave Functions are stateless and do not have access to any persistent
storage. Therefore, external storage within the cloud is necessary in order to
persist the user databases. 

The JavaScript engine in Conclave Functions supports a subset of the JavaScript
`fetch()` built-in capability to query and update an external data store with
each user's encrypted database entries. 

It is vitally important to ensure that any data exchanged via `fetch()` is
encrypted as the request is made outside the Conclave Functions Intel SGX
enclave. 

## Example

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

# Fetch Interface
`fetch()`

The main method that is used to fetch a resource.

### Usage:
```javascript
fetch(url, options).then(function(response) {
    // Handle HTTP response
}, function(error) {
    // Handle error
}
```

### Options
| Field | Description |
| ----- | ------------|
| `method` | The HTTP verb: POST/PUT/GET/DELETE/PATCH |
| `body` | The request body. |
| `headers` | Optional headers specified as an object. |
| `credentials` | Authentication credentials. |

### Response
An object that represents the response from a server.

| Field/Method | Description |
| ------------ | ----------- |
| `status` | HTTP response status (100-599). |
| `statusText` | Textual representation of the status. |
| `ok` | True if the status is `2xx`. |
| `text()` | Return the response as a string. |
| `json()` | Response parsed using `JSON.parse`. |
| `arrayBuffer()` | Response as an array buffer. |