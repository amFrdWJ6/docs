# Arrays

fixed size collection of homogenous elements stored in contiguous memory locations, therefore it's memory-efficient with constant-time access to elements by their index

## Methods

| Method | ECMAScript Version | Description |
|---|---|---|
| concat() | ES3 | Concatenates two or more arrays and returns a new array |
| copyWithin() | ES6 | Copies a sequence of elements within the array to another position |
| entries() | ES6 | Returns an iterator object that contains the key/value pairs for each index in the array |
| every() | ES5 | Checks if every element in the array satisfies a condition |
| fill() | ES6 | Fills all the elements of an array with a static value |
| filter() | ES5 | Creates a new array with all elements that pass the test implemented by the provided function |
| find() | ES6 | Returns the first element in the array that satisfies the provided testing function |
| findIndex() | ES6 | Returns the index of the first element in the array that satisfies the provided testing function |
| findLast | ES2023 | Returns the value of the last element in the array where predicate is true, and undefined otherwise |
| findLastIndex | ES2023 | Returns the index of the last element in the array where predicate is true, and -1 otherwise |
| flatMap() | ES2019 | Maps each element using a mapping function, then flattens the result into a new array |
| forEach() | ES5 | Executes a provided function once for each array element |
| includes() | ES2016 | Determines whether an array includes a certain element, returning true or false |
| indexOf() | ES5 | Returns the first index at which a given element can be found in the array, or -1 if it is not present |
| join() | ES3 | Joins all elements of an array into a string |
| keys() | ES6 | Returns an iterator that contains the keys for each index in the array |
| lastIndexOf() | ES5 | Returns the last index at which a given element can be found in the array, or -1 if it is not present |
| map() | ES5 | Creates a new array populated with the results of calling a provided function on every element in the array |
| pop() | ES3 | Removes the last element from an array and returns that element |
| push() | ES3 | Adds one or more elements to the end of an array and returns the new length of the array |
| reduce() | ES5 | Applies a function against an accumulator and each element in the array to reduce it to a single value |
| reduceRight() | ES5 | Applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value |
| reverse() | ES1 | Reverses the elements of an array in place |
| shift() | ES3 | Removes the first element from an array and returns that removed element |
| slice() | ES3 | Returns a shallow copy of a portion of an array into a new array object |
| some() | ES5 | Checks if at least one element in the array satisfies a condition |
| sort() | ES1 | Sorts the elements of an array in place and returns the sorted array |
| splice() | ES3 | Changes the contents of an array by removing or replacing existing elements and/or adding new elements |
| toLocaleString() | ES3 | Returns a string representing the elements of the array using the specified locale-specific conventions |
| toReversed() | ES2023 | Returns a copy of an array with its elements reversed |
| toSorted() | ES2023 | Returns a copy of an array with its elements sorted |
| toSpliced() | ES2023 | Copies an array and removes elements and, if necessary, inserts new elements in their place. Returns the copied array |
| toString() | ES3 | Returns a string representing the specified array and its elements |
| unshift() | ES3 | Adds one or more elements to the beginning of an array and returns the new length of the array |
| values() | ES6 | Returns an iterator that contains the values for each index in the array |
| with() | ES2021 | Copies an array, then overwrites the value at the provided index with the given value. If the index is negative, then it replaces from the end of the array |
| Array.from() | ES6 | Creates a new array from an array-like or iterable object |