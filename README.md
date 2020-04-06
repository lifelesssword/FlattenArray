// FlattenArray.js

function flattenArray (input) {
  
  if (Array.isArray(input)) {
    return input.reduce(
      function flattener (accumulator, value) {
        if (Array.isArray(value)) {
          
          return accumulator.concat(value.reduce(flattener, []))
       
          return accumulator.concat(value)
        }
      }
      , []
    )
  } else {
    throw new TypeError('Argument must be an array')
  }
}

module.exports = exports.default = flattenArray







// FlattenArray.test.js

const assert = require('assert')

const flattenArray = require('./flattenArray')

const tests = [
  {
    input: [[1,2,[3]],4],
    output: [1, 2, 3, 4]
  },
  {
    input: [],
    output: []
  },
  {
    input: ['a', 'b'],
    output: ['a', 'b']
  },
  {
    input: [1, [2, [3, [4, 5, [6, 7], 8], 9], 10, 11], 12],
    output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
  }
]


tests.forEach(({ input, output }) => {
  assert.deepEqual(flattenArray(input), output)
})

console.log(`run ${tests.length} tests`)
