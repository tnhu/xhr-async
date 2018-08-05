Modern await/async HTTP client library built on top of (axios)[https://github.com/axios/axios] inspired by golang's syntax.

## Install

```bash
npm i xhr-async
```

or

```bash
yarn add xhr-async
```

Then in your script:

```javascript
import xhr from 'xhr-async'
```

## API

```javascript
const {
  status,
  statusText,
  error,
  headers,
  response,
  request
} = await xhr.[get | post | delete | head | options | trace](url, options)
```

Most of the time, you'd probably need `status`, `error`, and `response` back from a request.

`options` is exactly the same as axios' [options](https://github.com/axios/axios#request-config).

xhr-async supports response alias, for example instead of:

```javascript
const { response: ip } = await xhr.get('https://httpbin.org/ip')
```

You can do:

```javascript
const { ip } = await xhr.get('https://httpbin.org/ip').as('ip')
```

### xhr.defaults

`xhr.defaults` is exactly the same as axios' [defaults](https://github.com/axios/axios#config-defaults). It is used to configure global configuration.

### Examples

#### GET

```javascript
const { response, status } = await xhr.get('https://httpbin.org/ip')
```

#### POST

```javascript
const {
  response,
  status
} = await xhr.post('https://httpbin.org/post', {
  data: {
    name: 'xhr-async',
    timestamp: new Date()
  }
})
```

### before/after hooks

Similar to axios' request and response interceptors, xhr-async support `before` and `after` hooks.

```javascript
xhr.before(({ url, params, headers = {}, data }) => {
  headers.Authorization = 'Bearer 1234567890'
})
```

```javascript
xhr.after(({ status, statusText, headers, response, error, request }) => {
  if (status === 401) {
    // redirect to login page
  }
})
```

### License

MIT