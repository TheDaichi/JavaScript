# Array Methods

## Array.every()

The `every()` method is available on all Arrays. It is used to test whether all the items in an array pass a specified test. The test is performed by executing a function that you pass into the `every()` method for every item in the Array.

### Example

```javascript
const oldEnough = [21, 25, 23, 21, 22, 24];
const notOldEnough = [21, 25, 23, 21, 17, 24];

function is21OrOver(age) {
    return age >= 21;
}

console.log(oldEnough.every(is21OrOver)); // true
console.log(notOldEnough.every(is21OrOver)); // false
```

The above code will print `true` then `false` to the console. The reason for this is because all the ages in the `oldEnough` array are `>= 21`, however there is a 17 year old in the `notOldEnough` array. Notice that the `is21OrOver` function is passed directly into the `every()` method. In many cases you will end up creating an anonymous function on the fly. The code below shows how you could use an anonymous function to achieve the same results:

```javascript
const oldEnough = [21, 25, 23, 21, 22, 24];
const notOldEnough = [21, 25, 23, 21, 17, 24];

console.log(
    oldEnough.every((age) => {
        return age >= 21;
    })
); // true
console.log(
    notOldEnough.every((age) => {
        return age >= 21;
    })
); // false
```

In this case it makes more sense to move the check for `>= 21` into its own function in order to avoid duplicating code. However, sometimes you will only be using a function one time. In that case it is fine to create it as an anonymous function as demonstrated above.

### Parameters

There is only 1 parameter required for the `every()` method, the test function (e.g. the `is21OrOver` function above). However there are a few arguments passed into the test function when the `every()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `every()` method:

```js
arr.every(callback(element[, index[, array]]))
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `every()` method, and that function takes 3 arguments. Those arguments are as follows:

1. `currentValue`: The current item being processed in the array
2. `index`: The index of the current item being processed in the array
3. `array`: The array for which `every()` was called

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `index` and `array` are optional, but `element` is a required argument.

The return value for the `every()` method is a boolean.



## Array.filter()

The `filter()` method is available on all Arrays. It is used to create a new array with all the items that pass a test. The test is performed by executing a function that you pass into the `filter()` method for every item in the Array.

### Example

```
const nums = [1, 2, 3, 4, 5];

const evens = nums.filter((i) => {
    return i % 2 == 0;
});

console.log(nums); // [1, 2, 3, 4, 5]
console.log(evens); // [2,4]
```

The above code will print the items in the `nums` array and the filtered items in the `events` array.

### Parameters

There is only 1 parameter required for the `filter()` method, the test function. However there are a few arguments passed into the test function when the `filter()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `filter()` method:

```
arr.filter(callback(element[, index[, array]]))
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `filter()` method, and that function takes 3 arguments. Those arguments are as follows:

1. `element`: The current item being processed in the array
2. `index`: The index of the current item being processed in the array
3. `array`: The array for which `filter()` was called

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `index` and `array` are optional, but `element` is a required argument.

The return value for the `filter()` method is a new, filtered array.



## Array.forEach()

Executes a callback for each item in the array.

The forEach method can be used instead of a `for` loop. The code is easier to read and follow as it makes logical sense. You are running a callback function "for each" item in the array.

### Example

```
const nums = [1, 3, 5];

nums.forEach((num, index) => {
    console.log(`The number at index ${index} is ${num}`);
});

// Output:
// The number at index 0 is 1
// The number at index 1 is 3
// The number at index 2 is 5
```

The above code will print the commented lines to the console.

### Parameters

There is only 1 parameter required for the `forEach()` method, the test function. However there are a few arguments passed into the test function when the `forEach()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `forEach()` method:

```
arr.forEach(callback(element[, index[, array]]))
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `forEach()` method, and that function takes 3 arguments. Those arguments are as follows:

1. `element`: The current item being processed in the array
2. `index`: The index of the current item being processed in the array
3. `array`: The array for which `forEach()` was called

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `index` and `array` are optional, but `element` is a required argument.

There is no return value for the `forEach()`.



## Array.indexOf()

The `indexOf()` method is available on all Arrays. It is used to determine the first index at which a given element exists in an Array. Typically people use it to determine whether or not an Array contains an element, but it can also be used to determine if an Array has more than one instance of an element.

### Example

```javascript
const nums = [1, 2, 3, 2, 5];

const has2 = nums.indexOf(2);
const has2Twice = nums.indexOf(2, 2);
const has6 = nums.indexOf(6);

console.log(has2); // 1
console.log(has2Twice); // 3
console.log(has6); // -1
```

The above code will print `1`, `3`, and then `-1` when logging `has2`, `has2Twice`, and `has6` respectively. The reason for this is because `2` can be found both at index `1` and `3`, and `6` is missing from the Array. `indexOf()` always returns `-1` when the given element is not found in the Array. Note for `has2Twice` we passed in a second argument, indicating that we want to start searching for `2` starting at index `2`, thus skipping index `1` where there is already a `2`. `nums.indexOf(2, 1);` would return `1`, since there is a `2` at index `1`.

### Parameters

There is only 1 parameter required for the `indexOf()` method, the element to locate in the array.

```js
arr.indexOf(searchElement[, fromIndex])
```

What this means is that `arr` is an array that we are assuming was pre-defined. `searchElement` is a value that you would pass into the `indexOf()` method, and the `indexOf()` method will search for the first index of that value. The arguments for `indexOf()` are as follows:

1. `searchElement`: The Element to locate in the array.
2. `fromIndex`: An optional (default is 0) index to start the search at. If the index is greater than the length of the array, `-1` will be returned. If the index is a negative number, it's value will be taken as the offset from the end of the array. For example, in the code above `nums.indexOf(2, 2);` and `nums.indexOf(2, -2);` would produce the same results, since the index that is `-2` from the length of the array is actually index `3` where there is a `2`.

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `fromIndex` is optional, but `searchElement` is a required argument.

The return value for the `indexOf()` method is a non-negative number indicating the first index where the element is found, or `-1` indicating that the element is not found.

A common function that some people create is as follows:

```js
function contains(arr, element) {
    return arr.indexOf(element) !== -1;
}

console.log(contains([1, 2, 3], 2)); // true
```

The `contains()` function is now a shortcut to knowing whether or not an array contains an element.



## Array.lastIndexOf()

The `lastIndexOf()` method is available on all Arrays. It is used to determine the last index at which a given element exists in an Array. In other words, it operates exactly as `indexOf()` only it searches the array backwards, starting at `fromIndex`.

### Example

```javascript
const nums = [1, 2, 3, 2, 5];

const has2 = nums.lastIndexOf(2);
const has2Twice = nums.lastIndexOf(2, 2);
const has6 = nums.lastIndexOf(6);

console.log(has2); // 3
console.log(has2Twice); // 1
console.log(has6); // -1
```

The above code will print `3`, `1`, and then `-1` when logging `has2`, `has2Twice`, and `has6` respectively. The reason for this is because `2` can be found both at index `3` and `1`, and `6` is missing from the Array. `lastIndexOf()` always returns `-1` when the given element is not found in the Array. Note for `has2Twice` we passed in a second argument, indicating that we want to start searching for `2` starting at index `2` and working backwards, thus skipping index `3` where there is already a `2`. `nums.lastIndexOf(2, 3);` would return `3`, since there is a `2` at index `3`.

### Parameters

There is only 1 parameter required for the `lastIndexOf()` method, the element to locate in the array.

```js
arr.lastIndexOf(searchElement[, fromIndex])
```

What this means is that `arr` is an array that we are assuming was pre-defined. `searchElement` is a value that you would pass into the `lastIndexOf()` method, and the `lastIndexOf()` method will search for the last index of that value. The arguments for `lastIndexOf()` are as follows:

1. `searchElement`: The Element to locate in the array.
2. `fromIndex`: An optional (default is arr.length - 1) index to start the search at. If the index is greater than the length of the array, the entire array will be searched. If the index is a negative number, it's value will be taken as the offset from the end of the array. For example, in the code above `nums.lastIndexOf(2, 2);` and `nums.lastIndexOf(2, -3);` would produce the same results, since the index that is `-3` from the length of the array is actually index `2` and the last index searching backwards from index `2` where there is a `2` is at index `1`.

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `fromIndex` is optional, but `searchElement` is a required argument.

The return value for the `lastIndexOf()` method is a non-negative number indicating the last index where the element is found, or `-1` indicating that the element is not found.



## Array.map()

Calls a function for every element in an array and returns a new array with the return value of each function call.

### Example

```
const nums = [1, 3, 5, 7, 9];

const doubles = nums.map((num) => {
    return num * 2;
});

console.log(nums); // [1, 3, 5, 7, 9]
console.log(doubles); // [2, 6, 10, 14, 18]
```

The code above will first print the `nums` array to the console and then the new `doubles` array which contains the result of calling the function that returns `num * 2` on each item in the `nums` array.

### Parameters

There is only 1 parameter required for the `map()` method, the test function. However there are a few arguments passed into the test function when the `map()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `map()` method:

```
arr.map(callback(element[, index[, array]]))
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `map()` method, and that function takes 3 arguments. Those arguments are as follows:

1. `element`: The current item being processed in the array
2. `index`: The index of the current item being processed in the array
3. `array`: The array for which `map()` was called

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `index` and `array` are optional, but `element` is a required argument.

The return value for the `map()` method is a new array containing the returned values from calling the iterator function.



## Array.reduce()

The `reduce()` method is available on all Arrays. It is an incredibly useful method to understand and it pretty much does what it says. The purpose of the reduce method is to "reduce" an array into a single output value. It does this by executing a "reducer" function for each item in an array, and allowing you to keep an accumulator that serves as the final reduced value.

### Example

```javascript
const array = [1, 2, 3, 4, 5];

function sum(a, b) {
    return a + b;
}

console.log(array.reduce(sum)); // 15
console.log(array.reduce(sum, 5)); // 20
```

The above code will print `15` then `20` to the console. The reason for this is because the `reduce` method takes the value returned from the last call to the "reducer" (in this case the `sum` function) and passes it on to the next call to the "reducer" with the next item in the array. The second log of `20` demonstrates how you can pass an initial value for the reduce method to pass to the first iteration of the sum. If you do not pass an initial value, then the first call to the reducer function will include the first and second elements in the array as arguments.

Below is a more complicated example. Say you have a list of objects with a `firstName` and `lastName` property, and you want to reduce it to just a list of all the concatenated names:

```javascript
const users = [
    { firstName: 'John', lastName: 'Doe' },
    { firstName: 'Jane', lastName: 'Smith' },
    { firstName: 'Jack', lastName: 'Nimble' },
    { firstName: 'James', lastName: 'Trickington' },
];

console.log(
    users.reduce((names, user) => {
        return names.concat(`${user.firstName} ${user.lastName}`);
    }, [])
); // ["John Doe", "Jane Smith", "Jack Nimble", "James Trickington"]
```

In this case we initialize our `reduce` with an empty array `[]`, then in each reducer we extract the `firstName` and `lastName` values from each user and append them onto the `names` accumulator array.

### Parameters

There is only 1 parameter required for the `reduce()` method, the test function (e.g. the `sum` function above). However there are a few arguments passed into the test function when the `reduce()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `reduce()` method:

```js
arr.reduce(callback[, initialValue])
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `reduce()` method, and that function takes 3 arguments. Those arguments are as follows:

1. ```
   callback
   ```

   : Function to execute on each element in the array, taking four arguments:

   1. `accumulator`: The accumulator accumulates the callback's return values; it is the accumulated value previously returned in the last invocation of the callback, or `initialValue`, if supplied
   2. `currentValue`: The current item being processed in the array
   3. `index`: The index of the current item being processed in the array
   4. `array`: The array for which `reduce()` was called

2. `initialValue`: An optional value to use as the first argument to the first call of the callback. If no initial value is supplied, the first element in the array will be used. Calling reduce() on an empty array without an initial value is an error.

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `initialValue` is optional, but `callback` is a required argument.

The return value for the `reduce()` method is the final value of `accumulator` obtained by calling the reducer callback for every item in the array.



## Array.reduceRight()

The `reduceRight()` method is available on all Arrays. It is an incredibly useful method to understand and it pretty much does what it says. The purpose of the reduceRight method is to "reduce" an array into a single output value. It does this by executing a "reducer" function for each item in an array in reverse order, and allowing you to keep an accumulator that serves as the final reduced value.

**NOTE:** `reduceRight()` is the same thing as `reduce()` only the array is called in reverse (right-to-left) order. So it is essentially doing `array.reverse().reduce(...)`.

### Example

```javascript
const users = [
    { firstName: 'John', lastName: 'Doe' },
    { firstName: 'Jane', lastName: 'Smith' },
    { firstName: 'Jack', lastName: 'Nimble' },
    { firstName: 'James', lastName: 'Trickington' },
];

console.log(
    users.reduceRight((names, user) => {
        return names.concat(`${user.firstName} ${user.lastName}`);
    }, [])
); // ["James Trickington", "Jack Nimble", "Jane Smith", "John Doe"]
```

In this case we initialize our `reduceRight` with an empty array `[]`, then in each reducer we extract the `firstName` and `lastName` values from each user and append them onto the `names` accumulator array.

### Parameters

There is only 1 parameter required for the `reduceRight()` method, the test function (e.g. the anonymous function above). However there are a few arguments passed into the test function when the `reduceRight()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `reduceRight()` method:

```js
arr.reduceRight(callback[, initialValue])
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `reduceRight()` method, and that function takes 3 arguments. Those arguments are as follows:

1. ```
   callback
   ```

   : Function to execute on each element in the array, taking four arguments:

   1. `accumulator`: The accumulator accumulates the callback's return values; it is the accumulated value previously returned in the last invocation of the callback, or `initialValue`, if supplied
   2. `currentValue`: The current item being processed in the array
   3. `index`: The index of the current item being processed in the array
   4. `array`: The array for which `reduceRight()` was called

2. `initialValue`: An optional value to use as the first argument to the first call of the callback. If no initial value is supplied, the first element in the array will be used. Calling reduceRight() on an empty array without an initial value is an error.

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `initialValue` is optional, but `callback` is a required argument.

The return value for the `reduceRight()` method is the final value of `accumulator` obtained by calling the reducer callback for every item in the array.



## Array.some()

The `some()` method is available on all Arrays. It is used to test whether at least one of items in an array passes a specified test. The test is performed by executing a function that you pass into the `some()` method for the items in the Array.

### Example

```
const noEvens = [1, 3, 5];
const oneEven = [1, 3, 4, 5];

function isEven(num) {
    console.log(num);

    return num % 2 === 0;
}

console.log(noEvens.some(isEven)); // false
console.log(oneEven.some(isEven)); // true
```

The above code will print `false` then `true` to the console. The reason for this is because all the numbers in the `noEvens` array are odd, however there is an even number in the in the `oneEven` array. It will also print the following numbers in this order: `1`, `3`, `5`, `1`, `3`, `4`. It will not print the final `5` in the `oneEven` array. This is because the `some()` method only continues iteration until a truthy value is returned from the test function, after which it will break out. Notice that the `isEven` function is passed directly into the `some()` method. In many cases you will end up creating an anonymous function on the fly. The code below shows how you could use an anonymous function to achieve the same results:

```
const noEvens = [1, 3, 5];
const oneEven = [1, 3, 4, 5];

console.log(
    noEvens.some((age) => {
        console.log(num);

        return num % 2 === 0;
    })
); // false
console.log(
    oneEven.some((age) => {
        console.log(num);

        return num % 2 === 0;
    })
); // true
```

In this case it makes more sense to move the check for `% 2 === 0` into its own function in order to avoid duplicating code. However, sometimes you will only be using a function one time. In that case it is fine to create it as an anonymous function as demonstrated above.

### Parameters

There is only 1 parameter required for the `some()` method, the test function (e.g. the `isEven` function above). However there are a few arguments passed into the test function when the `some()` method is iterating through the items in the array. You may see the following syntax diagram explaining how to call the `some()` method:

```
arr.some(callback(element[, index[, array]]))
```

What this means is that `arr` is an array that we are assuming was pre-defined. `callback` is a function that you would pass into the `some()` method, and that function takes 3 arguments. Those arguments are as follows:

1. `element`: The current item being processed in the array
2. `index`: The index of the current item being processed in the array
3. `array`: The array for which `some()` was called

The brackets (`[` and `]`) encapsulate optional arguments. So in this case `index` and `array` are optional, but `element` is a required argument.

The return value for the `some()` method is a boolean.





