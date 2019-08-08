# simple-zstd

[![Build Status](https://travis-ci.org/Stieneee/simple-zstd.svg?branch=master)](https://travis-ci.org/Stieneee/simple-zstd)
[![Package Size Size](https://badgen.net/badge/packagephobia/install/simple-zstd)](https://packagephobia.now.sh/result?p=simple-zstd)
[![License](https://badgen.net/badge/license/MIT/blue)](https://choosealicense.com/licenses/mit/)

Node.js interface to system installed zstandard (zstd).

## Why Another ZSTD Package

Other packages were either using out-of-date ZSTD versions or depended on native C bindings that required a compilation step during installation.
A package was needed that would cleanly work with [pkg](https://www.npmjs.com/package/pkg).

## Dependencies

ZSTD

Example:

`sudo apt install zstd`

## Installation

`npm i simple-zstd`

## Usage

simple-zstd exposes a stream interfaces for compression and decompression.

```javascript
const fs = require('fs');
const {ZSTDCompress, ZSTDDecompress} = require('zstd');

// ZSTDCompress(compressionLevel, streamOptions)
// ZSTDDecompress(streamOptions)

fs.createReadStream('example.txt')
  .pipe(ZSTDCompress(3))
  .pipe(ZSTDDecompress())
  .pipe(fs.createWriteStream('example_copy.txt'))
  .on('error', (err) => {
    //..
  })
  .on('finish', () => {
    console.log('Copy Complete!');
  })

  // -> Copy Complete
```

### Decompress Maybe

A maybe variant of decompress will pass-through a non-zst stream while decompressing a zst stream.

```javascript
const fs = require('fs');
const {ZSTDDecompressMaybe} = require('zstd');

// ZSTDDecompressMaybe(streamOptions)

fs.createReadStream('example.txt')
  // .pipe(ZSTDCompress(3))
  .pipe(ZSTDDecompressMaybe())
  .pipe(fs.createWriteStream('example_copy.txt'))
  .on('error', (err) => {
    //..
  })
  .on('finish', () => {
    console.log('Copy Complete!');
  })

  // -> Copy Complete
```

## Contributing

Pull requests are welcome.
