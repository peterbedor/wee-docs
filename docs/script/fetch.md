# Fetch

Data request and binding functions

## Response

Response object returned by all requests

### Properties

| Variable   | Type           | Default | Description            | Required |
|------------|----------------|---------|------------------------|----------|
| config     | object         | -       | Request configuration  | -        |
| data       | object, string | -       | Response data          | -        |
| headers    | object         | -       | Parse response headers | -        |
| request    | object         | -       | XHR request object     | -        |
| status     | number         | -       | Response status code   | -        |
| statusText | string         | -       | Response status text   | -        |

## $fetch

Make Ajax request

| Variable | Type   | Default | Description           | Required |
|----------|--------|---------|-----------------------|----------|
| options  | object | -       | Request options below | ✔        |

### Options Object

| Variable           | Type            | Default  | Description                                                                                                                      | Required |
|--------------------|-----------------|----------|----------------------------------------------------------------------------------------------------------------------------------|----------|
| url                | string          | -        | Request location                                                                                                                 | -        |
| data               | object, string  | -        | Data to be sent as the request body                                                                                              | -        |
| method             | string          | get      | Request verb - `get`, `post`, `put`, `patch`, `delete`                                                                           | -        |
| auth               | object          | -        | Set `username` and `password` for HTTP Basic auth. Will set Authorization header                                                 | -        |
| baseUrl            | string          | -        | Prepended to `url` unless `url` is absolute                                                                                      | -        |
| disableCache       | boolean         | false    | Add query string to request to bypass browser caching                                                                            | -        |
| headers            | object          | -        | Custom headers to be sent with request                                                                                           | -        |
| jsonp              | boolean, string | false    | Make JSONP request. If a string is provided, it will be used for the query parameter name instead of the default name `callback` | -        |
| jsonpCallback      | string          | 'jsonp1' | Name of function to be executed when JSONP response is returned                                                                  | -        |
| onDownloadProgress | function        | -        | Allows handling of progress events for downloads                                                                                 | -        |
| onUploadProgress   | function        | -        | Allows handling of progress events for uploads                                                                                   | -        |
| params             | object          | -        | Object of properties that will be added to the query string of the request URL                                                   | -        |
| processData        | boolean         | true     | Auto-format request                                                                                                              | -        |
| responseType       | string          | json     | Indicates type of data expected from server - `arraybuffer`, `blob`, `document`, `json`, `text`                                  | -        |
| scope              | object          | -        | Callback scope                                                                                                                   | -        |
| send               | function        | -        | Callback that executes before AJAX request is made                                                                               | -        |
| timeout            | number          | -        | Set timeout for request                                                                                                          | -        |
| transformRequest   | function        | -        | Customize how request body is transformed before sending                                                                         | -        |
| transformResponse  | function        | -        | Customize format of response data                                                                                                | -        |
| validateStatus     | function        | -        | Customize successful status code                                                                                                 | -        |

### Get

```js
import $fetch from'wee-fetch';

$fetch({ url: '/api.test' }).then((response) => {
    console.log(response.data.ok);
}).catch((error) => {
    console.error(error);
});
```

### Jsonp

```js
import $fetch from'wee-fetch';

$fetch({
    url: '/api.test',
    jsonp: true
}).then((response) => {
    console.log(response.data.ok);
}).catch((error) => {
    console.error(error);
});
```

### Post with Data

```js
import $fetch from'wee-fetch';

$fetch({
    url: '/contact-form',
    method: 'post',
    data: {
        name: 'Kevin',
        email: 'kevin@gmail.com'
    }
}).then(response => {
    console.log(response.status);
}).catch((error) => {
    console.error(error);
});
```

### Instantiation

Fetch can be instantiated. This is useful for when you want to set base configurations once that will be used for multiple requests in the future.

```js
import $fetch from'wee-fetch';

const apiFetch = $fetch.create({
  baseUrl: 'https://some-domain.com/api',
  timeout: 1000,
  headers: { 'X-Custom-Header': 'foobar' }
});

apiFetch({
    url: 'users', // URL will be appended to baseURL
}).then((response) => {
    console.log(response);
}).catch((error) => {
    console.log(error);
});
```

## $fetch.post

Convenience method for performing post requests

### Parameters

| Variable | Type   | Default | Description                     | Required |
|----------|--------|---------|---------------------------------|----------|
| url      | string | -       | Request location                | ✔        |
| data     | object | -       | Data to be sent as request body | ✔        |
| options  | object | -       | [Request options](#fetch)       | -        |

### Simple

```js
import $fetch from'wee-fetch';

$fetch.post('/api/users', { name: 'Tom', email: 'tommy1@gmail.com' })
  .then(response =>console.log(response))
  .catch(error =>console.error(error));
```

### With Options

```js
import $fetch from'wee-fetch';

$fetch.post('/api/users', { name: 'Tom', email: 'tommy1@gmail.com' }, {
  responseType: 'text'
}).then(response =>console.log(response))
  .catch(error =>console.error(error));
```

## $fetch.put

Convenience method for performing put requests

### Parameters

| Variable | Type   | Default | Description                     | Required |
|----------|--------|---------|---------------------------------|----------|
| url      | string | -       | Request location                | ✔        |
| data     | object | -       | Data to be sent as request body | ✔        |
| options  | object | -       | [Request options](#fetch)       | -        |

### Simple

```js
import $fetch from'wee-fetch';

$fetch.put('/api/users/1', { name: 'Tom Haverford', email: 'tommy1@gmail.com' })
  .then(response =>console.log(response))
  .catch(error =>console.error(error));
```

### With Options

```js
import $fetch from'wee-fetch';

$fetch.put('/api/users/1', { name: 'Tom Haverford', email: 'tommy1@gmail.com' }, {
  responseType: 'text'
}).then(response =>console.log(response))
  .catch(error =>console.error(error));
```

## $fetch.patch

Convenience method for performing patch requests

### Parameters

| Variable | Type   | Default | Description                     | Required |
|----------|--------|---------|---------------------------------|----------|
| url      | string | -       | Request location                | ✔        |
| data     | object | -       | Data to be sent as request body | ✔        |
| options  | object | -       | [Request options](#fetch)       | -        |

### Simple

```js
import $fetch from'wee-fetch';

$fetch.patch('/api/users', { name: 'Tom Haverford' })
  .then(response =>console.log(response))
  .catch(error =>console.error(error));
```

### With Options

```js
import $fetch from'wee-fetch';

$fetch.patch('/api/users', { name: 'Tom Haverford' }, {
  responseType: 'text'
}).then(response =>console.log(response))
  .catch(error =>console.error(error));
```

## $fetch.get

Convenience method for performing get requests

### Parameters

| Variable | Type   | Default | Description               | Required |
|----------|--------|---------|---------------------------|----------|
| url      | string | -       | Request location          | ✔        |
| options  | object | -       | [Request options](#fetch) | -        |

### Simple

```js
import $fetch from'wee-fetch';

$fetch.get('/api/users')
  .then(response =>console.log(response))
  .catch(error =>console.error(error));
```

### With Options

```js
import $fetch from'wee-fetch';

$fetch.get('/api/users', {
  responseType: 'document'
}).then(response =>console.log(response))
  .catch(error =>console.error(error));
```

## $fetch.delete

Convenience method for performing delete requests

### Parameters

| Variable | Type   | Default | Description               | Required |
|----------|--------|---------|---------------------------|----------|
| url      | string | -       | Request location          | ✔        |
| options  | object | -       | [Request options](#fetch) | -        |

### Simple

```js
import $fetch from'wee-fetch';

$fetch.delete('/api/users')
  .then(response =>console.log(response))
  .catch(error =>console.error(error));
```

### With Options

```js
import $fetch from'wee-fetch';

$fetch.delete('/api/users', {
  responseType: 'document'
}).then(response =>console.log(response))
  .catch(error =>console.error(error));
```
