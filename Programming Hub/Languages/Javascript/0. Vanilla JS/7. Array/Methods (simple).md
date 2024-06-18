## JavaScript Array Methods: `slice`, `splice`, `reverse`, এবং `join`

### 1. `slice()`

**বর্ণনা:**
`slice()` method একটি নতুন array object-এ একটি অংশের shallow copy ফেরত দেয়, যা `start` থেকে `end` (end অন্তর্ভুক্ত নয়) পর্যন্ত নির্বাচিত হয়। মূল array পরিবর্তন হয় না।

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
মৌলিক array পরিবর্তন না করেই একটি subarray বের করার জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
let subArray = numbers.slice(1, 3);
console.log(subArray); // [2, 3]
console.log(numbers); // [1, 2, 3, 4, 5]
```

### 2. `splice()`

**বর্ণনা:**
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
array-তে উপাদান insert, remove, বা replace করার জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
let removed = numbers.splice(2, 2, 6, 7);
console.log(numbers); // [1, 2, 6, 7, 5]
console.log(removed); // [3, 4]
```

### 3. `reverse()`

**বর্ণনা:**
`reverse()` method array-এর উপাদানগুলি উল্টানো হয়। প্রথম array উপাদানটি শেষ উপাদান হয়ে যায় এবং শেষ array উপাদানটি প্রথম উপাদান হয়ে যায়।

**Syntax:**
```javascript
array.reverse();
```

**Parameters:**
- None

**Mutability:**
- Mutable: মূল array পরিবর্তিত হয়।

**Use Case:**
array-এর উপাদানগুলির ক্রম উল্টানোর জন্য।
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.reverse();
console.log(numbers); // [5, 4, 3, 2, 1]
```

### 4. `join()`

**বর্ণনা:**
`join()` method একটি string-এ array-এর সমস্ত উপাদান যুক্ত করে এবং এই string ফেরত দেয়। আপনি একটি separator string উল্লেখ করতে পারেন যা প্রতিটি উপাদানকে আলাদা করবে।

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

### Summary

| Method   | Mutability        | Description                                                                 | Practical Use Case                                     |
|----------|-------------------|-----------------------------------------------------------------------------|--------------------------------------------------------|
| `slice`  | Immutable         | একটি নতুন array-তে একটি অংশের shallow copy ফেরত দেয়।                      | মৌলিক array পরিবর্তন না করেই subarrays বের করার জন্য।    |
| `splice` | Mutable           | উপাদানগুলো মুছে ফেলে, প্রতিস্থাপন করে, বা যোগ করে array পরিবর্তন করে।     | array-তে উপাদান insert, remove, বা replace করার জন্য।   |
| `reverse`| Mutable           | array-এর উপাদানগুলি উল্টায়।                                               | উপাদানগুলির ক্রম উল্টানোর জন্য।                         |
| `join`   | Immutable         | একটি string-এ array-এর সমস্ত উপাদান যুক্ত করে।                              | array-এর উপাদানগুলি থেকে একটি string তৈরির জন্য।        |

এই methods গুলি array গুলি ম্যানিপুলেট করার জন্য শক্তিশালী উপায় প্রদান করে, প্রতিটি এর নির্দিষ্ট ব্যবহার ক্ষেত্রে এবং মূল array-এ তাদের প্রভাব সহ।