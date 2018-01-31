# Mediator

## $mediator.emit

Publish to topic

### Parameters

| Variable | Type   | Default | Description                                                                                    | Required |
|----------|--------|---------|------------------------------------------------------------------------------------------------|----------|
| topic    | string | -       | Name of topic                                                                                  | ✔        |
| args     | *      | -       | Argument(s) to pass to subscriber callback functions registered with [on](#mediator-on) method | -        |

```js|js
import $mediator from'wee-mediator';

$mediator.on('message', (subject, message) => {
    console.log(subject);
    console.log(message);
});

$mediator.emit('message', 'Test', 'Can you hear me?');

---

'Test'
'Can you hear me?'
```

## $mediator.on

Subscribe to topic

### Parameters ### (.doc__label .doc__variables__label)

| Variable | Type     | Default | Description                                   | Required |
|----------|----------|---------|-----------------------------------------------|----------|
| topic    | string   | -       | Name of topic                                 | ✔        |
| callback | function | -       | Function to execute upon publication to topic | ✔        |

```js|js
import $mediator from'wee-mediator';

$mediator.on('message', (subject, message) => {
    console.log(subject);
    console.log(message);
});

$mediator.emit('message', 'Test', 'Can you hear me?');

'Test'
'Can you hear me?'
```

## $mediator.remove

Remove subscriber by id or all subscribers from topic

### Parameters

| Variable   | Type             | Default | Description                                   | Required |
|------------|------------------|---------|-----------------------------------------------|----------|
| topic      | string           | -       | Name of topic                                 | ✔        |
| identifier | string, function | -       | Subscriber id or registered callback function | -        |

### Remove by Function

```js|js
import $mediator from'wee-mediator';

const callback = functionsubscriber() {
    console.log('message published to subscriber 1');
};
$mediator.on('message', callback);
$mediator.on('message', () => {
    console.log('message published to subscriber 2');
});

$mediator.remove('message', callback);

$mediator.emit('message');

---

'message published to subscriber 2'
```

### Remove by Id

```js|js
import $mediator from'wee-mediator';

$mediator.on('message', () => {
    console.log('message published to subscriber 1');
});

const subscriber = $mediator.on('message', () => {
    console.log('message published to subscriber 2');
});

$mediator.remove('message', subscriber.id);

$mediator.emit('message');

---

'message published to subscriber 1'
```

### Remove all Subscribers

```js
import $mediator from'wee-mediator';

$mediator.on('message', () => {
    console.log('message published to subscriber 1');
});
$mediator.on('message', () => {
    console.log('message published to subscriber 2');
});

$mediator.remove('message'); // Removes all subscribers from this topic
```
