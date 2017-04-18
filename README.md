
# Orus JavaScript Style Guidelines
The Orus team JavaScript best pratices

No matter how many people consitute the Orus team, we always try to make all of our code looks like a single person wrote it. Every Orus team member should refer to this document as a statement of our projects commitment to code style readability and maintainability.

### Build & Deployment
Projects should always attempt to include some generic means by which source can be linted, tested and compressed in preparation for production use. And we rely on [Webpack](https://webpack.github.io/docs/) to accomplish this task.

### Tips
When you access a primitive type (`string`, `number`, `boolean`, `null`, `undefined`) you work directly on its value.

```javascript
const foo = 1;
let bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

But when you access a complex type (`object`, `array`, `function`) you work on a reference to its value.

```javascript
const foo = [1, 2];
const bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

### General formatting

Always use soft tabs (space character) set to 2 spaces.

```javascript
// STOP
function foo() {
∙∙∙∙let name;
}

// Not so good
function bar() {
∙let name;
}

// Better
function baz() {
∙∙let name;
}
```

Place no space between the argument list and the function name in function calls and declarations.

```javascript
// Avoid
function fight () {
  console.log ('Swooosh!');
}

// Better
function fight() {
  console.log('Swooosh!');
}
```

For readability, set off operators with spaces.

```javascript
// BAD BAD BAD!
const x=y+5;

// Better
const x = y + 5;
```

We recommend to add a newline character at the end of your files.
```javascript
// bad
import { kirk } from './Enterprise';
  // ...
export default fleet;
 
// Not so good
import { kirk } from './Enterprise';
  // ...
export default kirk;↵
↵

// Better
import { kirk } from './Enterprise';
  // ...
export default kirk;↵
```

Use indentation when typing long method chains (more than 2 method chains). Use a leading dot.

```javascript
// Not so good
$('#items').find('.selected').collapse().find('.is-open').lunchChat();

// Please don't
$('#items').
  find('.selected').
  collapse().
  find('.open').
  lunchChat();

// Better
$('#items')
  .find('.selected')
  .collapse()
  .find('.open')
  .lunchChat();
```

Put a blank line after blocks and before the next statement.

```javascript
// Not so good
if (human) {
  return earth;
}
return mars;

// Better
if (human) {
  return earth;
}

return mars;


// Not so good
const ship = {
  function fly() {
  },
  function fire() {
  },
};
return ship;

// Better
const ship = {
  function fly() {
  },

  function fire() {
  },
};

return ship;
```

Do not pad your blocks with blank lines.

```javascript
// Not so good
function fire() {

  console.log("Bullet fired");

}

// Better
function bar() {
  console.log(foo);
}
```

Do not add spaces inside parentheses.

```javascript
// Not so good
function doSomething( foo ) {
  return foo;
}

// Better
function doSomething(foo) {
  return foo;
}


// Not so good
if ( foo ) {
  console.log(foo);
}

// Better
if (foo) {
  console.log(foo);
}
```

Do not add spaces inside brackets.

```javascript
// Not so good
const arr = [ 1, 2, 3 ];
console.log(arr[ 0 ]);

// Better
const arr = [1, 2, 3];
console.log(arr[0]);
```

Add spaces inside curly braces.

```javascript
// Not so good
const arrow = {oliver: 'Queen'};

// Better
const arrow = { oliver: 'Quenn' };
```

Make sure you don't have in your code, line that are longer than 100 characters (including whitespace) for readability.

```javascript
// Not so good
$.ajax({ method: 'POST', url: 'https://starcity.com/', data: { name: 'Oliver Queen' } }).done(() => console.log('Congratulations Green Arrow!')).fail(() => console.log('You have failed this city.'));

// Better
$.ajax({
  method: 'POST',
  url: 'https://starcity.com/',
  data: { name: 'Oliver Queen' },
})
  .done(() => console.log('Congratulations Green Arrow!'))
  .fail(() => console.log('You have failed this city.'));
```


Do not use leading commas and add trailing commas. It's better for clarity and since Babel will remove them in the compilation process, you don't have to worry about the trailing comma problem.

```javascript
// Not so good
const legend = {
    firstName: 'Isaac'
  , lastName: 'Newton'
  , birthYear: 1642
  , domain: 'Physics'
};

// Better
const legend = {
  firstName: 'Isaac',
  lastName: 'Newton',
  birthYear: 1642,
  domain: 'Physics',
};
```

Always use semicolons.

```javascript
// bad
(function () {
  const name = 'Feynman'
  return name
})()

// Better
(function () {
  const name = 'Feynman';
  return name;
}());
```

### Comments
Use `/** ... */` for multi-line comments.

```javascript
// Not so good
// train() returns a new skill
// based on the passed in person
//
// @param {String} person
// @return {Skill} skill
function train(person) {

  // ...

  return skill;
}

// Better
/**
 * Train a person and return a new skill
 *
 * @param {String} person
 * @return {Skill} skill
 */
function train(person) {

  // ...

  return skill;
}
```

Prefer `//` for single line comments. Place single line comments on a newline above the subject of the comment. Unless you're on the first line of the block, always put new line before your comment.

```javascript
// Not so good
function getUser() {
  console.log('fetching user...');
  const user = this.user || 'John Doe'; // set the default user to 'John Doe'

  return user;
}

// Better
function getUser() {
  // set the default type to 'John Doe'
  const user = this.user || 'John Doe';

  return user;
}
```

Always start your comments with a space for readability.

```javascript
// Not so good
//is signing up
const processing = true;

// Better
// is signing up
const processing = true;
```

When Prefixing your comments with either `TODO` or `FIXME`, you give ability to other developers to fast understand what kind of message you are trying to send. Either is an issue that need to be fixed or a suggestion for a solution that should be implemented. That way helps better than typing a regular comment.

```javascript
class WaveRider {
  ride() {
    super();

    // FIXME: need to precise the time as well
    periode = new Date('3017-09-10');
  }
}
 
class WaveRide {
  ride() {
    super();

    // TODO: periode should be passed as parameter
    periode = new Date('3017-09-10');
  }
}
```

### Performance
This is maybe the most important guideline, always prior readability and correctness over performance. Optimize image and network access should be enough for performance.

```javascript
// Not so good
const arr = [1, 2, 3, 4];
const len = arr.length;
var i= -1;
var result = [];
while (++i < len) {
  var n = arr[i];
  if (n % 2 > 0) continue;
  result.push(n * n);
}

// Better
const arr = [1, 2, 3, 4];
const square = n => n * n;
const isEven = n => n % 2 == 0;

const result = arr.filter(isEven).map(square);
```

### Statelessness
Try to keep your functions pure. Functions should not produce side-effects, not affect any outside variable and always return new objects.

```javascript
// Not so good
const merge = (target, ...sources) => Object.assign(target, ...sources);
const result = merge({ oliver: "Queen" }, { barry: "Allen" });
console.log(result);
// => { oliver: "Queen", barry: "Allen" }

// Better
const merge = (...sources) => Object.assign({}, ...sources);
const result = merge({ oliver: "Queen" }, { barry: "Allen" });
console.log(result);
// => { oliver: "Queen", barry: "Allen" }
```

### Natives
When you can, rely on native methods

```javascript
// Not so good
const toArray = obj => [].slice.call(obj);

// Better
const toArray = (() =>
  Array.from ? Array.from : obj => [].slice.call(obj)
)();
```

### Coercion
Whether you prefer single or double shouldn't matter, 
What **ABSOLUTELY** matter is consistency. Never mix single and double quotes in the same project. Stick with only one please.

Your code need to be as simple as possible for readability. **Refactoring is the key**.

```javascript
// Not so good
if (x === undefined || x === null) { ... }

// Better
if (x == undefined) { ... }
```

### Naming

Avoid single letter names. Be descriptive with your naming.

```javascript
// Not so good
function q() {
  // ...
}

// Better
function query() {
  // ...
}
```

We are not a human code compiler/compressor, so don't try to be one. Your code has to be readable.
```javascript
// Never do that
function q( s ) {
  return document.querySelectorAll( s );
}
var i,a=[],els=q("#foo");
for(i=0;i< els.length;i++){a.push(els[i]);}
 
// Better
function query(selector) {
  return document.querySelectorAll(selector);
}

let idx = 0;
let elements = [];
const matches = query("#foo");
const length = matches.length;

for ( ; idx < length; idx++ ) {
  elements.push(matches[idx]);
}
```

Use camelCase when naming objects, functions, and instances.

```javascript
// Not so good
const NEVerrrrr = {};
const this_is_not_good = {};
function a() {}

// Better
const myObject = {};
function doSomethingAmazing() {}
```

Use PascalCase only when naming constructors or classes.

```javascript
// Not so good
function user(options) {
  this.name = options.name;
}

const never = new user({
  name: "don't",
});

// Better
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const better = new User({
  name: "yeah",
});
```

In JavaScript, we don't have the concept of privacy for properties or methods so don't put trailing or leading underscores before any of your varibles.

```javascript
// Not so good
this._firstName = 'Bad';
this.firstName_ = 'Worse';
this.__firstName__ = 'Never';

// Better
this.firstName = 'Yeah!';
```

Don't fall in saving reference to `this`. Use arrow functions or `Function#bind` instead.

```javascript
// Not so good
function run() {
  const self = this;
  return function () {
    console.log(self);
  };
}

// Better
function run() {
  return () => {
    console.log(this);
  };
}
```

Make sure your base filename exactly match the name of its default export.

```javascript
// Not so good

// in some file
class DatePicker {
  // ...
}
export default DatePicker;

// in another file
import DatePicker from './datePicker';



// Better

// in some file
class DatePicker {
  // ...
}
export default DatePicker;

// in another file
import DatePicker from './DatePicker';
```

Use camelCase when you export-default a function. Your filename should be identical to your function's name.

```javascript
function makePeace() {
  // ...
}

export default makePeace;
```

Use PascalCase when you export a constructor / class / singleton / function library / bare object.

```javascript
const OrusBestPractice = {
  es6: {
  },
};

export default OrusBestPractice;
```

Make sure acronyms and initialisms are either all capitalized, or all lowercased.

```javascript
// Not so good
import SmsNotification from './notifications/SmsNotification';
import DATABASENotification from './notifications/DATABASENotification';

// Better
import SMSNotification from './containers/SMSNotification';
import DatabaseNotification from './notifications/Databaseotification';


// Not so good
const HTTPRequests = [
  // ...
];

// Better
const Requests = [
  // ...
];
```

Here are  a few naming pointers.

```javascript
`hero` is a string

// Naming arrays
`heroes` is an array of `dog` strings

// Naming regular expressions
rDesc = //;
```
And Don't ever forget that
```javascript
functionNamesLikeThis;
variableNamesLikeThis;
ConstructorNamesLikeThis;
EnumNamesLikeThis;
methodNamesLikeThis;
SYMBOLIC_CONSTANTS_LIKE_THIS;
```

### Loops

We suggest you to Rely on `array.prototype` methods since loops force you to use mutable objects.

```javascript
// Not so good
const sum = arr => {
  var sum = 0;
  var i = -1;
  for (;arr[++i];) {
    sum += arr[i];
  }
  return sum;
};

console.log(sum([1, 2, 3]));
// => 6

// Better
const sum = arr =>
  arr.reduce((x, y) => x + y);

console.log(sum([1, 2, 3]));
// => 6
```

Use recursion when you cannot rely on `array.prototype` methods.

```javascript
// Not so good
const createParagraphs = howMany =>
  [...Array(howMany)].forEach(() =>
    document.body.insertAdjacentHTML("beforeend", "<div></div>")
  );
createParagraphs(5);

// Worse
const createParagraphs = howMany => {
  while (howMany--) {
    document.body.insertAdjacentHTML("beforeend", "<p></p>");
  }
};
createParagraphs(5);


// Better
const createParagraphs = howMany => {
  if (!howMany) return;
  document.body.insertAdjacentHTML("beforeend", "<p></p>");
  return createParagraphs(howMany - 1);
};
createParagraphs(5);
```

Here's a [generic loop function](https://gist.github.com/bendc/6cb2db4a44ec30208e86) making recursion easier to use.

### Arguments
Prefer the rest `...` parameter over the `arguments` object. It's name and is a real array so it's easier to use than the `arguments` object and its gives you a better idea of what the function is excepting.

```javascript
// Not so good
const sortNumbers = () =>
  Array.prototype.slice.call(arguments).sort();

// Better
const sortNumbers = (...numbers) => numbers.sort();
```

### Apply
Make sure to use the spread `...` operator instead of `apply()`.

```javascript
const greet = (first, last) => `Hi ${first} ${last}`;
const person = ["John", "Doe"];

// Not so good
greet.apply(null, person);

// Better
greet(...person);
```

### Bind
Don't `bind()` when there's a more simplistic approach.

```javascript
// Not so good
["foo", "bar"].forEach(func.bind(this));

// Better
["foo", "bar"].forEach(func, this);

// Or 

// Not so good
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = function() {
      return `${this.first} ${this.last}`;
    }.bind(this);
    return `Hello ${full()}`;
  }
}

// Better
const person = {
  first: "John",
  last: "Doe",
  greet() {
    const full = () => `${this.first} ${this.last}`;
    return `Hello ${full()}`;
  }
}
```

### Higher-order functions
Make sure to only use nesting functions when there is a need.

```javascript
// Not so good
[1, 2, 3].map(num => String(num));

// Better
[1, 2, 3].map(String);
```

### Composition
Prefer composition over multiple nested function calls.

```javascript
const addOne = a => a + 1;
const timesTwo = a => a * 2;

// Not so good
console.log(timesTwo(addOne(5)));
// => 12

// Better
const stack = (...funcs) => input => funcs.reduce((acc, func) => func(acc), input);
const addThenMult = stack(addOne, timesTwo);
addThenMult(5);
// => 12
```

### Variables
Always use `const` or `let` to declare variables. Not doing so will result in global variables.

```javascript
// Not so good
var me = new Hero();
me.set("name", "Oliver").set("location", "Star City");

// Better
let me = new Hero();
me.set("name", "Oliver").set("location", "Star City");
```

Use one `const` or `let` declaration per variable.
One `const`, `let` per scope makes it easier to detect undeclared variables that may become implied globals.

```javascript
// Not so good
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// Worse
const items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// Better
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

`var` statements should always be in the beginning of their respective scope (function).
```javascript
// Not so good
function doSomething() {

  // some statements here

  var myVariable = "",
    someVariable;
}

// Better
function doSomething() {
  var myVariable = "",
    someVariable;

  // ...
}
```

` let ` and ` const ` are block scoped not function scoped and should always be at the top of their scope.

```javascript
// Not so good
function makeHero() {
  let hero,
    power;
  if ( condition ) {
    power = "";
    // ...
  }
}
// Better
function makeHero() {
  let hero;
  if ( condition ) {
    let power = "";
    // ...
  }
}
```

We recommend to group your `const`s first and then your `let`s.

```javascript
// Not so good
let i;
const items = getItems();
let football;
const goSportsTeam = true;
let len;

// Better
const goSportsTeam = true;
const items = getItems();
let football;
let i;
let length;
```

Chaining variable assignments (`const`, `let`) creates implicit global variables so avoid it.

```javascript
// BAD BAD BAD!
(function make() {
  let a = b = c = 1;
  // let a = ( b = ( c = 1 ) );
}());

console.log(a); // undefined
console.log(b); // 1
console.log(c); // 1

// Better
(function make() {
  let a = 1;
  let b = a;
  let c = a;
}());

console.log(a); // undefined
console.log(b); // undefined
console.log(c); // undefined
```

Avoid using unary increments and decrements `(++, --) `.

```javascript
// Not so good
const array = [1, 2, 3];
let sum = 0;
let totalCount = 0;
for (let i = 0; i < array.length; i++) {
  let value = array[i];
  sum += value;
  if (value) {
    totalCount++;
  }
}

// Better
const arr = [1, 2, 3];
const sum = arr.reduce((acc, val) => acc + val, 0);
const totalCount = arr.filter(Boolean).length;
```

### Conditions

Prefer `===` and `!==` over `==` and `!=`.

```javascript
// Not so good
if (number ==1) {
  ...
}
 
// Better
if (number === 1) {
  ...
}
```

Use explicit comparisons unless you are comparing `boolean`s.

```javascript
// Not so good
if (items.length) {
  // ...
}
if (text) {
  // ...
}
if (isActive === true) {
  // ...
}


// Better
if (items.length > 0) {
  // ...
}
if (text != '') {
  // ...
}
if (isActive) {
  // ...
}
```

Do not nest ternaries and always write them as a signle line expressions.

```javascript
// Not so good
const result = left > right
  ? 'do something'
  : top > bottom ? 'do something' : 'do nothing';

// Better
const action = top > bottom ? 'do something' : 'do nothing';
const result = left > right ? 'another stuff' : maybeNull;
```

Do not use ternary statements when there is no need.

```javascript
// Not so good
const name = nickname ? nickname : lastname;
const isActive = selected ? true : false;

// Better
const foo = nickname || lastname;
const isActive = !!selected;
```

Prefer IIFE's and return statements over if, else if, else and switch statements.

```javascript
// Not so good
var hero;
if (city === "Star City")
  hero = "Green Arrow";
else if (city === "Central City")
  hero = "The Flash";
else
  hero = "Person";

// Better
const hero = (() => {
  if (city === "Star City")
    return "Green Arrow";
  if (city === "Central City")
    return "The Flash";
  return "Person";
})();
```

### Blocks

Prefer multi-lines blocks.

```javascript
// Not so good
function make() { return false; }

// Better
function make() {
  return false;
}
```

When using multi-line blocks with if and else, put `else` and `if` block's closing brace on the same line.

```javascript
// Not so good
if (car) {
  start();
  drive();
}
else {
  ride();
}

// Better
if (car) {
  start();
  drive();
} else {
  ride();
}
```

### Type Casting

When casting to Boolean

```javascript
const age = 0;

// Not so good
const hasAge = new Boolean(age);

// Better
const hasAge = !!age;
```

When castign to String

```javascript
let view_count = 9;

// Not so good
const views = this.view_count.toString();

// Better
const view = String(this.view_count);
```

When casting to Number
```javascript
const inputValue = '8';

// Not so good
const val = parseInt(inputValue);

// Not so good
const val = +inputValue;

// Better
const val = Number(inputValue);

// Better
const val = parseInt(inputValue, 10);
```

If for some reason you ended up not using `parseInt` or `Number`, add your reason in a comment.

```javascript
/**
 * parseInt was the reason my code was very slow.
 * using Number made it faster.
 */
const val = +inputValue;
```
 
Remeber that Numbers are represented as 64-bit values but bitshift operations always generate a 32-bit integer so pay attention to unexpected behavior when dealing with integer values larger than 32 bits.
 
 ```javascript
2147483647 >> 0; // => 2147483647
2147483648 >> 0; // => -2147483648
2147483649 >> 0; // => -2147483647
```

### Object iteration
When you want to iterate over object, prefer `Object.keys()` / `Object.values()` / `Object.entries()` methods over `for...in`.

```javascript
const shared = { foo: "foo" };
const obj = Object.create(shared, {
  bar: {
    value: "bar",
    enumerable: true
  }
});

// Not so good
for (var prop in obj) {
  if (obj.hasOwnProperty(prop))
    console.log(prop);
}

// Better
Object.keys(obj).forEach(prop => console.log(prop));
```

When iterating over arrays, refer to `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... 

```javascript
const numbers = [1, 2, 3, 4, 5];

// Not so good
let sum = 0;
for (let num of numbers) {
  sum += num;
}
sum === 15;


// Better
const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;
```


### Events
always pass hash instead of raw value when attaching data payloads to events.

```javascript
// Not so good
$(this).trigger('LegendCreated', legend.name);

// ...

$(this).on('LegendCreated', (e, name) => {
  console.log(name);
});
 

// Better
$(this).trigger('LegendCreated', { name: legend.name });

// ...

$(this).on('LegendCreated', (e, data) => {
  console.log(data.name);
});
```

### jQuery

Always add `$` Prefix to your jQuery object variables.

```javascript
// Not so good
const navbar = $('.navbar');

// Better
const $navbar = $('.navbar');
```

Cache jQuery lookups.

```javascript
// Not so good
function updateStatus() {
  $('.signup-nav').hide();

  // ...

  $('.signup-nav').css({
    'background-color': '#d8d8d8',
  });
}

// Better
function updateStatus() {
  const $signupNav = $('.signup-nav');
  $signupNav.hide();

  // ...

  $signupNav.css({
    'background-color': '#d8d8d8',
  });
}
```

Use `find` with scoped jQuery object queries and use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')` when manipulating DOM.

```javascript
// Not so good
$('ul', '.signup-nav').hide();
$('.profile').find('img.avatar').fadeIn();

// Better
$('.signup-nav > ul').hide();
$profile.find('img.avatar').fadeIn();
```

### Objects as Maps

Use object method shorthand.

```javascript
// Not so good
const atom = {
  proton: 1,

  addProton: function (value) {
    return atom.protons + value;
  },
};

// Better
const atom = {
  protons: 1,

  addProton(value) {
    return atom.protons + protons;
  },
};
```

While objects have legitimate use cases, maps are usually a better, more powerful choice. When in
doubt, use a `Map`.

```javascript
// Not so good
let me = {
  name: "Doe",
  age: 30
};
let meSize = Object.keys(me).length;
me.country = "Mars";
meSize += 1;
console.log(meSize);
// => 3

// Better
let me = new Map();
me.set("name", "Doe");
me.set("age", 30);
me.size; // => 2
me.set("country", "Mars");
me.size; // => 3
```

### Strings
Prefer single quotes `''` for strings.

```javascript
// Not so good
const name = "Capt. Hunter";

// Better
const name = 'Capt. Hunter';
```

Prefer template strings over concatenation when building up strings.

```javascript
// Not so good
function sayHello(name) {
  return ['What's up, ', name, '?'].join();
}


// Better
function sayHello(name) {
  return `What's up, ${name}?`;
}
```
**Never use eval() on a string, it opens too many vulnerabilities.**

Do not unnecessarily escape characters in strings.

```javascript
// Not so good
const foo = '\'this\' \i\s \"quoted\"';

// Better
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

### Functions

Unless you have a very complicated function, use arrow function notation.

```javascript
// Not so good
[1, 2, 3].map(function (value) {
  const coefficient = value + 1;
  return value * coefficient;
});

// Better
[1, 2, 3].map((value) => {
  const coefficient = value + 1;
  return value * coefficient;
});
```

You may remove braces and use the implicit return only when your function body is a single expression. Otherwise, keep the braces and use a `return` statement.

```javascript
// Not so good
[10, 21, 33].map(number => {
  if (number % 3 === 0 ){
    `is even`;
  }
  `is odd`;
});

// Better
[10, 21, 33].map((number) => {
  if (number % 3 === 0 ){
    return `is even`;
  }
  return `is odd`;
});
```

When and only when your function takes a single argument and doesn’t use braces, you are allowed to remove parentheses.

```javascript
// bad
[1, 2, 3].reduce((val) =>  val * 3);

// Better
[1, 2, 3].map(val => val * 3);
```

Wrap immediately invoked function expressions in parentheses.

```javascript
(function () {
  console.log('You love simplicity? We do too.');
}());
```

Don't try to declare a function in a non-function block (if, while, etc).

```javascript
// Not so good
if (activeUser) {
  function isAdmin() {
    console.log('Nope.');
  }
}

// Better
let isAdmin;
if (currentUser) {
  isAdmin = () => {
    console.log('Yeah!');
  };
}
```

Don't name a parameter `arguments`.

```javascript
// Not so good
function doSomething(name, options, arguments) {
  // ...
}

// Better
function doSomething(name, options, args) {
  // ...
}
```

Don't use `arguments`, prefer rest syntax `...`.

```javascript
// Not so good
function sum() {
  const args = Array.prototype.slice.call(arguments);
  return args.reduce((acc, val) => acc + val, 0);
}

// Better
const sum = (...args) => args.reduce((acc, val) => acc + val, 0);
```

Never mutate functions arguments.

```javascript
// Not so good
function handleThings(options) {
  options = options || {};
  // ...
}

// Better
function handleThings(opts = {}) {
  // ...
}
```

Default parameter should be at the end.

```javascript
// Not so good
function manage(opts = {}, name) {
  // ...
}

// Better
function manage(name, opts = {}) {
  // ...
}
```


### Classes & Constructors

Prefer `class` over `prototype`.

```javascript
// Not so good
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};


// Better
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

You may use fluent API for method chaining.

```javascript
// Not so good
Hero.prototype.fight = function () {
  this.fighting = true;
  return true;
};

Hero.prototype.setPower = function (power) {
  this.power = power;
};

const oliver = new Hero();
oliver.setPower('Arrow');
oliver.fight();


// Better
class Hero {
  fight() {
    this.fighting = true;
    return this;
  },

  setPower(power) {
    this.power = power;
    return this;
  }
};

const oliver = new Hero();

oliver
  .setPower('Arrow');
  .fight()
```

### Modules
Modules are the future, let's start using the future now.

Always use modules (`import`/`export`) over a non-standard module system.

```javascript
// Not so good
const HeroFactory = require('./HeroFactory');
module.exports = HeroFactory.flash;

// Better
import { flash } from './HeroFactory';
export default flash;
```

Makes sure you have a single default export.

```javascript
// Not so good
import * as HeroFactory from './HeroFactory';

// Better
import HeroFactory from './HeroFactory';
```

Prefer default export over named export in modules with a single export.

```javascript
// Not so good
export function code() {}

// Better
export default function code() {}
```


### Readability

Make your code as simple and readable as possible.

```javascript
// Not so good
foo || doSomething();

// Better
if (!foo) doSomething();
```

You earn nothing try to complicate your code.

```javascript
// Not so good
const n = ~~3.14;

// Better
const n = Math.floor(3.14);
```

### Code reuse
For a better workflow and time optimization, create small and resusable functions.

```javascript
// Not so good
const times = (a, b) => a * b;
const triple = n => n * 3;

// Better
const times = (a, b) => a * b;
const triple = n => times(n, 3);
```

### Dependencies

Avoid using Third-party code (Library) when the code is easy to write.

```javascript
// Not so good
var _ = require("underscore");
_.compact(["foo", 0]));

// Better
const compact = arr => arr.filter(el => el);
compact(["foo", 0]);
```

### Test Facility

All projects must include some form of unit, or functional testing. You are free to you any framework you judge fine but do not forget to write a regression test for every bug you fix.

### Resources & References

A few resources to help you improve your JavaScript skills.

- [Learn ES6](https://babeljs.io/learn-es2015/)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript#resources)
- [Frontend Guidelines](https://github.com/bendc/frontend-guidelines)
- [You May Not Need jQuery](http://youmightnotneedjquery.com/)
- [Eloquent JavaScript](http://eloquentjavascript.net/)
- [jsFiddle](https://jsfiddle.net/)
- [Codepen](http://codepen.io/)
- [jsbin](https://jsbin.com/)
- [JavaScript Lint (JSL)](http://www.javascriptlint.com/)
- [jshint](http://jshint.com/)
- [jslint](http://www.jslint.com/)
- [eslint](http://eslint.org/)
- [jscs](http://jscs.info/)
- [Editorconfig](http://editorconfig.org/)

