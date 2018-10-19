ember-async-await-for-each
==============================================================================

`async/await` aware `forEach` for Ember. Concept taken from [this great article](https://codeburst.io/javascript-async-await-with-foreach-b6ba62bbf404)
on `async/await` in `forEach`. 

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

License
------------------------------------------------------------------------------

This project is licensed under the [MIT License](LICENSE.md).
