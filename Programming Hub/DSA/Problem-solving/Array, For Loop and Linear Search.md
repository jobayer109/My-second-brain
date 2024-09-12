1. **Write a for loop that prints 1 - 100**
```js
for (let i = 1; i <= 100; i++) {
  console.log(i);
}
```

---

2. **Write a for loop that sum from 1 - 100**
```js
let sum = 0;
for (let i = 1; i <= 100; i++) {
  sum += i;
}
console.log(sum);

```

---

3. **Write a function that finds an element from an array. If it exists, that returns true; otherwise, it is false. [12,3,4,12,46,9,8]**
```js
function findElement(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return true; // Element found
    }
  }
  return false; // Element not found
}

const array = [12, 3, 4, 12, 46, 9, 8];
const target = 46;

console.log(findElement(array, target)); // Output: true

```
---

4.  **Write a function that finds only even number sum from array [12,3,4,12,46,9,8]**
```js
function evenNumberSum(arr) {
  let sum = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) {
      sum += arr[i]; // Add only even numbers
    }
  }

  return sum;
}

const array = [12, 3, 4, 12, 46, 9, 8];
console.log(evenNumberSum(array)); // Output: 82

```
---

5. **Write a function that finds only odd number sum from array [12,3,4,12,46,9,8,9,7]**
```js
function oddNumberSum(arr) {
  let sum = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 !== 0) {
      sum += arr[i]; // Add only odd numbers
    }
  }

  return sum;
}

const array = [12, 3, 4, 12, 46, 9, 8, 9, 7];
console.log(oddNumberSum(array)); // Output: 28

```
---

6. **Write a function that finds if all elements are unique [12,3,4,12,46,9,8,9,7], If any elements exist more than one that returns false, otherwise true.**
```js
function areAllElementsUnique(arr) {
  let uniqueElements = new Set();

  for (let i = 0; i < arr.length; i++) {
    if (uniqueElements.has(arr[i])) {
      return false; // Duplicate found, return false
    }
    uniqueElements.add(arr[i]); // Add element to the set
  }

  return true; // All elements are unique
}

const array = [12, 3, 4, 12, 46, 9, 8, 9, 7];
console.log(areAllElementsUnique(array)); // Output: false

```

---
