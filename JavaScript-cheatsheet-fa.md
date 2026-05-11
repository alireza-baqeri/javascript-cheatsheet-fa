# مرور مفاهیم جاوااسکریپت

## 1. مفاهیم پایه

### متغیرها و انواع داده
```javascript
//modern variables - متغیر های مدرن
const name = "Ali";             // ثابت (تغییرناپذیر)
let age = 30;                   // متغیر (قابل تغییر)
var oldStyle = "legacy";        // قدیمی (استفاده نشود)

// انواع داده اولیه (Primitive)
const string = "text";          // رشته
const number = 42;              // عدد
const boolean = true;           // منطقی
const nullValue = null;         // خالی
const undefinedValue = undefined; // تعریف نشده
const symbol = Symbol("id");    // نماد
const bigInt = 9007199254740991n; // اعداد بزرگ
```

### انواع داده مرجع (Reference)
```javascript
//Object - شئ
const object = {
  name: "Ali",
  age: 30
};

// آرایه (Array)
const array = [1, 2, 3, 4, 5];

// تابع (Function)
const func = function() {
  return "سلام";
};

// Date - تاریخ
const date = new Date();

// RegExp
const regex = /pattern/g;
```

### ساختارهای کنترلی
```javascript
// Conditional - شرطی
if (condition) {
  // کد
} else if (otherCondition) {
  // کد
} else {
  // کد
}

// switch
switch (value) {
  case 1:
    // کد
    break;
  default:
    // کد
}

// Lopps - حلقه ها
for (let i = 0; i < 5; i++) { }
while (condition) { }
do { } while (condition);
for (const item of array) { }  // برای آرایه‌ها
for (const key in object) { }  // برای شیء‌ها
```

## 2. توابع و Scope

### تعریف توابع
```javascript
//standard defention of a function - تعریف استاندارد یک تابع
function sayHello(name) {
  return `سلام ${name}`;
}

// Arrow Function
const sayHi = (name) => `سلام ${name}`;

// funcitons as a variable -  تابع ها به عنوان متغیر
const greet = function(name) {
  return `سلام ${name}`;
};

// IIFE (تابع فوراً اجرا شونده)
(function() {
  console.log("فوراً اجرا شدم");
})();
```

### Scope و Closure
```javascript
// محدوده ی متغیر - Scope
var globalVar = "جهانی";      // سطح جهانی
function test() {
  var localVar = "محلی";      // سطح تابع
  if (true) {
    let blockVar = "بلاکی";   // سطح بلاک
    const constVar = "ثابت";  // سطح بلاک
  }
}

// Closure (بستار)
function createCounter() {
  let count = 0;
  return function() {
    return ++count;
  };
}
const counter = createCounter();
counter(); // 1
counter(); // 2
```

## 3. اشیاء و OOP

### اشیاء و خصوصیات
```javascript
// تعریف شیء
const person = {
  name: "Ali",
  age: 30,
  greet() {
    return `سلام، من ${this.name} هستم`;
  }
};

// دسترسی به خصوصیات
person.name;           // نقطه
person["name"];        // براکت

// Object Destructuring
const { name, age } = person;

// Spread Operator
const newPerson = { ...person, job: "Developer" };
```

### کلاس‌ها و وراثت
```javascript
// تعریف کلاس
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  greet() {
    return `سلام، من ${this.name} هستم`;
  }
  
  // متد استاتیک
  static createAnonymous() {
    return new Person("ناشناس", 0);
  }
}

// وراثت
class Employee extends Person {
  constructor(name, age, job) {
    super(name, age);
    this.job = job;
  }
  
  work() {
    return `${this.name} در حال کار به‌عنوان ${this.job}`;
  }
}
```

### Prototype و This
```javascript
// Prototype (پیش از ES6)
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  return `${this.name} صدا می‌کند`;
};

// This و Context
function showThis() {
  console.log(this);
}

showThis();                // window/global
person.showThis = showThis;
person.showThis();         // person object

// Binding this
const boundFunc = showThis.bind(person);
const arrowFunc = () => { console.log(this); }; // lexical this
```

## 4. آرایه‌ها و کار با داده

### متودهای آرایه
```javascript
const arr = [1, 2, 3, 4, 5];

// Iteration
arr.forEach((item) => console.log(item));
const doubled = arr.map((item) => item * 2);
const filtered = arr.filter((item) => item > 2);
const sum = arr.reduce((total, item) => total + item, 0);

// جستجو
const found = arr.find((item) => item > 3);
const index = arr.findIndex((item) => item === 3);
const includes = arr.includes(3);

// ویرایش آرایه
arr.push(6);                // اضافه به انتها
arr.pop();                  // حذف از انتها
arr.unshift(0);             // اضافه به ابتدا
arr.shift();                // حذف از ابتدا
arr.splice(1, 2, "a", "b"); // حذف/اضافه در موقعیت خاص
```

### متودهای String
```javascript
const str = "Hello World";

str.length;               // طول رشته
str.indexOf("World");     // پیدا کردن موقعیت
str.includes("Hello");    // چک وجود
str.replace("Hello", "Hi");  // جایگزینی
str.split(" ");           // تقسیم به آرایه
str.toLowerCase();        // تبدیل به حروف کوچک
str.toUpperCase();        // تبدیل به حروف بزرگ
str.trim();               // حذف فضاهای خالی
str.substring(0, 5);      // استخراج بخشی از رشته
```

## 5. ناهمگامی (Asynchronous)

### Callback
```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("داده");
  }, 1000);
}

fetchData((data) => {
  console.log(data);
});
```

### Promise
```javascript
const promise = new Promise((resolve, reject) => {
  if (success) {
    resolve("موفق");
  } else {
    reject("خطا");
  }
});

promise
  .then(data => console.log(data))
  .catch(error => console.error(error))
  .finally(() => console.log("پایان"));

// Promise.all - همه را همزمان انجام بده
Promise.all([promise1, promise2])
  .then(results => console.log(results));

// Promise.race - اولین را برگردان
Promise.race([promise1, promise2])
  .then(firstResult => console.log(firstResult));
```

### Async/Await
```javascript
async function fetchUser() {
  try {
    const response = await fetch('/api/user');
    const user = await response.json();
    return user;
  } catch (error) {
    console.error(error);
  }
}

// فراخوانی
fetchUser().then(user => console.log(user));
```

## 6. رویدادها (Events)

### گوش دادن به رویداد
```javascript
// اضافه کردن Event Listener
element.addEventListener("click", function(event) {
  console.log("کلیک شد");
});

// حذف Event Listener
element.removeEventListener("click", handlerFunction);

// Event Object
element.addEventListener("click", function(event) {
  event.preventDefault();  // جلوگیری از رفتار پیش‌فرض
  event.stopPropagation(); // توقف انتشار
  console.log(event.target); // عنصری که رویداد اتفاق افتاده
});
```

### Event Bubbling و Capturing
```javascript
// Event Bubbling - از پایین به بالا
/*
<div id="parent">
  <button id="child">کلیک</button>
</div>
*/

// Bubbling (پیش‌فرض): child -> parent
parent.addEventListener("click", () => console.log("parent"));
child.addEventListener("click", () => console.log("child"));

// Capturing: parent -> child
parent.addEventListener("click", () => console.log("parent"), true);
child.addEventListener("click", () => console.log("child"), true);
```

### Event Delegation
```javascript
// استفاده از رویداد والد برای فرزندان
document.getElementById("parent").addEventListener("click", function(e) {
  if (e.target.tagName === "BUTTON") {
    console.log("دکمه کلیک شد");
  }
});
```

## 7. مدیریت خطا

### Try/Catch
```javascript
try {
  // کدی که ممکن است خطا دهد
  throw new Error("خطای سفارشی");
} catch (error) {
  console.error(error.message);
} finally {
  // همیشه اجرا می‌شود
}
```

### Error Types
```javascript
// انواع خطاها
new Error("خطای عمومی");
new SyntaxError("خطای نحوی");
new TypeError("خطای نوع");
new ReferenceError("خطای ارجاع");
new RangeError("خطای محدوده");

// خطای سفارشی
class CustomError extends Error {
  constructor(message) {
    super(message);
    this.name = "CustomError";
  }
}
```

## 8. کارکردهای پیشرفته

### Debounce و Throttle
```javascript
// Debounce - اجرای تابع بعد از مدت زمان مشخص از آخرین فراخوانی
function debounce(func, delay) {
  let timeout;
  return function(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}

// Throttle - اجرا حداکثر یکبار در بازه زمانی
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// استفاده
const debouncedSearch = debounce(search, 300);
window.addEventListener("resize", throttle(handleResize, 100));
```

### Memoization
```javascript
// ذخیره نتایج تابع برای فراخوانی‌های بعدی
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key] === undefined) {
      cache[key] = fn.apply(this, args);
    }
    return cache[key];
  };
}

// استفاده
const memoizedFib = memoize(function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
});
```

### Proxy و Reflect
```javascript
// Proxy - میانجی برای دسترسی به شیء
const handler = {
  get(target, prop) {
    console.log(`دریافت ${prop}`);
    return target[prop];
  },
  set(target, prop, value) {
    console.log(`تنظیم ${prop} به ${value}`);
    target[prop] = value;
    return true;
  }
};

const user = new Proxy({name: "Ali"}, handler);
user.name;  // "دریافت name"
user.age = 30; // "تنظیم age به 30"

// Reflect - عملیات روی اشیاء
Reflect.get(user, "name");
Reflect.has(user, "age");
Reflect.defineProperty(user, "job", { value: "Developer" });
```

### Generators و Iterators
```javascript
// Generator - تابعی که می‌تواند مکث و ادامه دهد
function* countGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const counter = countGenerator();
counter.next(); // { value: 1, done: false }
counter.next(); // { value: 2, done: false }
counter.next(); // { value: 3, done: false }
counter.next(); // { value: undefined, done: true }

// Iterator - شیئی که با .next() مقادیر را تولید می‌کند
const customIterator = {
  index: 0,
  next() {
    if (this.index < 3) {
      return { value: this.index++, done: false };
    }
    return { value: undefined, done: true };
  }
};
```

## 9. ماژول‌ها

### ES Modules
```javascript
// صادرات (export.js)
export const name = "Ali";
export function greet() { return "سلام"; }
export default class Person { }

// واردات (import.js)
import Person, { name, greet } from './export.js';
import * as Module from './export.js';
import { name as userName } from './export.js';
```

### CommonJS (Node.js)
```javascript
// صادرات (module.js)
const name = "Ali";
function greet() { return "سلام"; }
module.exports = { name, greet };
// یا
module.exports.name = "Ali";

// واردات
const module = require('./module.js');
const { name, greet } = require('./module.js');
```

## 10. API‌های مرورگر

### DOM Manipulation
```javascript
// انتخاب عناصر
const element = document.getElementById("id");
const elements = document.getElementsByClassName("class");
const elements2 = document.getElementsByTagName("div");
const element2 = document.querySelector(".class");
const elements3 = document.querySelectorAll("div");

// ویرایش المان‌ها
element.innerHTML = "<p>جدید</p>";
element.textContent = "متن جدید";
element.setAttribute("id", "newId");
element.style.color = "red";
element.classList.add("active");
element.classList.remove("inactive");
element.classList.toggle("visible");

// ایجاد و حذف عناصر
const newElement = document.createElement("div");
element.appendChild(newElement);
element.removeChild(childElement);
element.replaceChild(newElement, oldElement);
```

### Fetch API
```javascript
// درخواست HTTP
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

// تنظیمات Fetch
fetch('https://api.example.com/post', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ key: 'value' })
});
```

### Local Storage و Session Storage
```javascript
// Local Storage (ماندگار)
localStorage.setItem("key", "value");
const value = localStorage.getItem("key");
localStorage.removeItem("key");
localStorage.clear();

// Session Storage (تا بستن مرورگر)
sessionStorage.setItem("key", "value");
const sessionValue = sessionStorage.getItem("key");
```

### Web APIs دیگر
```javascript
// setTimeout و setInterval
const timeoutId = setTimeout(() => {
  console.log("بعد از 2 ثانیه");
}, 2000);
clearTimeout(timeoutId);

const intervalId = setInterval(() => {
  console.log("هر 1 ثانیه");
}, 1000);
clearInterval(intervalId);

// Geolocation
navigator.geolocation.getCurrentPosition(
  position => console.log(position.coords),
  error => console.error(error)
);

// History
history.back();
history.forward();
history.pushState({}, "عنوان", "/مسیر/جدید");

// Web Workers
const worker = new Worker("worker.js");
worker.postMessage("پیام");
worker.onmessage = e => console.log(e.data);
```

---

این سند مفاهیم کلیدی جاوااسکریپت را به‌صورت خلاصه پوشش می‌دهد. برای درک عمیق‌تر هر مبحث، منابع تخصصی بیشتری را مطالعه کنید.
