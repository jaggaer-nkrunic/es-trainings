---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
---

# Welcome to Slidev

Presentation slides for developers

<div class="pt-10">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: center
---

# Evolution of javascript

ECMAScript is a standard
JavaScript is an implemention

<v-clicks>

- ES5: 2009
- ES6: 2015
- ES2016
- ES2017
- ...
- ESNext

</v-clicks>

---
layout: center
---

# [TC39](http://tc39.es)
Technical Committee 39

The ECMA TC39 committee is responsible for evolving ECMAScript language 
Members from large companies - Google, Apple, Facebook, MS, Intel... 

[Stages](https://tc39.es/process-document/)  

<v-clicks>

- Stage 0 : Strawman - A free-form idea submission
- Stage 1 : Proposal : A formal proposal for the feature
- Stage 2 : Draft : first version of specification
- Stage 3 : Candidate : mostly finished, waiting for feedback
- Stage 4 : Finished : ready to be included in standard

</v-clicks>

---
layout: center
---

# ES5 - 2009
- Server side JS aka Node.js
- package managers - npm, bower
- modules - CommonJS, AMD, Browserify
- JS preprocessors - Grunt, Gulp, Webpack, ...

---
layout: center
---

# ES5 - 2009
- Server side JS aka Node.js
- package managers - npm, bower
- modules - CommonJS, AMD, Browserify
- JS preprocessors - Grunt, Gulp, Webpack, ...


---
layout: section
---

# Features

---

# let & const

Block scoped 

<div grid="~ cols-2 gap-4">
<div>

##### const

'Immutable' variable, cannot be reassigned  
```js {none|1|3-4|all}
const PI = 3.1415926;

PI = 3;
// TypeError: Assignment to constant variable.

```

note: only variable is immutable, not it's content  
```js {none|1-3|6|6-8|all}
const obj = {
  foo: 'bar',
};

// this is valid
obj.foo = 'mutable';

console.log(obj); // output: { foo: 'mutable' }

```
</div>
<div>

##### let

let works similarly to var, but the variable it declares is block-scoped

```js {none|1|3-6|8|all}
let foo = 'outer';

{
  let foo = 'inner';
  console.log(foo); // output: inner
}

console.log(foo); // output: outer
```

let cannot be redeclared

```js
let x = "Welcome";

let x = 0;

// SyntaxError: 'x' has already been declared
```

</div>
</div>

---

# Arrow functions
() => ({});

<div grid="~ cols-2 gap-4">
<div>

Less verbose, more expressive  

```js
const odds = evens.map(v => v + 1);
const pairs = evens.map(v => ({ even: v, odd: v + 1 }));
const pairsArray = evens.map(v => ([v, v + 1]));
const nums = evens.map((v, i) => v + i);
```

when using block syntax, `return` must be explicit

```js
const add = (x, y) => { return x + y };
```

fn without parameters

```js
const logDocument = () => console.log(document);
```

</div>
<div>

They share lexical `this` with surrounding code  

```js
function UiComponent() {
    const button = document.getElementById('myButton');
    button.addEventListener('click', () => {
        console.log('CLICK');
        this.handleClick(); // lexical `this`
    });
}
```

The following variables are all lexical inside arrow functions:  

<Transform :scale=".6">
<ul>
<li>arguments</li>
<li>super</li>
<li>this</li>
<li>new.target</li>
</ul>
</Transform>

</div>
</div>


---

# Function default parameters, rest, spread

defaults

<div grid="~ cols-2 gap-4">
<div>

give function parameters a default value

```js
function tuple(x, y = 0) {
    return [x, y];
}

tuple(10); // output: [10, 0]
tuple(10, 20); // output [10, 20]
```

rest parameters

aggregate remaining arguments into a single parameter
```js
function func(x, y, ...a) {
    return (x + y) + a.length;
}

func(1, 2, 'hello', true, 7); // output: 6
```

</div>
<div>

spread operator
```js {all|2|all}
function addTwo(x, y) {
  return x + y;
}

addtwo(...[2, 4]); // output: 6

// can be applied to any iterable
const str = 'foo';
const chars = [...str]; // output: ['f', 'o', 'o']

const parts = ['shoulders', 'knees'];
const lyrics = ['head', ...parts, 'and', 'toes'];
//output:  ["head", "shoulders", "knees", "and", "toes"]

// concatenate arrays
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];

arr1 = [...arr1, ...arr2]; // output: [0, 1, 2, 3, 4, 5]
```

</div>
</div>


---

# Template literals

Multi-line string literals that support interpolation

```js
const customer = { name: 'Foo' };
const card = { amount: 7, product: 'Bar', unitprice: 42 };
const message = `
Hello ${customer.name},
want to buy ${card.amount} ${card.product} for
a total of ${card.amount * card.unitprice} bucks?
`;

// output:
// Hello Foo,
// want to buy 7 Bar for
// a total of 294 bucks?
```

---

# Enhanced object literals

<div grid="~ cols-2 gap-4">
<div>

Short-hand object properties

```js
const first = 'John';
const last = 'Doe';

const name = { first, last };
// output:
// { first: 'John', last: 'Doe' }
```

Methods

```js
const firstName = 'John';
const lastName = 'Doe';

const user = {
  firstName,
  lastName,
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

user.fullName(); // output: John Doe
```
</div>
<div>

Computed property names

```js
const propKey = 'foo';
const obj = {
    [propKey]: true,
    ['b' + 'ar']: 123
};

console.log(obj) // output: { foo: true, bar: 123 }

const propKey = () => 'computed';
const obj = {
  [`${propKey()}_key`]: 42
};

console.log(obj); // output: { computed_key: 42 }

```

</div>
</div>

---

# Destructuring assignment

Destructure data structures into variable assignment

<div grid="~ cols-2 gap-4">
<div>

Arrays

```js
const arr = [1, 2, 3];

let [a, b, c] = arr;
// a = 1, b = 2, c = 3

let [a, ...rest] = arr;
// a = 1, rest = [2, 3]

// with defaults
let [a, b, c, d = 4] = arr;
// a = 1, b = 2, c = 3, d = 4

let [a, , b] = arr;
// a = 1, b = 3

// swap values
[a, b] = [b, a];
// a = 3, b = 1
```

</div>
<div>

Objects

```js
const user = {
  firstName: 'John',
  lastName: 'Doe',
}

const { firstName, lastName } = user;
// firstName = John, lastName = Doe

const { firstName, lastName, age = 25 } = user;
// firstName = John, lastName = Doe, age = 25;

// rename variables
const { firstName: first, lastName: last } = user;
// first = John, last = Doe

function fullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}

fullName(user); // output: John Doe
```

</div>
</div>
---

# Classes

<div grid="~ cols-2 gap-4">
<div>

```js
class Person {
  constructor({ firstName, lastName }) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  static staticMethod() {
    return 'this is a static method';
  }
}

const personData = {
  firstName: 'John',
  lastName: 'Doe',
}

const john = new Person(personData);
console.log(john);
// output: { firstName: 'John', lastName: 'Doe' }
console.log(john.fullName); // output: John Doe


```

</div>
<div>

```js
class User extends Person {
  static displayName = 'user';
  kind = 42;

  constructor({ firstName, lastName, email, role }) {
    super({ firstName, lastName });
    this.email = email;
    this._role = role;
  }

  get role() {
    return this._role;
  }

  set role(newRole) {
    this._role = newRole;
  }

  static staticMethod() {
    return `${super.staticMethod()} extended`;
  }
}


```

</div>
</div>

---

# Modules
Language-level support for modules

<div grid="~ cols-2 gap-4">
<div>

```js {none|1-3|1-7|all}
// lib/math.js
export function sum (x, y) { return x + y };
export const pi = 3.1415926;

// someComponent.js
// destructured imports
import { sum, pi } from './lib/math';

// wildcard imports
import * as math from './lib/math';

math.pi;
math.sum(5, 10);
```

Grouped exports

```js {none|1-2|1-3|all}
// lib/math.js
function sum(x, y) { return x + y };
const pi = 3.1415926;

export { sum, pi }
```

</div>
<div>

Default exports

```js
// lib/math.js
export default function sum(x, y) {
  return x + y;
}

//someComponent.js
import sum from 'lib/math';

```

</div>
</div>

---

# Map
Object-like data structure  

<div grid="~ cols-2 gap-4">
<div>

Map object holds key-value pairs and remembers the original insertion order 
Keys of a Map can be arbitrary values 

```js
const hashMap = new Map();

hashMap.set('a', 1);
hashMap.set('b', 2);
const objKey = { foo: 'bar' };
hashMap.set(objKey, { baz: 'x' });

hashMap.get('a'); // 1
hashMap.get(objKey); // { baz: 'x' }

// iterating
for (const entry of list) {
  console.log(entry);]
}
// destructure key, value
for (const [key, value] of list) {
  console.log(key, value);
}
```

</div>
<div>

Performs better in scenarios involving frequent additions and removals of key-value pairs. 

```js
// initialize from [key, value] pairs
const hashMap = new Map([
  ['a', 1],
  ['b', 2],
  [objKey, { baz: 'x' }]
]);

// methods and properties
hashMap.size // 3
hashMap.set(KEY, VALUE);
hashMap.get(KEY);
hashMap.delete(KEY);
hashMap.has(KEY);
hashMap.clear();
hashMap.keys();
hashMap.values();
hashMap.entries();

```

</div>
</div>

---

# Set
Array-like object  

The Set object lets you store unique values of any type  
It can be iterated through in insertion order  

<div grid="~ cols-2 gap-4">
<div>

```js
const list = new Set();
list.add('welcome');

// additions can be chained
list.add('hello').add('goodbye');

// initialize from array
const arr = [1, 1, 2, 2, 3, 4, 5];
const list = new Set(arr);
console.log(list); // Set(5) {1, 2, 3, 4, 5}

// convert it to array
const uniqueArray = [...list];
```
</div>
<div>

```js
// methods and properties
list.size // 5
list.add(VALUE);
list.delete(VALUE);
list.has(VALUE);
list.clear();
list.values();
list.keys();
list.entries();
```

</div>
</div>
---

# Arrays
New array methods 

Static methods  

```js
// creates array from array-like data structures
Array.from(document.querySelectorAll('*'));

// Similar to new Array(...), but without special one-arg behavior
Array.of(1, 2, 3);
```

Instance methods  

```js
const arr = [1, 2, 3];
arr.find(x => x === 3); // 3
arr.findIndex(x => x === 2); // 1
arr.includes(3); // true

// flatten an array
const arr1 = [0, 1, 2, [3, 4]];
arr.flat(); // [0, 1, 2, 3, 4];
```
---

# Objects
New object methods

<div grid="~ cols-2 gap-4">
<div>

Object.assign()

```js
// copy object own enumerable properties
// from one or more sources to a target

const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);
console.log(returnedTarget); // { a: 1, b: 4, c: 5 }
console.log(target); // { a: 1, b: 4, c: 5 }

// to clone object use empty object as target
const newObj = Object.assign({}, { a: 2 }, source);
// note: This is a shallow clone

// alternative with spread syntax
const newObj = { ...source, ...target };
```

</div>
<div>

Object.entries()

```js
// iterate over object's [key, value] pairs
const object1 = {
  a: 'somestring',
  b: 42
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"
```


</div>
</div>

---

<div grid="~ cols-2 gap-4">
<div>

Object.fromEntries()  
Inverse of Object.entries(), create object from [key, value] pairs  

```js
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```

Object.keys()

```js
// returns array of own enumerable property names
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]
```

</div>
<div>

Object.values()

```js
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.values(object1));
// expected output: Array ["somestring", 42, false]
```

</div>
</div>

---

# Promises
Async stuff  

<div grid="~ cols-2 gap-4">
<div>

```js
// create a promise
const promise = new Promise((resolve, reject) => {
  let condition;

  if (condition) {
    resolve('Promise is resolved successfully.');
  } else {
    reject('Promise is rejected');
  }
})


promise.then(result => {
  console.log(`Promise resolved: ${result}`);
}).catch(message => {
  console.log(`Promise rejected: ${message}`);
}).finally(() => {
  console.log('Do something regardless of promise state');
});
```

</div>
<div>
Async/await syntax

```js
async function fetchUserPreferences() {
  const user = await fetch('/api/user')
  const prefs = await fetch(`/api/prefs/${user.id}`);

  return prefs;
}

// error handling
async function fetchUserPreferences() {
  try {
    const user = await fetch('/api/user');
    const prefs = await fetch(`/api/prefs/${user.id}`);
  } catch (error) {
    // either throw error or return empty data
    throw new Error(error);
    return null;
  }
}
```


</div>
</div>

---

Send requests in parallel

```js
let names = ['iliakan', 'remy', 'jeresig'];

let requests = names.map(name => fetch(`https://api.github.com/users/${name}`));

Promise.all(requests)
  .then(responses => {
    // all responses are resolved successfully
    for(let response of responses) {
      alert(`${response.url}: ${response.status}`); // shows 200 for every url
    }

    return responses;
  })
  // map array of responses into an array of response.json() to read their content
  .then(responses => Promise.all(responses.map(r => r.json())))
```

```js
async function sendInParallel {
  let results = await Promise.all([
    fetch(url1),
    fetch(url2),
    ...
  ]);
}
```
---
