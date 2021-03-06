# smart-deep-sort

> Deep sort an object, no matter what the contents are.

[![CircleCI](https://circleci.com/gh/CollinearGroup/smart-deep-sort.svg?style=svg)](https://circleci.com/gh/CollinearGroup/smart-deep-sort)
[![Coverage Status](https://coveralls.io/repos/github/CollinearGroup/smart-deep-sort/badge.svg?branch=master)](https://coveralls.io/github/CollinearGroup/smart-deep-sort?branch=master)

## Install

```
npm install smart-deep-sort
```

## Usage

```js
var sort = require("smart-deep-sort")

var mixedTypes = {
  primativeInt: 2,
  primativeString: "1",
  mixedArray: [
    {
      nestedObjName: "Nestle",
      abilities: ["rock", "and", "roll"]
    },
    [4, 1, 2, "two", "twenty-thousand"],
    "basicString"
  ]
}

var sortedMixedTypes = {
  mixedArray: [
    [1, 2, 4, "twenty-thousand", "two"],
    {
      abilities: ["and", "rock", "roll"],
      nestedObjName: "Nestle"
    },
    "basicString"
  ],
  primativeInt: 2,
  primativeString: "1"
}

var ret = sort(mixedTypes)
console.log(JSON.stringify(ret) === JSON.stringify(sortedMixedTypes))
```

## The Rules

- Objects fields are deep sorted by key using [deep-sort-object](https://www.npmjs.com/package/deep-sort-object)
  - keys at all levels are sorted using default string Unicode code sort order
- Arrays elements are sorted by type, ordered on the constructor name. *A*rrays come first then *B*ooleans, etc.
  - Nested objects are sorted by using [sorty](https://www.npmjs.com/package/sorty) to order them by keys and values.
  - All other nested object types are sorted by their contents using [array-sort](https://www.npmjs.com/package/array-sort)

## Limitations

- Cannot handle objects with undefined keys, _they will probably be dropped from the resulting object_.
- Not optimized, I don't recommend using this as part of stream processing.
- Does not handle Date types. The default string representation of the date will be used in comparisons.
