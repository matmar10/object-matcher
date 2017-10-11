# object-matcher

Match objects in mongoDb's fashion.

## Installation

```

npm install --save object-matcher
```

## Usage

Generalized:

```

var matcher = objectMatcher(matchingCriteria);
var booleanResult = matcher(someObject);
```

Example:

```

var objectMatcher = require('object-matcher');

var person1 = {
  name: {
    first: 'Simon',
    last: 'Fan'
  },
  age: 25,
  location: {
    lat: -23.6821604,
    lng: -46.8754915,
    city: 'Sao Paulo,
    country: Brazil'
  }
};

var isSimonFan = objectMatcher({
  'name.first': 'Simon',
  'name.last': 'Fan'
});

console.log(isSimonFan(person)); // -> true

var isWithinContinentalUSA = objectMatcher({

  // northmost USA: 49.384472, -95.153389
  // southmost USA: 25.118333, -81.086389  

  'location.lat': {
    $gte: 25.118333,
    $lte: 49.384472
  },
  'location.lng': {
    $gte: -81.086389,
    $lte: -95.153389
  }
});

console.log(isWithinContinentalUSA(person)); // -> false

```

Plain strings are treated as property names. Dots indicate sub-properties.

Example: `'name.first': 'Simon'` expects an object at property `name` and inside that object to contain a `first` property equaling the string `'Simon'`

## Operators

The following Mongo-style operators are supported

### Match Operators

#### $match

Verify if value supplied attends the expected. Behaves according to the type of expected.

If value is an array of values, returns true if ANY of the values matches the expected.

See [MongoDB $elemMatch](https://docs.mongodb.com/v3.2/reference/operator/query/elemMatch)

**Parameters:**

* _expected_ -  String | Number | RegExp
* _value_ - String | Number | Boolean | Array

**Returns**

_Boolean_ - True if matches, false if not.

### Range Operators

#### $lt

See [MongoDB $lt](https://docs.mongodb.com/v3.2/reference/operator/query/$lt)

#### $lte

See [MongoDB $lte](https://docs.mongodb.com/v3.2/reference/operator/query/$lte)

#### $gt

See [MongoDB $gt](https://docs.mongodb.com/v3.2/reference/operator/query/$gt)

#### $gte

See [MongoDB $gte](https://docs.mongodb.com/v3.2/reference/operator/query/$gte)

### Set Operators

#### $all

See [MongoDB $all](https://docs.mongodb.com/v3.2/reference/operator/query/all)

#### $nin

See [MongoDB $nin](https://docs.mongodb.com/v3.2/reference/operator/query/nin)

#### $in

See [MongoDB $in](https://docs.mongodb.com/v3.2/reference/operator/query/in)

#### $match

See [MongoDB $match](https://docs.mongodb.com/v3.2/reference/operator/query/match)

#### $matchSingle

See [MongoDB $matchSingle](https://docs.mongodb.com/v3.2/reference/operator/query/matchSingle)

### Boolean

These are not yet implemented. Contributions welcome :-)

#### $and

**UNIMPLEMENTED**

See [MongoDB $and](https://docs.mongodb.com/v3.2/reference/operator/query/and)

#### $e

**UNIMPLEMENTED**

See [MongoDB $e](https://docs.mongodb.com/v3.2/reference/operator/query/e)

#### $ne

**UNIMPLEMENTED**

See [MongoDB $ne](https://docs.mongodb.com/v3.2/reference/operator/query/ne)

#### $not

**UNIMPLEMENTED**

See [MongoDB $not](https://docs.mongodb.com/v3.2/reference/operator/query/not)

#### $or

**UNIMPLEMENTED**

See [MongoDB $or](https://docs.mongodb.com/v3.2/reference/operator/query/or)
