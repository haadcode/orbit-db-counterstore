# orbit-db-counterstore

[![npm version](https://badge.fury.io/js/orbit-db-counterstore.svg)](https://badge.fury.io/js/orbit-db-counterstore)

A simple counters database. Useful for example counting events separate from data.

Used in [orbit-db](https://github.com/haadcode/orbit-db).

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [API](#api)
- [Contributing](#contributing)
- [License](#license)

## Install
```
npm install orbit-db ipfs
```

## Usage

First, create an instance of OrbitDB:

```javascript
const IPFS = require('ipfs')
const OrbitDB = require('orbit-db')

const ipfs = new IPFS()
const orbitdb = new OrbitDB(ipfs)
```

Get a log database and add an entry to it:

```javascript
const counter = orbitdb.counter('visitors')
counter.inc()
console.log(counter.value)
// 1
counter.inc(4)
console.log(counter.value)
// 5
```

Later, when the database contains data, load the history and query when ready:

```javascript
const counter = orbitdb.counter('visitors')
counter.events.on('ready', () => {
  counter.inc()
  console.log(counter.value)
  // 6
})
```

See [example/index.html]() for a detailed example. Note that to run this example, you need to have a local [IPFS daemon](https://dist.ipfs.io/go-ipfs/floodsub-2) [running](https://ipfs.io/docs/getting-started/) at port 5001.

## API

### counter(name)

  Package: 
  [orbit-db-counter](https://github.com/haadcode/orbit-db-counter)

  ```javascript
  const counter = orbitdb.counter('song_123.play_count')
  ```

  - **value**
    ```javascript
    counter.value // 0
    ```

  - **inc([value])**
    ```javascript
    counter.inc()
    counter.value // 1
    counter.inc(7)
    counter.value // 8
    counter.inc(-2)
    counter.value // 8
    ```
    
  - **events**

    ```javascript
    db.events.on('data', (dbname, event) => ... )
    ```

    See [Events](https://github.com/haadcode/orbit-db-store#events) for full description

## Contributing

See [orbit-db's contributing guideline](https://github.com/haadcode/orbit-db#contributing).

## License

[MIT](LICENSE) ©️ 2016 Haadcode
