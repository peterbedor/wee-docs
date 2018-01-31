# Location

## $location.segments

Retrieve the current location's path segments as an array or individual segment by index

### Parameters

| Variable | Type   | Default | Description                                    | Required |
|----------|--------|---------|------------------------------------------------|----------|
| index    | number | -       | Specific index to retrieve from segments array | -        |

```js|js
import $location from'wee-location';

// Current URL is https://weepower.com/script/location
$location.segments();
$location.segments(1);

---

['script', 'location']
'location'
```

## $location.uri

Retrieve information about current location or parse a provided URL

### Parameters

| Variable | Type   | Default | Description      | Required |
|----------|--------|---------|------------------|----------|
| url      | string | -       | URL to be parsed | -        |

### Return Value

| Variable | Type   | Default | Description                              | Required |
|----------|--------|---------|------------------------------------------|----------|
| fullPath | string | -       | URL path, query string, and hash         | -        |
| hash     | string | -       | URL hash value with `#` omitted          | -        |
| path     | string | -       | URL path                                 | -        |
| search   | string | -       | Query string of URL including `?`        | -        |
| query    | object | -       | Unserialized key/value pairs from search | -        |
| segments | array  | -       | Parsed path segments                     | -        |
| url      | string | -       | Full URL value                           | -        |
| origin   | string | -       | Full URL origin                          | -        |
| protocol | string | -       | `http` or `https`                        | -        |
| port     | string | -       | URL port if available                    | -        |

```js|js
import $location from'wee-location';

$location.uri('https://origin.com:80/path/to/page?prop1=test#some-hash');

---

{
    fullPath: '/path/to/page?prop1=test#some-hash',
    hash: 'some-hash',
    path: '/path/to/page',
    search: '?prop1=test',
    query: { prop1: 'test' },
    segments: ['path', 'to', 'page'],
    url: 'https://origin.com/path/to/page?prop1=test#some-hash',
    origin: 'https://origin.com',
    protocol: 'https',
    port: '80'
}
```
