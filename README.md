# AsyncAPI Converter

Convert [AsyncAPI](https://asyncapi.com) documents from version 1.x to 2.0.0-rc1.

## Installation

```sh
npm i asyncapi-converter
```

## Usage

### From CLI

Minimal example:

```sh
asyncapi-converter streetlights.yml

# Result:
asyncapi: '2.0.0-rc1'
id: 'urn:streetlights.api'
channels:
...
```

Specify the application id:

```sh
asyncapi-converter --id=urn:com.asynapi.streetlights streetlights.yml

# Result:
...
id: 'urn:com.asynapi.streetlights'
...
```

Save the result in a file:

```sh
asyncapi-converter streetlights.yml > streetlights2.yml
```

### As a package

```js
const { convert } = require('asyncapi-converter')

try {
  const asyncapi = fs.readFileSync('streetlights.yml', 'utf-8')
  console.log(convert(asyncapi, '2.0.0-rc1', {
      id: 'urn:com.asynapi.streetlights'
  }))
} catch (e) {
  console.error(e)
}
```

## Known missing features

* Streaming APIs (those using `stream` instead of `topics` or `events`) are coverted correctly but information about framing type and delimiter is missing until a [protocolInfo](https://github.com/asyncapi/extensions-catalog/issues/1) for that purpose is created.
