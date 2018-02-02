# Fetch

Data request and binding functions

## Request

Make Ajax request based on specified options

|Variable|Type    |Default |Description          |Required|
|--------|--------|--------|---------------------|--------|
|options |object  |-       |Request options below|✔		  |

### Options Object 

|Variable     |Type                         |Default |Description                                                  |Required|
|-------------|-----------------------------|--------|-------------------------------------------------------------|--------|
|args         |array                        |-       |Callback arguments appended after default parameters         |-       |
|cache        |boolean                      |true    |Disable automatic cache-busting query string                 |-       |
|complete     |[function](/script#functions)|-       |Complete callback                                            |-       |
|data         |object                       |-       |Object to serialize and pass along with request              |-       |
|error        |[function](/script#functions)|-       |Failure callback                                             |-       |
|headers      |object                       |-       |{key: val} object of request headers                         |-       |
|json         |boolean false                |-       |Evaluate the response as JSON and return object              |-       |
|jsonp        |boolean, string              |false   |Boolean or override name for callback query string parameter |-       |
|jsonpCallback|string                       |-       |Override the name of the JSONP callback function             |-       |
|method       |string                       |get     |Request verb (get, post, put, etc) in lowercase              |-       |
|processData  |boolean                      |true    |Post data in the body if applicable                          |-       |
|root         |string                       |-       |Prepended request path                                       |-       |
|scope        |object                       |-       |Callback scope                                               |-       |
|send         |[function](/script#functions)|-       |Send callback                                                |-       |
|success      |[function](/script#functions)|-       |Success callback                                             |-       |
|type         |string                       |-       |Form, html, json, or xml to toggle content type header       |-       |
|url          |string                       |-       |URL endpoint to request                                      |✔		|

### Get

The callback receives the response as the first parameter followed by the XHR object. Any custom arguments provided are injected afterwards.

```js
Wee.fetch.request({
    url: '/samples/test.json',
    success: function(data, xhr) {
        console.log(data);
    }
});
```

By default the X-Requested-With header is set to XMLHttpRequest. Also, when `js json` is set to true the Content-Type header is set to 'application/json’. Either can be overridden or removed if set to false.

### Post w/Data

```js
Wee.fetch.request({
    url: '/samples/login.php',
    method: 'post',
    data: {
        username: 'user@weepower.com',
        password: 'pass123'
    },
    success: function(data) {
        console.log('Login succeeded');
    },
    error: function(data) {
        console.log('Login failed');
    }
});
```

### JSONP

JSONP is a technique for cross-domain requests that would otherwise be blocked because of the same-origin policy. Unless overridden Wee will send `js callback` as the query string parameter to communicate to the server how to format the response.

```js
Wee.fetch.request({
    url: 'https://example.com/entry/465',
    jsonp: true,
    success: function(data) {
        console.log('Login succeeded');
    }
});
```

The request above will create a script reference in the head with the source set to `js https://example.com/entry/465?callback=callback1`. If configured correctly the server will return a JSON object executed like the following.

```js
callback1({
    id: 465,
    name: "Lorem Ipsum",
    active: true
});
```

The `jsonpCallback` parameter can be set to direct the callback to a pre-existing method instead of the generically registered success callback.