## Codestyle
styles taken from [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)

- [2.1](#references--prefer-const) Use `const` for all of your references; avoid using `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

> Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

- [2.2](#references--disallow-var) If you must reassign references, use `let` instead of `var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

> Why? `let` is block-scoped rather than function-scoped like `var`.

```javascript
// bad
var count = 1;
if (true) {
count += 1;
}

// good, use the let.
let count = 1;
if (true) {
count += 1;
}
```

## Objects

- [3.1](#objects--no-new) Use the literal syntax for object creation. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

```javascript
// bad
const item = new Object();

// good
const item = {};
```

- [3.3](#es6-object-shorthand) Use object method shorthand. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

- [3.8](#objects--rest-spread) Prefer the object spread operator over [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted.

```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```


## Arrays

- [4.1](#arrays--literals) Use the literal syntax for array creation. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

```javascript
// bad
const items = new Array();

// good
const items = [];
```

- [4.3](#es6-array-spreads) Use array spreads `...` to copy arrays.

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

- [4.6](#arrays--callback-return) Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement returning an expression without side effects, following [8.2](#arrows--implicit-return). eslint: [`array-callback-return`](https://eslint.org/docs/rules/array-callback-return)

```javascript
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map(x => x + 1);

// bad - no returned value means `memo` becomes undefined after the first iteration
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
});

// good
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  memo[index] = flatten;
  return flatten;
});

// bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

// good
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

## Destructuring

- [5.1](#destructuring--object) Use object destructuring when accessing and using multiple properties of an object. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring) 

> Why? Destructuring saves you from creating temporary references for those properties.

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

- [5.2](#destructuring--array) Use array destructuring. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)  

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```


## Strings

- [6.3](#es6-template-literals) When programmatically building up strings, use template strings instead of concatenation. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing) 

> Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

- [6.4](#strings--eval) Never use `eval()` on a string, it opens too many vulnerabilities. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

- [6.5](#strings--escaping) Do not unnecessarily escape characters in strings. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

> Why? Backslashes harm readability, thus they should only be present when necessary.

```javascript
// bad
const foo = '\'this\' \i\s \"quoted\"';

// good
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

## Functions

- [7.3](#functions--in-blocks) Never declare a function in a non-function block (`if`, `while`, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears. eslint: [`no-loop-func`](https://eslint.org/docs/rules/no-loop-func.html)

- [7.6](#es6-rest) Never use `arguments`, opt to use rest syntax `...` instead. eslint: [`prefer-rest-params`](https://eslint.org/docs/rules/prefer-rest-params)

> Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```

- [7.7](#es6-default-parameters) Use default parameter syntax rather than mutating function arguments.

```javascript
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```


- [7.8](#functions--default-side-effects) Avoid side effects with default parameters.

> Why? They are confusing to reason about.

```javascript
var b = 1;
// bad
function count(a = b++) {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

- [7.9](#functions--defaults-last) Always put default parameters last.

```javascript
// bad
function handleThings(opts = {}, name) {
  // ...
}

// good
function handleThings(name, opts = {}) {
  // ...
}
```

- [7.10](#functions--constructor) Never use the Function constructor to create a new function. eslint: [`no-new-func`](https://eslint.org/docs/rules/no-new-func)

> Why? Creating a function in this way evaluates a string similarly to eval(), which opens vulnerabilities.

```javascript
// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');
```

- [7.11](#functions--signature-spacing) Spacing in a function signature. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

> Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.

```javascript
// bad
const f = function(){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

- [7.13](#functions--reassign-params) Never reassign parameters. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

> Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```

- [7.14](#functions--spread-vs-apply) Prefer the use of the spread operator `...` to call variadic functions. eslint: [`prefer-spread`](https://eslint.org/docs/rules/prefer-spread)

> Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose `new` with `apply`.

```javascript
// bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// good
const x = [1, 2, 3, 4, 5];
console.log(...x);

// bad
new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

// good
new Date(...[2016, 8, 5]);
```

- [7.15](#functions--signature-invocation-indentation) Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item.

```javascript
// bad
function foo(bar,
             baz,
             quux) {
  // ...
}

// good
function foo(
  bar,
  baz,
  quux,
) {
  // ...
}

// bad
console.log(foo,
  bar,
  baz);

// good
console.log(
  foo,
  bar,
  baz,
);
```

## Arrow Functions

- [8.1](#arrows--use-them) When you must use an anonymous function (as when passing an inline callback), use arrow function notation. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html) 

> Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

> Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.

```javascript
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

- [8.2](#arrows--implicit-return) If the function body consists of a single statement returning an [expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a `return` statement. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html) 

> Why? Syntactic sugar. It reads well when multiple functions are chained together.

```javascript
// bad
[1, 2, 3].map(number => {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map(number => `A string containing the ${number}.`);

// good
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  return `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number, index) => ({
  [index]: number,
}));

// No implicit return with side effects
function foo(callback) {
  const val = callback();
  if (val === true) {
    // Do something if callback returns true
  }
}

let bool = false;

// bad
foo(() => bool = true);

// good
foo(() => {
  bool = true;
});
```

- [8.5](#arrows--confusing) Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`). eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

```javascript
// bad
const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

// good
const itemHeight = (item) => {
  const { height, largeSize, smallSize } = item;
  return height > 256 ? largeSize : smallSize;
};
```
    
## Classes & Constructors

- [9.1](#constructors--use-class) Always use `class`. Avoid manipulating `prototype` directly.

> Why? `class` syntax is more concise and easier to reason about.

```javascript
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

- [9.2](#constructors--extends) Use `extends` for inheritance.

> Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

```javascript
// bad
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};

// good
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}
```

- [9.3](#constructors--chaining) Methods can return `this` to help with method chaining.

```javascript
// bad
Jedi.prototype.jump = function () {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function (height) {
  this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();

luke.jump()
  .setHeight(20);
```

## Modules

- [10.7](#modules--imports-first) Put all `import`s above non-import statements.
eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
> Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

```javascript
// bad
import foo from 'foo';
foo.init();

import bar from 'bar';

// good
import foo from 'foo';
import bar from 'bar';

foo.init();
```

- [10.8](#modules--multiline-imports-over-newlines) Multiline imports should be indented just like multiline array and object literals.

> Why? The curly braces follow the same indentation rules as every other curly brace block in the style guide, as do the trailing commas.

```javascript
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

// good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE,
} from 'path';
```

## Iterators and Generators

- [11.1](#iterators--nope) Don’t use iterators. Prefer JavaScript’s higher-order functions instead of loops like `for-in` or `for-of`. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

> Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side effects.

> Use `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... to iterate over arrays, and `Object.keys()` / `Object.values()` / `Object.entries()` to produce arrays so you can iterate over objects.

```javascript
const numbers = [1, 2, 3, 4, 5];

// bad
let sum = 0;
for (let num of numbers) {
  sum += num;
}
sum === 15;

// good
let sum = 0;
numbers.forEach((num) => {
  sum += num;
});
sum === 15;

// best (use the functional force)
const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;

// bad
const increasedByOne = [];
for (let i = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}

// good
const increasedByOne = [];
numbers.forEach((num) => {
  increasedByOne.push(num + 1);
});

// best (keeping it functional)
const increasedByOne = numbers.map(num => num + 1);
```
## Properties

- [12.1](#properties--dot) Use dot notation when accessing properties. eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

```javascript
const luke = {
  jedi: true,
  age: 28,
};

// bad
const isJedi = luke['jedi'];

// good
const isJedi = luke.jedi;
```

- [12.2](#properties--bracket) Use bracket notation `[]` when accessing properties with a variable.

```javascript
const luke = {
  jedi: true,
  age: 28,
};

function getProp(prop) {
  return luke[prop];
}

const isJedi = getProp('jedi');
```

## Variables

- [13.1](#variables--const) Always use `const` or `let` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that. eslint: [`no-undef`](https://eslint.org/docs/rules/no-undef) [`prefer-const`](https://eslint.org/docs/rules/prefer-const)

```javascript
// bad
superPower = new SuperPower();

// good
const superPower = new SuperPower();
```

- [13.2](#variables--one-const) Use one `const` or `let` declaration per variable. eslint: [`one-var`](https://eslint.org/docs/rules/one-var.html) 

> Why? It’s easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

```javascript
// bad
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// bad
// (compare to above, and try to spot the mistake)
const items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

- [13.3](#variables--const-let-group) Group all your `const`s and then group all your `let`s.

> Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

```javascript
// bad
let i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;
let len;

// good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

- [13.5](#variables--no-chain-assignment) Don’t chain variable assignments. eslint: [`no-multi-assign`](https://eslint.org/docs/rules/no-multi-assign)

> Why? Chaining variable assignments creates implicit global variables.

```javascript
// bad
(function example() {
  // JavaScript interprets this as
  // let a = ( b = ( c = 1 ) );
  // The let keyword only applies to variable a; variables b and c become
  // global variables.
  let a = b = c = 1;
}());

console.log(a); // throws ReferenceError
console.log(b); // 1
console.log(c); // 1

// good
(function example() {
  let a = 1;
  let b = a;
  let c = a;
}());

console.log(a); // throws ReferenceError
console.log(b); // throws ReferenceError
console.log(c); // throws ReferenceError

// the same applies for `const`
```
    
## Comparison Operators & Equality

- [15.1](#comparison--eqeqeq) Use `===` and `!==` over `==` and `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

- [15.3](#comparison--shortcuts) Use shortcuts for booleans, but explicit comparisons for strings and numbers.

  ```javascript
  // bad
  if (isValid === true) {
    // ...
  }

  // good
  if (isValid) {
    // ...
  }

  // bad
  if (name) {
    // ...
  }

  // good
  if (name !== '') {
    // ...
  }

  // bad
  if (collection.length) {
    // ...
  }

  // good
  if (collection.length > 0) {
    // ...
  }
  ```
- [15.5](#comparison--switch-blocks) Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`). eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

> Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

```javascript
// bad
switch (foo) {
  case 1:
    let x = 1;
    break;
  case 2:
    const y = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}

// good
switch (foo) {
  case 1: {
    let x = 1;
    break;
  }
  case 2: {
    const y = 2;
    break;
  }
  case 3: {
    function f() {
      // ...
    }
    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}
```

- [15.6](#comparison--nested-ternaries) Ternaries should not be nested and generally be single line expressions. eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

```javascript
// bad
const foo = maybe1 > maybe2
  ? "bar"
  : value1 > value2 ? "baz" : null;

// split into 2 separated ternary expressions
const maybeNull = value1 > value2 ? 'baz' : null;

// better
const foo = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// best
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

- [15.7](#comparison--unneeded-ternary) Avoid unneeded ternary statements. eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

```javascript
// bad
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;

// good
const foo = a || b;
const bar = !!c;
const baz = !c;
```

- [15.8](#comparison--no-mixed-operators) Enclose operators in parentheses when they are mixed in a statement. When mixing arithmetic operators, do not mix `**` and `%` with themselves or with `+`, `-`, `*`, & `/`. eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

> Why? This improves readability and clarifies the developer’s intention.

```javascript
// bad
const foo = a && b < 0 || c > 0 || d + 1 === 0;

// bad
const bar = a ** b - 5 % d;

// bad
if (a || b && c) {
  return d;
}

// good
const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

// good
const bar = (a ** b) - (5 % d);

// good
if ((a || b) && c) {
  return d;
}

// good
const bar = a + b / c * d;
```


## Blocks

- [16.1](#blocks--braces) Use braces with all multi-line blocks. eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

```javascript
// bad
if (test)
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}

// bad
function foo() { return false; }

// good
function bar() {
  return false;
}
```

- [16.2](#blocks--cuddled-elses) If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your `if` block’s closing brace. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

```javascript
// bad
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

// good
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}
```
## Control Statements

- [17.1](#control-statements) In case your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

> Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

```javascript
// bad
if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// bad
if (foo === 123 &&
  bar === 'abc') {
  thing1();
}

// bad
if (foo === 123
  && bar === 'abc') {
  thing1();
}

// bad
if (
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}

// good
if (
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

// good
if (
  (foo === 123 || bar === "abc")
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

// good
if (foo === 123 && bar === 'abc') {
  thing1();
}
```

## Comments


- [18.1](#comments--multiline) Use `/** ... */` for multi-line comments.

```javascript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed-in tag name
 */
function make(tag) {

  // ...

  return element;
}
```

- [18.2](#comments--singleline) Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

```javascript
// bad
const active = true;  // is current tab

// good
// is current tab
const active = true;

// bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
}

// good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
}

// also good
function getType() {
  // set the default type to 'no type'
  const type = this.type || 'no type';

  return type;
}
```

- [18.3](#comments--spaces) Start all comments with a space to make it easier to read. eslint: [`spaced-comment`](https://eslint.org/docs/rules/spaced-comment)

```javascript
// bad
//is current tab
const active = true;

// good
// is current tab
const active = true;

// bad
/**
 *make() returns a new element
 *based on the passed-in tag name
 */
function make(tag) {

  // ...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed-in tag name
 */
function make(tag) {

  // ...

  return element;
}
```

- [18.4](#comments--actionitems) Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME: -- need to figure this out` or `TODO: -- need to implement`.

- [18.5](#comments--fixme) Use `// FIXME:` to annotate problems.

```javascript
class Calculator extends Abacus {
  constructor() {
    super();

    // FIXME: shouldn’t use a global here
    total = 0;
  }
}
```

- [18.6](#comments--todo) Use `// TODO:` to annotate solutions to problems.

```javascript
class Calculator extends Abacus {
  constructor() {
    super();

    // TODO: total should be configurable by an options param
    this.total = 0;
  }
}
```

## Whitespace

- [19.2](#whitespace--before-blocks) Place 1 space before the leading brace. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html) 

```javascript
// bad
function test(){
  console.log('test');
}

// good
function test() {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```

- [19.3](#whitespace--around-keywords) Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html) 

```javascript
// bad
if(isJedi) {
  fight ();
}

// good
if (isJedi) {
  fight();
}

// bad
function fight () {
  console.log ('Swooosh!');
}

// good
function fight() {
  console.log('Swooosh!');
}
```

- [19.4](#whitespace--infix-ops) Set off operators with spaces. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html) 

```javascript
// bad
const x=y+5;

// good
const x = y + 5;
```
- [19.6](#whitespace--chains) Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which
emphasizes that the line is a method call, not a new statement. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

```javascript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// bad
$('#items').
  find('.selected').
    highlight().
    end().
  find('.open').
    updateCount();

// good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();

// bad
const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
    .attr('width', (radius + margin) * 2).append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led')
    .data(data)
  .enter().append('svg:svg')
    .classed('led', true)
    .attr('width', (radius + margin) * 2)
  .append('svg:g')
    .attr('transform', `translate(${radius + margin},${radius + margin})`)
    .call(tron.led);

// good
const leds = stage.selectAll('.led').data(data);
```

- [19.7](#whitespace--after-blocks) Leave a blank line after blocks and before the next statement.

```javascript
// bad
if (foo) {
  return bar;
}
return baz;

// good
if (foo) {
  return bar;
}

return baz;

// bad
const obj = {
  foo() {
  },
  bar() {
  },
};
return obj;

// good
const obj = {
  foo() {
  },

  bar() {
  },
};

return obj;

// bad
const arr = [
  function foo() {
  },
  function bar() {
  },
];
return arr;

// good
const arr = [
  function foo() {
  },

  function bar() {
  },
];

return arr;
```

- [19.8](#whitespace--padded-blocks) Do not pad your blocks with blank lines. eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html)

```javascript
// bad
function bar() {

  console.log(foo);

}

// bad
if (baz) {

  console.log(qux);
} else {
  console.log(foo);

}

// bad
class Foo {

  constructor(bar) {
    this.bar = bar;
  }
}

// good
function bar() {
  console.log(foo);
}

// good
if (baz) {
  console.log(qux);
} else {
  console.log(foo);
}
```

- [19.9](#whitespace--in-parens) Do not add spaces inside parentheses. eslint: [`space-in-parens`](https://eslint.org/docs/rules/space-in-parens.html)

```javascript
// bad
function bar( foo ) {
  return foo;
}

// good
function bar(foo) {
  return foo;
}

// bad
if ( foo ) {
  console.log(foo);
}

// good
if (foo) {
  console.log(foo);
}
```

- [19.10](#whitespace--in-brackets) Do not add spaces inside brackets. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html) 

```javascript
// bad
const foo = [ 1, 2, 3 ];
console.log(foo[ 0 ]);

// good
const foo = [1, 2, 3];
console.log(foo[0]);
```

- [19.11](#whitespace--in-braces) Add spaces inside curly braces. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html) 

```javascript
// bad
const foo = {clark: 'kent'};

// good
const foo = { clark: 'kent' };
```

- [19.12](#whitespace--max-len) Avoid having lines of code that are longer than 150 characters (including whitespace). Note: per [above](#strings--line-length), long strings are exempt from this rule, and should not be broken up. eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

> Why? This ensures readability and maintainability.

```javascript
// bad
const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

// bad
$.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

// good
const foo = jsonData
  && jsonData.foo
  && jsonData.foo.bar
  && jsonData.foo.bar.baz
  && jsonData.foo.bar.baz.quux
  && jsonData.foo.bar.baz.quux.xyzzy;

// good
$.ajax({
  method: 'POST',
  url: 'https://airbnb.com/',
  data: { name: 'John' },
})
  .done(() => console.log('Congratulations!'))
  .fail(() => console.log('You have failed this city.'));
```

## Commas

- [20.1](#commas--leading-trailing) Leading commas: **Nope.** eslint: [`comma-style`](https://eslint.org/docs/rules/comma-style.html)

```javascript
// bad
const story = [
    once
  , upon
  , aTime
];

// good
const story = [
  once,
  upon,
  aTime,
];

// bad
const hero = {
    firstName: 'Ada'
  , lastName: 'Lovelace'
  , birthYear: 1815
  , superPower: 'computers'
};

// good
const hero = {
  firstName: 'Ada',
  lastName: 'Lovelace',
  birthYear: 1815,
  superPower: 'computers',
};
```

- [20.2](#commas--dangling) Additional trailing comma: **Yup.** eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

> Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don’t have to worry about the [trailing comma problem](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) in legacy browsers.

```diff
// bad - git diff without trailing comma
const hero = {
     firstName: 'Florence',
-    lastName: 'Nightingale'
+    lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing']
};

// good - git diff with trailing comma
const hero = {
     firstName: 'Florence',
     lastName: 'Nightingale',
+    inventorOf: ['coxcomb chart', 'modern nursing'],
};
```

```javascript
// bad
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

const heroes = [
  'Batman',
  'Superman'
];

// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

const heroes = [
  'Batman',
  'Superman',
];

// bad
function createHero(
  firstName,
  lastName,
  inventorOf
) {
  // does nothing
}

// good
function createHero(
  firstName,
  lastName,
  inventorOf,
) {
  // does nothing
}

// good (note that a comma must not appear after a "rest" element)
function createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
) {
  // does nothing
}

// bad
createHero(
  firstName,
  lastName,
  inventorOf
);

// good
createHero(
  firstName,
  lastName,
  inventorOf,
);

// good (note that a comma must not appear after a "rest" element)
createHero(
  firstName,
  lastName,
  inventorOf,
  ...heroArgs
);
```

## Semicolons

- [21.1](#semicolons--required) **Yup.** eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

```javascript
// bad
(function () {
  const name = 'Skywalker'
  return name
})()

// good
(function () {
  const name = 'Skywalker';
  return name;
}());

// good, but legacy (guards against the function becoming an argument when two files with IIFEs are concatenated)
;((() => {
  const name = 'Skywalker';
  return name;
})());
```

## Type Casting & Coercion

- [22.3](#coercion--numbers) Numbers: Use `Number` for type casting and `parseInt` always with a radix for parsing strings. eslint: [`radix`](https://eslint.org/docs/rules/radix) [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

```javascript
const inputValue = '4';

// bad
const val = new Number(inputValue);

// bad
const val = +inputValue;

// bad
const val = inputValue >> 0;

// bad
const val = parseInt(inputValue);

// good
const val = Number(inputValue);

// good
const val = parseInt(inputValue, 10);
```


- [22.6](#coercion--booleans) Booleans: eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

```javascript
const age = 0;

// bad
const hasAge = new Boolean(age);

// good
const hasAge = Boolean(age);

// best
const hasAge = !!age;
```

## Naming Conventions

- [23.1](#naming--descriptive) Avoid single letter names. Be descriptive with your naming. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

```javascript
// bad
function q() {
  // ...
}

// good
function query() {
  // ...
}
```

- [23.2](#naming--camelCase) Use camelCase when naming objects, functions, and instances. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

```javascript
// bad
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

// good
const thisIsMyObject = {};
function thisIsMyFunction() {}
```


- [23.3](#naming--PascalCase) Use PascalCase only when naming constructors or classes. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

```javascript
// bad
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```

- [23.7](#naming--camelCase-default-export) Use camelCase when you export-default a function. Your filename should be identical to your function’s name.

```javascript
function makeStyleGuide() {
  // ...
}

export default makeStyleGuide;
```

- [23.8](#naming--PascalCase-singleton) Use PascalCase when you export a constructor / class / singleton / function library / bare object.

```javascript
const AirbnbStyleGuide = {
  es6: {
  },
};

export default AirbnbStyleGuide;
```

- [23.9](#naming--Acronyms-and-Initialisms) Acronyms and initialisms should always be all capitalized, or all lowercased.

> Why? Names are for readability, not to appease a computer algorithm.

```javascript
// bad
import SmsContainer from './containers/SmsContainer';

// bad
const HttpRequests = [
  // ...
];

// good
import SMSContainer from './containers/SMSContainer';

// good
const HTTPRequests = [
  // ...
];

// also good
const httpRequests = [
  // ...
];

// best
import TextMessageContainer from './containers/TextMessageContainer';

// best
const requests = [
  // ...
];
```

    
taken from  [https://standardjs.com/rules.html#javascript-standard-style](https://standardjs.com/rules.html#javascript-standard-style)

#### 24.1 No unused variables.

eslint: [`no-unused-varsp`](https://eslint.org/docs/rules/no-unused-vars.html)
```
function myFunction () {
var result = something()   // ✗ avoid 
}
```

#### 24.2 Multiple blank lines not allowed.
eslint: [`no-multiple-empty-lines`](https://eslint.org/docs/rules/no-multiple-empty-lines.html)

```
// ✓ ok 
var value = 'hello world'
console.log(value)

// ✗ avoid 
var value = 'hello world'


console.log(value)
```

#### 24.3 For the ternary operator in a multi-line setting, place ? and : on their own lines.

eslint: [`operator-linebreak`](https://eslint.org/docs/rules/operator-linebreak.html) 

```
// ✓ ok 
var location = env.development ? 'localhost' : 'www.api.com'

// ✓ ok 
var location = env.development
? 'localhost'
: 'www.api.com'

// ✗ avoid 
var location = env.development ?
'localhost' :
'www.api.com'
```

#### 24.4 Add space between colon and value in key value pairs.

eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing.html) 

```
var obj = { 'key' : 'value' }    // ✗ avoid 
var obj = { 'key' :'value' }     // ✗ avoid 
var obj = { 'key':'value' }      // ✗ avoid 
var obj = { 'key': 'value' }     // ✓ ok 
```

#### 24.5 No debugger statements.

eslint: [`no-debugger`](https://eslint.org/docs/rules/no-debugger.html) 

```
function sum (a, b) {
debugger      // ✗ avoid 
return a + b
}
```

#### 24.6 No function declarations in nested blocks.

eslint: [`no-inner-declarations`](https://eslint.org/docs/rules/no-inner-declarations.html) 

```
if (authenticated) {
function setAuthUser () {}    // ✗ avoid 
}
```

#### 24.7 No invalid regular expression strings in RegExp constructors.

eslint: [`no-invalid-regexp`](https://eslint.org/docs/rules/no-invalid-regexp.html) 

```
RegExp('[a-z')    // ✗ avoid 
RegExp('[a-z]')   // ✓ ok 
```

#### 24.8 No unnecessary nested blocks.

eslint: [`no-lone-blocks`](https://eslint.org/docs/rules/no-lone-blocks.html) 

```
function myFunc () {
{                   // ✗ avoid 
myOtherFunc()
}
}

function myFunc () {
myOtherFunc()       // ✓ ok 
}
```

#### 24.9 No unreachable code after return, throw, continue, and break statements.

eslint: [`no-unreachable`](https://eslint.org/docs/rules/no-unreachable.html) 

```
function doSomething () {
return true
console.log('never called')     // ✗ avoid 
}
```

#### 24.10 No unnecessary constructor.

eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor.html) 


```
class Car {
constructor () {      // ✗ avoid 
}
}
```

#### 24.11 Maintain consistency of newlines between object properties.

eslint: [`object-property-newline`](https://eslint.org/docs/rules/object-property-newline.html) 

```
const user = {
name: 'Jane Doe', age: 30,
username: 'jdoe86'            // ✗ avoid 
}

const user = { name: 'Jane Doe', age: 30, username: 'jdoe86' }    // ✓ ok 

const user = {
name: 'Jane Doe',
age: 30,
username: 'jdoe86'
}  
```

#### 24.12 No padding within blocks.

eslint: [`padded-blocks`](https://eslint.org/docs/rules/padded-blocks.html) 

```
if (user) {
                        // ✗ avoid 
const name = getName()

}

if (user) {
const name = getName()    // ✓ ok 
}
```

#### 24.13 typeof must be compared to a valid string.

eslint: [`valid-typeof`](https://eslint.org/docs/rules/valid-typeof.html) 

```
typeof name === 'undefimed'     // ✗ avoid 
typeof name === 'undefined'     // ✓ ok 
```

#### 24.14 Avoid Yoda conditions.

eslint: [`yoda`](https://eslint.org/docs/rules/yoda.html) 

```
if (42 === age) { }    // ✗ avoid 
if (age === 42) { }    // ✓ ok
```

#### 24.15 enforce a maximum file length

eslint: [`max-lines`](https://eslint.org/docs/rules/max-lines.html) 
