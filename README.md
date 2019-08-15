ember-async-await-for-each
==============================================================================
<a href="https://shipshape.io/"><img src="http://i.imgur.com/KVqNjgO.png" alt="Ship Shape" width="100" height="100"/></a>

**[ember-async-await-for-each is built and maintained by Ship Shape. Contact us for Ember.js consulting, development, and training for your project](https://shipshape.io/ember-consulting/)**.

[![npm version](https://badge.fury.io/js/ember-async-await-for-each.svg)](http://badge.fury.io/js/ember-async-await-for-each)
![Download count all time](https://img.shields.io/npm/dt/ember-async-await-for-each.svg)
![npm](https://img.shields.io/npm/dm/ember-async-await-for-each.svg)
[![Ember Observer Score](http://emberobserver.com/badges/ember-async-await-for-each.svg)](http://emberobserver.com/addons/ember-async-await-for-each)
[![Build Status](https://travis-ci.org/shipshapecode/ember-async-await-for-each.svg)](https://travis-ci.org/shipshapecode/ember-async-await-for-each)
[![Code Climate](https://codeclimate.com/github/shipshapecode/ember-async-await-for-each/badges/gpa.svg)](https://codeclimate.com/github/shipshapecode/ember-async-await-for-each)
[![Test Coverage](https://codeclimate.com/github/shipshapecode/ember-async-await-for-each/badges/coverage.svg)](https://codeclimate.com/github/shipshapecode/ember-async-await-for-each/coverage)

`async/await` aware `forEach` for Ember. Concept taken from [this great article](https://codeburst.io/javascript-async-await-with-foreach-b6ba62bbf404)
on `async/await` in `forEach`.

Compatibility
------------------------------------------------------------------------------

* Ember.js v3.4 or above
* Ember CLI v2.13 or above
* Node.js v8 or above

Installation
------------------------------------------------------------------------------

```
ember install ember-async-await-for-each
```


Usage
------------------------------------------------------------------------------
First you will want to import `asyncForEach`

```js
import asyncForEach from 'ember-async-await-for-each';
```

You can then use it inside of any `async` functions and await its result.
An example of how you could use it to save addresses for a person model is below.

```js
const saveAddresses = async () => {
  await asyncForEach(person.get('addresses').toArray(), async (address) => {
    const address = await person.get('address');

    if (address.get('isDirty')) {
      return await address.save();
    }
  });
};

saveAddresses();
```

You can continue to wrap this in other `async` functions as well.

```js
const doOtherAsyncStuff = async () => {
  await saveAddresses();
  await otherFunction();
  // etc
};
```

### Serial vs parallel execution
`asyncForEach` resolves the callbacks in a serial fashion. This means that it waits until a callback is fully resolved before moving onto the next element in the list.

To launch all callbacks in parallel, you would have to do something like below instead:

```js
import { all } from 'rsvp';

const saveAddressesParallel = async () => {
  await all(person.get('addresses').toArray().map(async (address) => {
    const address = await person.get('address');

    if (address.get('isDirty')) {
      return await address.save();
    }
  }));
};
```

Contributing
------------------------------------------------------------------------------

See the [Contributing](CONTRIBUTING.md) guide for details.

License
------------------------------------------------------------------------------

This project is licensed under the [MIT License](LICENSE.md).
