1. `What are the limitations of React?`
	- এটি শুধু ইউজার ইন্টারফেস তৈরির জন্য ..... অন্য কাজের জন্য অন্যান্য লাইব্রেরি লাগে।
	- Development a onek external packages and libraries install korte hoy.
	- Natively SEO friendly na. 
2. `What are the differences between controlled and uncontrolled components?`
	- কন্ট্রোলড কম্পোনেন্ট হল যে কম্পোনেন্টের স্টেট রিঅ্যাক্ট ম্যানেজ করে অর্থাৎ কোনো ইনপুটের ভ্যালু বা পরিবর্তন রিঅ্যাক্টের স্টেটের মাধ্যমে নিয়ন্ত্রিত হয়। আর আনকন্ট্রোলড কম্পোনেন্ট হল যেখানে ইনপুট এলিমেন্টের ভ্যালু সরাসরি ডম দ্বারা নিয়ন্ত্রিত হয় রিঅ্যাক্ট সরাসরি সেটা ম্যানেজ করে না। সহজ কথায় কন্ট্রোলড কম্পোনেন্টে রিঅ্যাক্ট সবকিছু নিয়ন্ত্রণ করে আর আনকন্ট্রোলডে ডম নিয়ন্ত্রণ করে।
	```js
import React, { useRef } from 'react';

function FormValidation() {
  const inputValue = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Input value: ${inputValue.current.value}`);
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input type="text" ref={inputValue} />
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}

export default FormValidation;

```

3. Why do React Hooks make use of refs?
	- কিছু নির্দিষ্ট ক্ষেত্রে 'useRef' খুব উপকারী যেমন ডম এলিমেন্ট-এ সরাসরি কিছু পরিবর্তন করতে কোনও ভ্যালু ধরে রাখতে যেটা রেন্ডারের সময় পরিবর্তন হবে না আর কম্পোনেন্টের লাইফসাইকেল-এর মধ্যে ভ্যালু ট্র্যাক করতে
	- ইনপুট ফিল্ডের ফোকাস ধরে রাখতে 
	- অ্যানিমেশন কন্ট্রোল করতে 'useRef' খুবই কাজে লাগে 
	- এছাড়া আরও কিছু ক্ষেত্রে এটা ব্যবহার করা যায় যেমন মিডিয়া প্লেব্যাক কন্ট্রোল করতে বা কোনও ইন্টারভাল আইডি সেভ করতে

4. `Custom hooks`
	- কাস্টম হুকস হলো নিজের বানানো ফাংশন যেগুলো রিঅ্যাক্ট-এর হুকস-এর লজিক ব্যবহার করতে পারে আপনি নিজের প্রয়োজন মতো হুকস তৈরি করতে পারেন এবং সেই লজিক গুলোকে আলাদা কম্পোনেন্টে শেয়ার করতে পারেন এটা কোডকে আরও রিইউজেবল এবং অর্গানাইজড করে তোলে
	- উদাহরণ: 'useFormInput' ফর্মের ইনপুট গুলো ম্যানেজ করতে 'useLocalStorage' লোকাল স্টোরেজে ডেটা সেভ আর রিট্রিভ করতে 'useFetch' এপিআই কল করতে 'useWindowSize' উইন্ডোর সাইজ ট্র্যাক করতে আর 'useDebounce' ইনপুট ভ্যালু ডিবাউন্স করতে
5. `What are the lifecycle methods of React?`
	- React এর লাইফ সাইকেল মেথডগুলোকে প্রধানত তিনটা ভাগে ভাগ করা যায়: মাউন্টিং, আপডেটিং আর আনমাউন্টিং। মাউন্টিং স্টেজে কম্পোনেন্ট প্রথমবার তৈরি হয়ে DOM-এ অ্যাড হয়। এখানে কম্পোনেন্ট ডিড মাউন্ট মেথডটা রান হয়, যেখানে আপনি ইনিশিয়াল ডেটা লোড করার মতো কাজ করতে পারেন। এরপর আপডেটিং স্টেজে কম্পোনেন্ট যখন স্টেট বা প্রপ্স চেঞ্জ হয় তখন রি-রেন্ডার করে। এখানে কম্পোনেন্ট ডিড আপডেট মেথডটা কল হয়, যেখানে আপনি আপডেট হওয়ার কাজ করতে পারেন। আর আনমাউন্টিং স্টেজে কম্পোনেন্ট যখন DOM থেকে রিমুভ হয়, তখন কম্পোনেন্ট উইল আনমাউন্ট কল হয়। এখানে আপনি ক্লিনিং আপ টাস্ক, যেমন নেটওয়ার্ক রিকোয়েস্ট ক্যানসেল করা বা ইভেন্ট লিসনার সরানো-এসব করতে পারেন।
6. `কি কি কারণে রি-রেন্ডারিং হয় ?`
	- React কম্পোনেন্টগুলো তখনই রি-রেন্ডার হয়, যখন তাদের স্টেট বা প্রপ্স চেঞ্জ হয়। কিন্তু অনেক সময় অপ্রয়োজনীয় রি-রেন্ডারিং হয়, যেমন প্যারেন্ট কম্পোনেন্ট রি-রেন্ডার হলে, তার সব চাইল্ড কম্পোনেন্টও রি-রেন্ডার হতে পারে, এমনকি যদি তাদের প্রপ্স চেঞ্জ না হয় তবুও। এছাড়াও, স্টেটের অপ্রয়োজনীয় আপডেট, বা মেমোইজেশন টেকনিক ইউজ না করলে, রি-রেন্ডারিং সমস্যা বাড়ে। মেমোইজেশন ইউজ করলে রিয়াক্ট চেক করে যে কম্পোনেন্টের প্রপ্স বা স্টেট আগের মতো আছে কিনা, যদি সেম থাকে তাহলে নতুন করে রেন্ডার করে না।
	- 'useMemo' আর 'useCallback' মেমোইজেশন টেকনিক হিসেবে খুব ভালো। 'useMemo' ইউজ করে আপনি এক্সপেনসিভ ক্যালকুলেশন মেমোইজ করতে পারেন, যাতে কম্পোনেন্ট রি-রেন্ডার হলেও সেটা বারবার ক্যালকুলেট না হয়। আর 'useCallback' ইউজ করে আপনি ফাংশন গুলোকে মেমোইজ করতে পারেন, যাতে প্যারেন্ট কম্পোনেন্ট রি-রেন্ডার হলেও, সেই ফাংশনগুলো নতুন করে ক্রিয়েট না হয়। এগুলো ইউজ করলে অপ্রয়োজনীয় রি-রেন্ডারিং অনেক কমে যায়।
- `7. Strict Mode.`
	- স্ট্রিক্ট মোড আনসেফ লাইফ সাইকেল মেথডগুলো চেক করে, যেমন 'componentWillMount' বা 'componentWillUpdate'। এছাড়াও, লিগেসি ফিচার ব্যবহার হচ্ছে কিনা সেটাও দেখে, যেমন পুরনো কনটেক্সট API ব্যবহার। যদি এই ধরনের কিছু পায়, তাহলে ডেভেলপমেন্টের সময় কনসোলে ওয়ার্নিং দেখায়, যাতে আপনি সমস্যাগুলো ফিক্স করতে পারেন এবং কোডকে ফিউচার-প্রুফ করতে পারেন। এটা বিশেষ করে নতুন ফিচার বা আপডেটের সময় খুব হেল্পফুল।
	- componentWillMount' এবং 'componentWillUpdate' মেথডগুলোকে আনসেফ বলা হয় কারণ এই মেথডগুলো রি-রেন্ডারিং-এর আগে কল হয় এবং প্রপ্স বা স্টেট আপডেট করার কারণে আনএক্সপেক্টেড বিহেভিয়ার তৈরি করতে পারে। নতুন রিয়াক্ট ভার্সনগুলোতে এই মেথডগুলো ডুপ্লিকেট টাইম কল হতে পারে, যা পারফরম্যান্স ইস্যু তৈরি করে এবং কোডকে কনফিউজিং বানায়। এজন্য রিয়াক্ট টিম রেকমেন্ড করে যে এই মেথডগুলোর পরিবর্তে 'componentDidMount', 'componentDidUpdate' বা অন্যান্য নতুন মেথড ইউজ করতে।
- `What is React ?`
	- রিয়াক্ট হচ্ছে একটা ওপেন সোর্স জাভাস্ক্রিপ্ট লাইব্রেরি যেটা কম্পোনেন্ট-বেসড আর্কিটেকচার ফলো করে ইউজার ইন্টারফেস তৈরি করার জন্য। এটা কম্পোনেন্টগুলোকে রিইউজেবল বানায় এবং ডেটা চেঞ্জ হলে শুধুমাত্র দরকারি কম্পোনেন্টগুলোকেই আপডেট করে, যার ফলে অ্যাপ্লিকেশনের পারফর্মেন্স বাড়ে। ekhetre vertual DOM role play kore.
- `React 18.2.0 er update gulo ki ki ?`
	- d
- `Explain the building blocks of React.****
	- ****Components:**** These are reusable blocks of code that return [HTML](https://www.geeksforgeeks.org/html-tutorial/).
	- ****JSX:**** It stands for JavaScript and XML and allows you to write HTML in [React](https://www.geeksforgeeks.org/reactjs-introduction/).
	- ****Props and State:**** props are like function parameters and State is similar to variables.
	- ****Context:**** This allows data to be passed through components as props in a hierarchy.
	- ****Virtual DOM:**** It is a lightweight copy of the actual DOM which makes DOM manipulation easier.
- `What is real DOM?`
	- sfs
- `How do browsers read JSX?****
    - In general, browsers are not capable of reading [JSX](https://www.geeksforgeeks.org/reactjs-jsx-introduction/) and only can read pure JavaScript. The web browsers read JSX with the help of a transpiler. Transpilers are used to convert JSX into JavaScript. The transpiler used is called [Babel](https://www.geeksforgeeks.org/what-is-babel/).
- `One-way and Reactive data binding`
	- ওয়ান-ওয়ে ডেটা বাইন্ডিং ব্যবহার করা হয় যখন ডেটা থেকে UI-এর দিকে পরিবর্তন দরকার কিন্তু UI থেকে ডেটাতে পরিবর্তন করার দরকার নেই....যেমন ধরো একটা ওয়েবসাইটে শুধু ডেটা প্রদর্শন করা হচ্ছে সেখানে ব্যবহারকারীর পরিবর্তনের প্রয়োজন নেই শুধু মাত্র ডেটা UI-তে প্রদর্শিত হবে
	- রিয়েকটিভ ডেটা বাইন্ডিং-এর ক্ষেত্রে ডেটা এবং UI উভয়দিকেই পরিবর্তন হতে পারে ডেটাবেসে পরিবর্তন হলে UI আপডেট হয় আবার UI-তে পরিবর্তন হলে ডেটাবেসেও পরিবর্তন হতে পারে
- `What is the role of shouldComponentUpdate() in React?
    - [shouldComponentUpdate()](https://www.geeksforgeeks.org/reactjs-shouldcomponentupdate-method/) is a lifecycle method that allows you to control whether a component should re-render when it receives new props or state. If it returns false, React will skip the re-render process for that component.
- `DangeriouslySetInnerHTML`
	- n
- `what is Javascript ?`
	- জাভাস্ক্রিপ্ট হল একটা ডাইনামিক প্রোগ্রামিং ল্যাঙ্গুয়েজ যা মূলত ওয়েব পেজগুলোকে ইন্টারঅ্যাকটিভ করতে ব্যবহৃত হয় এটা ব্রাউজারকে রিয়াল-টাইমে কন্টেন্ট চেঞ্জ করার ফর্ম ভ্যালিডেট করার আর অন্যান্য ইন্টারেক্টিভ ফিচার যোগ করার অনুমতি দেয় সার্ভার-সাইড ডেভেলপমেন্ট, মোবাইল অ্যাপ ডেভেলপমেন্ট এবং গেম ডেভেলপমেন্টেও এটা ব্যবহার করা হয় এক কথায় ওয়েবকে ডাইনামিক আর ইউজার-ফ্রেন্ডলি করার জন্য জাভাস্ক্রিপ্ট খুবই গুরুত্বপূর্ণ
- `Arrow Function `
	- অ্যারো ফাংশন এমন একটা ফাংশন যাকে একটা ভেরিয়েবলের মধ্যে রাখা যায় এবং ভেরিয়েবলের নাম ইউজ করে কল করা যায় এটা লেখার একটা সংক্ষিপ্ত পদ্ধতি আর এটা নরমাল ফাংশনের চেয়ে কিছু আলাদাভাবে কাজ করে যেমন এটার নিজের কোন 'this' কনটেক্সট থাকে
	- অ্যারো ফাংশন তার নিজের কোন 'this' কনটেক্সট ইউজ করে না এটা তার প্যারেন্ট স্কোপের 'this' কনটেক্সট ব্যবহার করে এটাকে বলা হয় লেক্সিক্যাল 'this' বাইন্ডিং' এর ফলে ফাংশনের ভেতরে 'this' সবসময় প্রেডিক্টেবল থাকে