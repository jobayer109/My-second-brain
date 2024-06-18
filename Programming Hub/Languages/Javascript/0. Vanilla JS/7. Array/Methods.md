## Array Methods: `slice`, `splice`, `reverse`, & `join`
---

---

### 1. `slice()`
`slice()` method মূল array এর একটি  shallow copy তৈরী করে,  মূল array কে পরিবর্তন করেনা।

**Syntax:**
```javascript
array.slice(start, end);
```

**Parameters:**
- `start` (optional): নির্দিষ্ট অংশের শুরু index। যদি বাদ দেওয়া হয়, এটি ডিফল্টভাবে 0 হয়।
- `end` (optional): নির্দিষ্ট অংশের শেষ index (অন্তর্ভুক্ত নয়)। যদি বাদ দেওয়া হয়, এটি array-এর দৈর্ঘ্য পর্যন্ত হয়।

**Mutability:**
- Immutable: মূল array পরিবর্তন হয় না।

**Use Case:**
>মূল array পরিবর্তন না করেই একটি subarray বের করার জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
let subArray = numbers.slice(1, 3);
console.log(subArray); // [2, 3]
console.log(numbers); // [1, 2, 3, 4, 5]
```

---

### 2. `splice()`
`splice()` method array-এর উপাদানগুলি পরিবর্তন করে এবং/অথবা নতুন উপাদান যোগ করে।

**Syntax:**
```javascript
array.splice(start, deleteCount, item1, item2, ...);
```

**Parameters:**
- `start`: array পরিবর্তন শুরু করার index।
- `deleteCount` (optional): মুছে ফেলার উপাদান সংখ্যা। যদি 0 হয়, কোন উপাদান মুছে ফেলা হয় না।
- `item1, item2, ...` (optional): array-তে যোগ করার উপাদান। যদি বাদ দেওয়া হয়, কোন উপাদান যোগ করা হয় না।

**Mutability:**
- Mutable: মূল array পরিবর্তিত হয়।

**Use Case:**
>array-তে উপাদান insert, remove, বা replace করার জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
let removed = numbers.splice(2, 2, 6, 7);
console.log(numbers); // [1, 2, 6, 7, 5]
console.log(removed); // [3, 4]
```

---

### 3. `reverse()`
`reverse()` method array-এর উপাদানগুলি উল্টানো হয়। প্রথম array উপাদানটি শেষ উপাদান হয়ে যায় এবং শেষ array উপাদানটি প্রথম উপাদান হয়ে যায়।

**Syntax:**
```javascript
array.reverse();
```

**Parameters:**
- None; অর্থাৎ কোনো প্যারামিটার প্রয়োজন নেই।

**Mutability:**
- Mutable: মূল array পরিবর্তিত হয়।

**Use Case:**
>array-এর উপাদানগুলির ক্রম উল্টানোর জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.reverse();
console.log(numbers); // [5, 4, 3, 2, 1]
```

---

### 4. `join()`
`join()` method একটি string-এ array-এর সমস্ত উপাদানগুলিকে যুক্ত কর। একটি separator string উল্লেখ করা যেতে পারে; যাতে প্রতিটি উপাদানকে আলাদা করা যায়।

**Syntax:**
```javascript
array.join(separator);
```

**Parameters:**
- `separator` (optional): প্রতিটি উপাদানকে আলাদা করতে একটি string উল্লেখ করে। ডিফল্ট হল একটি কমা (",")।

**Mutability:**
- Immutable: মূল array পরিবর্তিত হয় না।

**Use Case:**
array-এর উপাদানগুলি থেকে একটি string তৈরির জন্য।
```javascript
let words = ["Hello", "world", "!"];
let sentence = words.join(" ");
console.log(sentence); // "Hello world !"
console.log(words); // ["Hello", "world", "!"]
```

---
