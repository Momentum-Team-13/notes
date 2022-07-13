# Working through Exercism's ETL problem

In class we worked through getting the first test to pass for the [ETL exercise](https://exercism.org/tracks/javascript/exercises/etl) on in the JavaScript track on Exercism.

## The task is to transform data from one structure to another

The first test:
```js
const old = { 1: ['A'] };
const expected = { a: 1 };
expect(transform(old)).toEqual(expected);
```

Here is the code we wrote to pass the first test.
```js
export const transform = (obj) => {
  const newObj = {} // this is what we'll build up to form the return value
  const newValue = Object.keys(obj)[0]
  let newKey = Object.values(obj)[0][0].toLowerCase()
  newObj[newKey] = parseInt(newValue)
  return newObj
}
```

## We wrote pseudo code for all the steps

- take in the input, which is an object that looks like `{ 1: ['A'] }`
- get the value from the object that's passed in
- get the key from the object that's passed in
- create a new object
- create a new key-value pair in the new object
  - use the value from the object (that is passed in) as the key in the new object (and make sure to lowercase it)
  - use the key from the object (that is passed in) as the value in the new object (and make sure that it is a number, not a string)
- return the new object

## 🔎 We had to look up a lot of syntax! We looked up:

- [how to get the values from an object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Object/values)
- [how to get the keys from an object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
- [how to turn a string into a number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- [how to lowercase a string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

## After all that we still had only passed the first test 😞

The other tests we need to pass include:

- translate a single score with multiple letters into the new format
- translate multiple scores with multiple letters into the new format
- translate a lot more multiple scores and multiple letters

We knew we were going to need a loop! But we didn't get to it in class.

This seems like a lot of work. We need to loop over BOTH the keys and the values. 🤔 Is there an easier way?

Check out this method! [`Object.entries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

This is going to let us access both keys and values at the same time.

```js
export const transform = (obj) => {
  let newObj = {}
  for (const [score, letters] of Object.entries(obj)) {
    for (const letter of letters) {
      newObj[letter.toLowerCase()] = parseInt(score)
    }
  }
  return newObj
}
```

Try running that code yourself and using console.log to inspect the values. This isn't the only way to do this -- and a nested loop is definitely hard to reason about and not super efficient. 🥴 But it gets us the output we want!
