# cutie-brief
It's just a set of async objects that can replace commonly used big compositions of async objects.

## example

Instead of writing this composition

```js
new ParsedJSON(
  new StringFromBuffer(
    new ResponseBody(
      new ResponseFromHttpsGetRequest(
        requestOptions
      )
    )
  )
).call()
```
we can just use following async object

```js
new JSONFromHttpsRequest(requestOptions).call()
```

And `JSONFromHttpsRequest` can be implemented in the following way:

```js
const { ParsedJSON } = require('@cuties/json')
const { StringFromBuffer } = require('@cuties/buffer')
const { ResponseFromHttpsGetRequest, ResponseBody } = require('@cuties/https')

class JSONFromHttpsRequest {
  constructor (requestOptions) {
    return new ParsedJSON(
      new StringFromBuffer(
        new ResponseBody(
          new ResponseFromHttpsGetRequest(
            requestOptions
          )
        )
      )
    )
  }
}
```

And that's it. That's so simple.
